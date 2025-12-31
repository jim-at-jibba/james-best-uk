---
layout: ../../layouts/BlogLayout.astro
title: "Building at the Speed of Thought: A Year of AI-Assisted Development"
description: "Reflections on shipping 20+ projects by partnering with AI to validate ideas faster"
tags: ["ai", "productivity", "mobile", "engineering"]
time: 6
featured: true
timestamp: 2025-12-31T10:00:00+00:00
filename: 2025-a-busy-year-building
---

This year has been transformative. Not because I learnt a revolutionary new framework or switched tech stacks, but because I fundamentally changed how I validate ideas. By treating AI as a development partner rather than just a code completion tool, I've shipped more projects in 2025 than in the previous three years combined.

## The Numbers
The velocity speaks for itself:
- **20+ projects** shipped across mobile, web, and developer tooling
- **~3,000 commits** pushed over the year
- **3 active projects** still in development
- **10 complete projects** shipped and stable
- **2 projects** retired to the graveyard

These aren't vanity metrics—they represent a fundamental shift in how quickly I can move from idea to validated prototype.

## The Shift: From Planning Paralysis to Rapid Prototyping

Previously, ideas would linger in my notebook for months. The friction of starting—setting up boilerplate, wrestling with authentication flows, configuring build systems—meant only the most compelling concepts made it past the ideation phase.

With AI assistance, that friction disappeared. An idea that surfaces during breakfast can be a working prototype by lunch. This velocity has completely changed my relationship with side projects. The question is no longer "Is this worth the investment?" but rather "Let's build it and see."

## Three Categories of Projects

My project graveyard is no longer a place of abandoned dreams—it's a collection of validated hypotheses. Here's how my work naturally organised itself:

### In Progress: The Keepers

**Komitto** emerged from a personal need to track habits in a way that felt engaging rather than punishing. The streak-based mechanics combined with journalling capabilities kept me coming back. It's built with Expo, and the mobile-first approach has been crucial for capturing daily check-ins.

**ContentSage** started as a shell script to analyse bug videos for the mobile app I build at Breedr, hoping to speed up triage for our QA team. When the script proved useful, it evolved into a desktop app for easier engagement. Eventually, I added multi-tenancy with Turso (libsql), transforming it into a full video analysis platform.

**Kyo** represents my most ambitious undertaking—a suite of productivity tools designed specifically for ADHD brains. The mobile app focuses on impulse control and managing emotional dysregulation, addressing challenges that traditional productivity tools overlook. What started as browser extensions evolved into a comprehensive system that helps users navigate the unique difficulties of neurodivergence.

### Complete: Shipped and Stable

Some projects reach a natural resting point where they're feature-complete for their intended scope:

