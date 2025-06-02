---
layout: ../../layouts/BlogLayout.astro
title: "Building Whilst on Holiday: A Week of Personal Projects and Production Polish"
description: "Reflections on balancing annual leave with coding passion projects, from spelling apps to mobile architecture decisions"
tags:
  [
    "technical-leadership",
    "mobile-development",
    "personal-projects",
    "react-native",
  ]
time: 6
featured: true
timestamp: 2025-06-02T14:30:00+00:00
filename: wkend-01-06
---

Welcome to the first instalment of my weekly rundowns—a new series where I'll be sharing what I've been working on, reading, and learning each week. As a lead engineer building mobile apps with a focus on AI tools, I find myself constantly exploring new technologies, refining existing systems, and balancing the demands of technical leadership with hands-on development.

These posts will capture the reality of modern engineering: the personal projects that scratch creative itches, the production systems that demand careful attention, and the continuous learning that keeps our craft evolving. Think of it as a weekly snapshot of an engineer's mind in motion.

This week started with annual leave, which for many engineers means one thing: finally having uninterrupted time to work on those personal projects that have been gathering digital dust. There's something uniquely satisfying about coding without meetings, without sprint pressures, and without the constant ping of Slack notifications.

## The Parent-Engineer Dilemma: Build vs Buy

The week's most interesting challenge emerged from an unexpected source: my 8-year-old's spelling practice. After discovering that the educational app we'd been using wanted £7.99 monthly for premium features, I found myself facing the classic engineer's dilemma. Do I pay the subscription, or do I build something better?

You can probably guess which path I chose.

**Word Buddies** became my holiday passion project—a spelling and word game app built from scratch as a companion to the STEM website I also created for my daughter, **STEM Buddies** (available at [stem-buddies.co.uk](https://stem-buddies.co.uk)). Over 30 commits later, I've implemented a Spelling Bee game with word list support, a Word Search game with grid selection and scoring, and a complete profile management system with encrypted storage.

The app is still very much in active development and will continue to evolve over the coming weeks as I add more educational games and features. The satisfaction of watching my daughter play a game I built specifically for her learning needs? Priceless.

But this raises an interesting question about our industry's relationship with the "build vs buy" decision. How often do we default to building because we can, rather than because we should? In this case, the educational value for both my daughter and my own learning justified the time investment, but it's worth reflecting on when this impulse serves us well and when it doesn't.

## Production Engineering: The Art of Incremental Polish

Whilst working on personal projects, the production systems kept demanding attention. **Breedr Mobile** saw 34 commits focused primarily on UI refinement and user experience improvements. The work included migrating styles to unistyles for better maintainability, fixing spacing issues across multiple components, and enhancing the draft section layout with responsive flex design.

What strikes me about this pattern is how much of production engineering involves these small, incremental improvements. Renaming `DraftSection` to `GroupDraftSection` for clarity, adjusting draft header heights, improving alert indicator styling—none of these changes will make headlines, but collectively they represent the unglamorous work that separates polished products from merely functional ones.

## The Rhythm of Feature Development

**Komitto**—one of my latest personal projects focused on helping users track and complete personal challenges like "30 days of cold showers" or "75 Hard"—dominated the commit count this week with 130 commits, representing the bulk of active feature development. The challenge management platform saw significant enhancements to its task management capabilities, dashboard improvements, and the addition of templates with quick-start functionality.

The commit breakdown tells an interesting story:

- 78 new features
- 43 improvements and refactoring
- 10 bug fixes

This 6:3:1 ratio suggests a project in active growth phase, where new functionality is outpacing maintenance work. As a lead engineer, these metrics help me understand project health and development momentum.

## React Native and Modern Tooling

Across all three projects, I've been impressed by how React Native's ecosystem continues to mature. The integration of react-hook-form in Komitto's task management, TanStack Router's navigation patterns in Word Buddies, and the seamless use of unistyles for design system consistency in Breedr all speak to a platform that's found its stride.

The testing story has also improved dramatically. Implementing comprehensive test suites using vitest for the word games felt natural and productive—a far cry from the React Native testing experience of just a few years ago.

## Balancing Personal and Professional

This week reinforced something I've been thinking about: the value of personal projects for lead engineers. Building Word Buddies reminded me of the pure joy of creating something from nothing, whilst the production work on Breedr and Komitto kept me grounded in the realities of maintaining complex systems at scale.

The cognitive switching between these contexts—from experimental game development to production mobile app refinement—exercises different engineering muscles. Personal projects allow for architectural experimentation and rapid iteration, whilst production work demands discipline, attention to detail, and systems thinking.

## Looking Ahead

As I transition back from holiday mode to full lead engineer responsibilities, I'm carrying forward a few observations:

The importance of maintaining deep technical expertise whilst providing technical leadership cannot be overstated. This week's 194 total commits across three projects reminded me why I fell in love with software engineering in the first place.

The educational technology space remains ripe for innovation, particularly in creating engaging experiences that respect both children's learning needs and parents' budgets.

React Native continues to be an excellent choice for cross-platform mobile development, especially when combined with modern tooling and testing practices.

Sometimes the best professional development happens during personal time, when we're free to experiment, learn, and create without constraint.

The week ahead will likely bring fewer commits but deeper architectural thinking as I return to the lead engineer rhythm. Both modes have their place, and the tension between them keeps the work interesting.

Remember: effective technical leadership requires staying close enough to the code to understand implementation details, whilst maintaining enough perspective to guide architectural decisions and mentor the team. This week provided a valuable recalibration of that balance.
