---
layout: ../../layouts/BlogLayout.astro
title: "New Company, Home Labs, and Getting back in to Tmux"
description: "A week of new beginnings at a fintech startup, finally setting up a home lab, and rediscovering the joy of Tmux"
tags: ["weeknotes", "engineering", "homelab", "ai-tools", "side-projects"]
time: 5
featured: true
timestamp: 2026-03-05T09:00:00+00:00
filename: 2026-03-starting-again
---

It's taken a while to get these notes back on track this year. A busy start, a new company, and the mental overhead that comes with both. But the fog is lifting. Here's what's been happening.

## Starting Fresh at Sidekick Money

I joined [Sidekick Money](https://www.sidekickmoney.com/) at the start of the year—a fintech startup with a genuinely compelling mission: bringing proper banking facilities to the mass affluent. The people who are too wealthy for standard high-street products but not wealthy enough to access the private banking tier. It's an underserved segment, and the problem is interesting.

Starting somewhere new is always expensive in ways that aren't immediately obvious. The cognitive cost is significant. You're not just learning a codebase—you're learning how a team communicates, what matters to them, how decisions get made, where the bodies are buried. For the first few weeks, you're running at capacity just staying oriented.

That's why the weeknotes went quiet. Not for lack of things happening, but because the mental capacity wasn't there once the working day was done.

That's changed now. I feel settled enough to start building again outside of work hours.

## The Home Lab: Why Did I Wait So Long?

The headline from the past few weeks: I finally set up my home lab.

The hardware was sitting there all along—an old MacBook Pro that had been gathering dust for longer than I'd care to admit. I kept putting it off, telling myself I'd do it properly, find the right time, plan it thoroughly. Classic overthinking.

I wish I hadn't waited. It's excellent.

There's something genuinely satisfying about having infrastructure you own and control. No cloud bills. No vendor decisions made without you. No wondering what's happening to your data. Just a machine in your house, running services you chose, configured the way you want.

The setup involved more decision-making than I expected—but the good kind. Which services to self-host, how to structure the network, what to expose and what to keep local. Constraints that force clarity.

I'm also using a Raspberry Pi as a thin client to connect to it. The combination works beautifully. The Pi handles display and input; the old MacBook does the actual work. It's a proper separation of concerns in physical form.

There will be dedicated articles on how I set it all up. The home lab journey deserves more than a paragraph.

## Back in Tmux

I used Tmux for years. Then I switched to [Ghostty](https://ghostty.org/) and quietly stopped.

It wasn't a deliberate decision. Ghostty just handled so much of what I'd been using Tmux for — split panes, tabs, a fast terminal experience that didn't feel like a compromise. The day-to-day friction that Tmux had been solving was gone, and with it, the habit.

For local development, that trade-off made sense. Ghostty is genuinely excellent and I don't miss the overhead of managing Tmux sessions for work I'm doing on my own machine.

The home lab changed the calculation.

SSHing into a remote machine is where Tmux earns its keep in ways no local terminal emulator can replicate. Sessions that persist when your connection drops. The ability to detach, walk away, come back later and find everything exactly as you left it. Multiple windows on a server that has no GUI. These aren't features Ghostty can provide — they're not even in the same category of problem.

So the return wasn't about abandoning Ghostty. Both have a place now. Ghostty for local work. Tmux for the home lab and anything remote. The right tool, in the right context.

## STEM Buddies Returns

STEM Buddies is back after a break over Christmas and into the new year. Getting back into running these sessions always takes a bit of effort—not because the sessions themselves are difficult, but because the scheduling and logistics eat time.

It's worth it. Teaching technical concepts to young people forces you to understand them more precisely. You can't hide behind jargon when your audience will immediately ask what the word means.

## What's Being Built

Despite the quieter period, a few projects have been gestating:

**Prompt Party** — a terminal-based tool for working with prompts. Early days, but the idea is solid. Prompt management is surprisingly messy for how central prompts have become to everyday development work.

**Qmdf** — a TUI wrapper around `qmd`. I find myself using quarto regularly but the command-line interface has friction I want to eliminate. A proper TUI should help.

**Falimy** — a privacy-first family app where all data stays on your self-hosted backend. More to come.

The common thread across these: built for my own workflow, solving friction I encounter daily. Most lean terminal-first, though not all — Falimy is a different kind of project entirely, and the home lab makes it possible.

## Patterns Worth Noting

Starting a new job and returning to personal projects in the same period is instructive.

At work, you inherit constraints: existing architecture, existing patterns, existing decisions. Some are good. Some you'd do differently. Learning to work within those constraints—and choosing carefully which ones to push back on—is a skill that matters.

On personal projects, you have full autonomy. Which sounds freeing but can actually be paralysing. The absence of constraints requires you to impose your own. The home lab forced me to think carefully about what I actually wanted to self-host. The terminal-first constraint on my projects forces clarity about what the tool actually needs to do.

There's a useful feedback loop between the two. The discipline required to work effectively within someone else's system makes you better at designing your own. The freedom of your own projects keeps the creative muscles from atrophying.

## What's Next

The home lab documentation needs writing while it's still fresh. The terminal projects need momentum now that mental capacity is returning. STEM Buddies needs a proper schedule.

The broader pattern: get back into rhythm. Weeknotes. Building. Learning. The interruption was necessary and the restart is overdue.

Good to be back.

