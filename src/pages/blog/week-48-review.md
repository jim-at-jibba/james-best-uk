---
layout: ../../layouts/BlogLayout.astro
title: "Week 48: Discipline, Spaced Repetition, and Building for Users Who Matter"
description: "A week of building 2 terminal tools, implementing mastery systems, and learning why constraints make better software"
tags: ["weeknotes", "engineering", "ai-tools", "side-projects"]
time: 7
featured: true
timestamp: 2025-12-01T11:45:00+00:00
filename: week-48-review
---

This week I shipped features across three projects, discovered why Cerebrus is absurdly fast, and learnt that my daughter's engagement with educational software depends entirely on whether it has a heatmap. Here's what happened.

## The Discipline of Constraints

I read [The Discipline of Constraints](https://cekrem.github.io/posts/the-discipline-of-constraints-elm-usereducer-lessons/) this week—an article about what Elm teaches you about React's `useReducer`. The core insight hit hard: **the default case is where discipline goes to die**.

When you write a reducer with a default case that silently returns state, you've created a escape hatch for lazy thinking. That `any` type creeps in because someone needed to ship quickly. Unhandled actions get swallowed. You've gone from a system that forces careful thought about state transitions to one that lets you sweep complexity under the rug.

Elm wouldn't allow this for a second. Its type system forces exhaustive handling. You can't ignore an action—you must either handle it explicitly or document why you're not.

What Elm taught the author—and what resonated with me—isn't that React's approach is wrong. It's that **discipline is a muscle that needs exercise**. When the language forces you to be disciplined, you develop better habits.

Here's what I'm taking forward:

- **Never add a default case that just returns state**. If you're not handling an action, throw an error or comment why it's ignored.
- **Design invalid states out of existence**. Rather than separate booleans for `loading`, `error`, and `data`, use discriminated unions.
- **Exhaustive action handling**. Comment explicitly when intentionally ignoring an action.
- **Effect isolation**. Keep effects in custom hooks that communicate through dispatch.

This mindset directly influenced work on all three projects this week.

## IDA: Multi-Account Intelligence

IDA (Intelligent Digital Assistant) is my terminal-based AI assistant that integrates with Gmail, Calendar, Screen shots with OCR and local notes. This week brought 21 commits focused on making it genuinely useful rather than merely clever.

### Multi-Account Support

The biggest feature: multi-account support for Gmail and Calendar. Turns out people have more than one email address. Revolutionary insight, I know.

The implementation required rethinking how context gets filtered. When you ask "What's on my calendar today?", which calendar matters? The system now categorises questions intelligently and filters context accordingly.

### Conversation History

Added multi-turn chat with conversation history. Previously, each question existed in isolation. Now you can ask follow-up questions and IDA maintains context. This sounds simple but required careful thought about when to clear history versus when to maintain it.

### Slash Commands

Introduced slash commands for quick access to insights. Rather than asking full natural language questions, you can now type `/emails` or `/calendar` for immediate summaries. The interface stays conversational when you want it and efficient when you don't.

### The Cerebrus Experiment

I discovered Shore—a terminal-based LLM chat app—through a video recommendation. The creator mentioned using Cerebrus as an inference provider through Hugging Face. The speed is genuinely shocking. I've never seen response times like this.

I integrated Cerebrus into IDA for testing. The speed is remarkable but it struggles with following system prompts. Fast isn't useful if it ignores instructions. Still evaluating whether the trade-off is worth it for certain tasks.

**Key Statistics:**
- 21 commits total
- 6 new features
- 10 bug fixes
- Focus: context filtering, multi-turn chat, multi-account support

## Drill: Terminal-Based Spaced Repetition

Drill is a spaced repetition app built with Ink (React for CLIs). It uses Markdown for cards and Git for version control. I was inspired by GoCard but wanted it to work my way—and crucially, to work in light mode.

This week brought it from rough prototype to v0.1.1.

### Core Features Shipped

- **Title support** for better card organisation
- **Markdown formatting** for richer content (code blocks, lists, emphasis)
- **Tests, documentation, and validation** for the SRS algorithm and config

### Bug Fixes

- Fixed multiline cards display (turns out terminals are finicky about line breaks)
- Corrected stats summary (nothing kills trust like incorrect statistics)
- Improved question and answer display for clarity

### The SRS Implementation

The spaced repetition algorithm is straightforward but requires precision. Cards get reviewed at increasing intervals: 1 day, 3 days, 7 days, 14 days, 30 days. Get it wrong and the interval resets. Get it right and it extends.

The validation tests ensure the algorithm works correctly across edge cases. This is where the "discipline of constraints" thinking from that article mattered. Invalid states—like negative intervals or cards scheduled in the past—get designed out of existence through TypeScript's type system.

**Key Statistics:**
- 15 commits total
- 4 new features
- 3 bug fixes
- 6 documentation updates
- Released v0.1.1

## Word Buddies: When Gamification Actually Works

Word Buddies is a spelling game I built for my daughter. Initial excitement wore off quickly—she kept returning to TT Rockstars instead. So I studied what TT Rockstars does right and rebuilt Word Buddies around those insights.

### The Problem

Educational software often focuses on the educational part and forgets the software part. If children don't want to use it, the education never happens. My daughter needs spelling practise but she wasn't engaging with the tool I'd built.

### The Solution: Quest Mode

I introduced a complete mastery system with three progressive chapters, each with unique mechanics:

**Chapter 1: Classic Mode**
Standard spelling with preview phase. Learn the word, spell the word.

**Chapter 2: Listen & Spell**
No preview. Just listen and spell. Forces actual recall rather than short-term memory.

**Chapter 3: Challenge Mode**
10-second timer with response time bonuses. Fast correct answers grant extra mastery points.

### The Mastery System

Six levels from "Need Practise" to "MASTERED!", using spaced repetition intervals (0d, 1d, 3d, 7d, 14d, 30d). Correct answers move you up one level. Incorrect answers drop you two levels. Chapter 3 speed bonuses can add an extra level.

The key insight: children need **visible progress**. Adults might internalise improvement. Children need to see it.

### The Heatmap

This was the breakthrough. I added a heatmap showing mastery levels in a six-colour grid (red through dark green). Every word visible. Every improvement tracked.

My daughter's engagement transformed immediately. She started chasing "all green". The heatmap made progress tangible in a way statistics never could.

### Technical Implementation

- **Database Schema v3** with `masteryLevel`, `consecutiveCorrect`, and `responseTime` fields
- **TypeScript strict mode** with zero errors
- **17 unit tests** covering core mastery logic
- **Batch word updates** for performance
- **Tutorial system** explaining how mastery works

18 commits over two sessions, roughly six hours of focused work. ~2000 lines changed across 20 files.

**Result:** Production-ready Quest Mode with sophisticated mastery tracking.

## Patterns Across Projects

Looking across IDA, Drill, and Word Buddies, several patterns emerge:

### 1. Terminal-First Development

Two of the three projects embrace terminal UIs. This isn't aesthetic preference—it's about focus. Terminal applications eliminate distraction. No notifications. No tabs. Just the task at hand.

Building with Ink makes terminal UIs genuinely pleasant to build. The React mental model translates surprisingly well to terminal rendering.

### 2. Spaced Repetition Everywhere

Two of three projects implement spaced repetition algorithms. There's something compelling about systems that adapt to what you know and don't know. Done correctly, they minimise wasted effort whilst maximising retention.

The algorithms aren't complex. The challenge is implementation discipline—ensuring intervals calculate correctly, stats track accurately, and edge cases get handled properly.

### 3. Building for Specific Users

Word Buddies exists for one user: my daughter. This specificity made it better software. I wasn't trying to solve spelling practise for all children. I was solving it for one child whose engagement I could directly observe.

When she gravitated to TT Rockstars over Word Buddies, I didn't need surveys or analytics. I watched her choose and asked why. The answer (visible progress through heatmaps) became the solution.

IDA and Drill follow similar patterns. I'm building tools I need, which means I immediately know when they're not working.

### 4. Constraints Breed Quality

That article about Elm's constraints applies across all three projects. When you can't take shortcuts, you build better foundations.

TypeScript's strict mode forced careful thinking about state transitions in Word Buddies. The result: zero runtime errors related to mastery calculations.

Markdown as the storage format for Drill seemed limiting initially. In practise, it meant cards remain portable, version-controllable, and readable without the application.

IDA's multi-account support required explicit context filtering. The constraint (which account's data matters?) forced better question categorisation.

## Miscellaneous Discoveries

**LEGO × Nintendo:** Finished the Game Boy build this week. Excellent construction, satisfying clicks, and nostalgic in the best way. The partnership produces genuinely good sets rather than lazy cash-ins.

**Shore CLI:** Terminal-based LLM chat that introduced me to Cerebrus. Worth exploring if you live in the terminal.

## What's Next

Word Buddies needs user testing (the specific user is currently at school). IDA's Cerebrus integration needs evaluation—speed versus instruction-following is an interesting trade-off. Drill needs real-world usage to find gaps in the SRS implementation.

The broader pattern continues: build tools I need, ship incremental improvements, observe what works. No grand plans. Just useful software that solves actual problems.

The discipline of constraints keeps proving its value. Invalid states designed out of existence. Explicit error handling. Type systems that force careful thought. These aren't burdens—they're force multipliers for small projects where quality matters more than speed.

Building three projects simultaneously sounds scattered. In practise, they inform each other. Patterns learned in one apply to others. The mastery system from Word Buddies could improve Drill's SRS implementation. IDA's context filtering logic might help Drill categorise cards.

Next week: more of the same. Small improvements. Specific users. Terminal UIs. Constraints that force better thinking.

The work continues.