**[OpenSpec](https://openspec.dev/)** was my first significant open-source contribution this year. The specification-driven development approach elegantly solves the problem of helping AI assistants understand project context. Contributing to this tool improved how I document my own work by adding support for Opencode.

**[ThoughtScribe](https://thoughtscribe.uk/)** validates a hypothesis about friction in voice notes. By combining Expo's audio capabilities, Supabase's real-time sync and OpenAi transcirption APIs, I created a transcription tool that's genuinely useful in my daily workflow.

**[nvim-redraft](https://github.com/jim-at-jibba/nvim-redraft)** brings AI-powered inline code editing to Neovim, supporting multiple LLM providers (OpenAI, Anthropic, xAI, GitHub Copilot, OpenRouter, Cerebras). Solving my own editor frustrations resulted in a plugin others found useful.

**[nvim-stride](https://github.com/jim-at-jibba/nvim-stride)** brings Cursor-like tab completion to Neovim, providing multi-line code completions and NES (Next Edit Suggestions) powered by Cerebras. The ultra-low latency makes it feel native, and the completion and refactor modes have become essential in my workflow.

**[drill](https://github.com/jim-at-jibba/drill)** is a terminal-based spaced repetition system using plain Markdown flashcards with the SM-2 algorithm. Built for developers who prefer text files and Git version control over proprietary SRS tools.

**[Word Buddies](https://word-buddies.co.uk/)** was built for my daughter to help with her spelling practice. Combining Next.js with audio pronunciation and spaced repetition algorithms, it's become a genuinely useful tool in her learning routine. Watching your own work help your child improve their skills is remarkably rewarding.

### The Graveyard: Failed Fast, Learnt Faster

Not every idea deserves to exist long-term, and that's perfectly fine:

**[Voidpad](https://voidpad.jamesbest.uk/)** aimed to be a "beautiful digital scratchpad" for disposable thoughts. After building it, I discovered another app that executed the concept far better. Rather than compete, I shelved it—a good reminder that sometimes the best decision is recognising when someone else has already solved the problem.

**[Cortex](https://github.com/jim-at-jibba/cortex)** attempted to create a local-first knowledge management CLI with semantic search. Whilst the technical implementation was solid, the approach was superseded by Ida—a terminal-based AI assistant that monitors calendar, email, tasks, and Obsidian notes to provide intelligent, context-aware assistance. Ida better solved the problem I was actually trying to address.

## Patterns That Emerged

Several principles crystallised through this rapid prototyping approach:

### Start with the Hard Bit

I now tackle the most uncertain technical challenge first. For ContentSage, that was multi-tenant data isolation. For Kyo, it was the adaptive algorithms. If the core risk isn't viable, better to learn that on day two rather than week six.

### Mobile-First Matters

Five of my successful projects are mobile apps built with Expo. The React Native ecosystem has matured to the point where I can ship production-quality apps with excellent developer experience. The constraint of mobile forces clearer UX decisions.

### Developer Tooling Creates Real Value

Building [nvim-redraft](https://github.com/jim-at-jibba/nvim-redraft), [nvim-prophecy](https://github.com/jim-at-jibba/nvim-prophecy), and [drill](https://github.com/jim-at-jibba/drill) taught me that solving your own tooling problems creates genuinely useful open-source projects. These tools emerged from daily frustrations, which means they solve real problems rather than imagined ones.

### Building for Neurodivergence

My focus on ADHD-friendly tools (Kyo Shift, Kyo Notes, Kyo mobile app) stems from building for myself. The mobile app's focus on impulse control and emotional dysregulation addresses real gaps in existing productivity tools. Neurodivergent developers have unique insights into alternative interaction patterns that often benefit everyone.

## The AI Partnership Model

Working with AI isn't about generating boilerplate and calling it done. The most effective approach I've found is:

1. **Rapidly scaffold the prototype** - Let AI handle the tedious setup whilst I focus on architecture decisions
2. **Validate the core hypothesis** - Does this idea actually solve the problem?
3. **Refine through iteration** - This is where human judgement becomes crucial
4. **Know when to stop** - Not every project needs to scale to production

The key insight is that AI accelerates the journey to "no" as much as it accelerates the journey to "yes." Finding out an idea isn't viable after two days of work is a win, not a failure.

## What's Next

I can't promise I won't start new projects—ideas still arrive in the shower with the same frequency—but I'm committed to finishing what's in flight. Kyo, Komitto, and ContentSage deserve the attention required to become genuinely excellent rather than merely functional.

Beyond that, two principles remain:

**Open-source by default** - My Neovim plugins and contributions to OpenSpec have been the most rewarding work. I'm committing to more public building.

**Writing alongside building** - Sharing what I learn whilst building is as valuable as the code itself. This post is part of that commitment.

## Reflection

The graveyard isn't a collection of failures—it's evidence of a healthier development process. Each abandoned project represents a validated learning. The completed projects prove I can ship. The in-progress work shows I can sustain momentum.

Working at the intersection of mobile development and AI tooling has been fascinating. The barrier to creating useful AI-enhanced applications is lower than ever, but the craft of building genuinely helpful tools remains as challenging as it's always been.

The partnership with AI hasn't made me a better coder per se—it's made me better at validating ideas. And in a world where we're drowning in possibilities, that might be the more valuable skill.

---

*Building Kyo, ThoughtScribe, and various other experiments. Interested in ADHD-focused productivity tools, mobile development, and AI-assisted workflows. Find my work at [jamesbest.uk](https://jamesbest.uk).*

