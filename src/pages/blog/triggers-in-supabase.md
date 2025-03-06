---
layout: ../../layouts/BlogLayout.astro
title: "Automatic API Key Generation with PostgreSQL Triggers"
description: "A practical guide to automating secure API key generation when users register in your application"
tags: ["postgresql", "security", "supabase", "database", "authentication"]
time: 7
featured: true
timestamp: 2025-03-10T14:45:00+00:00
filename: triggers-in-supabase
---

Having recently worked on a project where we needed to automatically generate API keys for users upon registration, I discovered an elegant solution using PostgreSQL triggers. In this post, I'll walk through how to implement this pattern in your own applications, particularly when working with Supabase or similar PostgreSQL-based backends.

## The Challenge

When building applications with API access, a common requirement is generating secure tokens for each user. Ideally, this should happen:

1. Automatically when users register
2. Without requiring additional application code
3. Securely, with proper permissions

Rather than handling this in your application layer, PostgreSQL's trigger system offers a more robust and centralised approach.

## Understanding Database Triggers

Triggers in PostgreSQL are special functions that execute automatically when specific database events occur. They're particularly useful for:

- Enforcing business rules
- Maintaining relationships between tables
- Automating processes like the one we're discussing today

Let's see how we can leverage this powerful feature to solve our API key generation challenge.

## Implementation Approach

We'll create a system that automatically generates and stores an API key whenever a new user signs up. Here's the overall architecture:

1. A function to generate secure random tokens using pgcrypto
2. A trigger function that runs on user creation
3. A trigger that connects our function to the user registration event
4. Appropriate permissions to ensure everything works securely

Let's dive into the implementation.

## Step 1: Creating a Token Generator Function

First, we need a way to generate secure random strings. We'll use PostgreSQL's `pgcrypto` extension, which provides cryptographically strong random generation:

```sql
-- Enable the pgcrypto extension if not already enabled
CREATE EXTENSION IF NOT EXISTS pgcrypto;

CREATE OR REPLACE FUNCTION generate_secure_token(length INT DEFAULT 32)
RETURNS TEXT AS $$
DECLARE
  bytes BYTEA;
  token TEXT;
BEGIN
  -- Generate cryptographically strong random bytes
  bytes := gen_random_bytes(length);
  -- Convert to a hexadecimal string
  token := encode(bytes, 'hex');
  -- Return the first 'length' characters
  RETURN LEFT(token, length);
END;
$$ LANGUAGE plpgsql;
```

This function uses `pgcrypto.gen_random_bytes()` to generate truly random data, which is then encoded as a hexadecimal string.

## Step 2: Creating the Trigger Function

Next, we'll create a function that will be called whenever a user signs up:

```sql
CREATE OR REPLACE FUNCTION handle_new_user()
RETURNS TRIGGER AS $$
DECLARE
  secure_token TEXT;
BEGIN
  -- Generate our secure token
  secure_token := generate_secure_token(32);

  -- Insert the user's ID and token into the profiles table
  INSERT INTO profiles (user_id, api_key)
  VALUES (NEW.id, secure_token);

  RETURN NEW;
END;
$$ LANGUAGE plpgsql SECURITY DEFINER;
```

The `SECURITY DEFINER` clause is particularly important—it ensures the function runs with the privileges of its creator rather than the caller, which helps overcome potential permission issues.

## Step 3: Setting Function Ownership and Permissions

For our trigger to work properly, we need to ensure it has the correct ownership and execution permissions:

```sql
-- Set appropriate ownership
ALTER FUNCTION handle_new_user() OWNER TO postgres;

-- Grant execution permissions
GRANT EXECUTE ON FUNCTION handle_new_user() TO authenticated, service_role;
```

## Step 4: Creating the Trigger

Now we connect our trigger function to the user registration event:

```sql
CREATE TRIGGER on_user_signup
AFTER INSERT ON auth.users
FOR EACH ROW
EXECUTE FUNCTION handle_new_user();
```

This tells PostgreSQL to run our function automatically after each new row is inserted into the `auth.users` table.

## Step 5: Granting Necessary Permissions

We need to ensure our function can insert rows into the profiles table:

```sql
GRANT INSERT ON TABLE profiles TO authenticated, service_role;
```

## Step 6: Configuring Row-Level Security

If you're using Supabase or have Row-Level Security (RLS) enabled, you'll need policies that allow the insertion:

```sql
-- Basic policy allowing users to insert their own row
CREATE POLICY "Allow user insert"
ON profiles
FOR INSERT
WITH CHECK (auth.uid() = user_id);

-- Optional more permissive policy for service roles
CREATE POLICY "Allow service role inserts"
ON profiles
FOR INSERT
WITH CHECK (auth.uid() IS NOT NULL);
```

## Verifying Your Setup

After implementing these changes, you can verify everything is working correctly with these diagnostic queries:

```sql
-- Check if the pgcrypto extension is installed
SELECT * FROM pg_extension WHERE extname = 'pgcrypto';

-- Check if the function exists and has correct ownership
SELECT nspname, proname, proowner::regrole
FROM pg_proc
JOIN pg_namespace ON pg_proc.pronamespace = pg_namespace.oid
WHERE proname = 'handle_new_user';

-- Check if the trigger is properly attached
SELECT event_object_table, trigger_name, action_statement
FROM information_schema.triggers
WHERE trigger_name = 'on_user_signup';

-- Verify RLS policies
SELECT * FROM pg_policies WHERE tablename = 'profiles';
```

## Benefits of This Approach

By implementing API key generation at the database level, we gain several advantages:

1. **Separation of concerns**: Authentication logic stays close to our user data
2. **Reduced application complexity**: No need for additional API endpoints or handlers
3. **Consistency**: Keys are generated reliably regardless of registration path
4. **Security**: With proper RLS policies and cryptographically strong random generation, we maintain robust security

## Potential Enhancements

While this implementation works well for many applications, you might consider these enhancements:

- Add key rotation capabilities through additional triggers
- Implement expiration timestamps for your API keys
- Create audit logging for key usage

## Conclusion

PostgreSQL triggers offer an elegant way to handle API key generation without cluttering your application code. By implementing this pattern with pgcrypto, you create a more robust system that leverages the database's strengths for authentication-related tasks.

This approach has significantly improved our architecture by reducing the complexity of our application layer whilst ensuring consistent security practices. The declarative nature of PostgreSQL triggers makes the system's behaviour clear and the centralised implementation makes it easier to audit and maintain.

By using pgcrypto's gen_random_bytes function, we ensure our API keys are generated with cryptographically strong randomness, providing a higher level of security than approaches using less secure randomization methods.

Remember that while this implementation works well, you should always consider your specific security requirements. For particularly sensitive applications, you might want to integrate additional security measures or use dedicated authentication services alongside this approach.
