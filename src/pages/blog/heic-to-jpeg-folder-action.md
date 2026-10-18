---
layout: ../../layouts/BlogLayout.astro
title: "HEIC to JPEG on Autopilot: A Folder Action for My Downloads"
description: "How I set up a tiny macOS automation that turns every HEIC photo landing in Downloads into a JPEG, and why launchd wasn't the right tool for it."
tags: ["macos", "automation", "productivity", "ai"]
time: 5
featured: true
timestamp: 2026-10-18T10:00:00+01:00
filename: heic-to-jpeg-folder-action
type: build-log
---

It's been a while since I last wrote a post, so it feels good to be back with something small and practical.

I copy photos from my phone to my laptop all the time. They arrive as HEIC, Apple's default image format, and that's fine right up until I need to put them somewhere else. Some of the coding harnesses (I'm looking at you Opencode) I use don't cope with HEIC, so I end up converting files by hand, one at a time, usually at the exact moment I'm trying to do something else.

Yesterday I finally automated it. Any HEIC file that lands in `~/Downloads` now gets a JPEG sitting next to it within a second or two. It took two attempts and one slightly alarming malware warning to get there, so here's the whole journey.

## The shape of it

The final setup has two parts:

1. **A trigger**: a macOS Folder Action attached to `~/Downloads`, which runs a small AppleScript at `~/Library/Scripts/Folder Action Scripts/heic-to-jpeg.scpt`.
2. **A converter**: a shell script in my dotfiles, `~/dotfiles/utilities/heic-to-jpeg.sh`, which does the actual work using `sips`.

Keeping the logic in a shell script in my dotfiles, rather than inside the AppleScript, means it's version-controlled, easy to read, and I can run it by hand whenever I like.

## The converter

`sips` is the image tool built into macOS. Most people never touch it, but it can resize, rotate and convert images from the command line, with nothing to install. Here's the whole script:

```bash
#!/usr/bin/env bash

# Convert HEIC files in a folder to JPEG alongside the originals (originals kept)
# Usage: heic-to-jpeg.sh [folder]
# Run by the heic-to-jpeg.scpt Folder Action attached to ~/Downloads

set -euo pipefail

WATCH_DIR="${1:-$HOME/Downloads}"

shopt -s nullglob nocaseglob

for INPUT_FILE in "$WATCH_DIR"/*.heic; do
	OUTPUT_FILE="${INPUT_FILE%.*}.jpg"

	# Already converted on a previous run
	[ -e "$OUTPUT_FILE" ] && continue

	echo "$(date '+%F %T') Converting '$INPUT_FILE'"
	if ! sips -s format jpeg -s formatOptions best "$INPUT_FILE" --out "$OUTPUT_FILE" >/dev/null; then
		# Remove partial output so the next trigger retries
		rm -f "$OUTPUT_FILE"
		echo "$(date '+%F %T') Failed: '$INPUT_FILE'" >&2
	fi
done
```

A few details that matter more than they look:

- **`nocaseglob`** catches both `.heic` and `.HEIC`. iPhones use the uppercase version, and it's an easy thing to miss.
- **It skips anything that already has a JPEG.** The script scans the whole folder each time rather than tracking individual files, so this check is what stops it converting the same photo over and over.
- **Failed conversions clean up after themselves.** If `sips` falls over halfway, the partial JPEG gets deleted. Otherwise the skip check would see a broken file, assume the job was done, and never try again. Deleting it means the next trigger has another go.
- **Originals are kept.** I went back and forth on this, but disk space is cheap and HEIC is still the better format on Apple devices. I'd rather have both than lose the original.

## Attempt one: launchd

My first instinct was launchd. I already run a handful of `com.user.*` LaunchAgents for my vault (daily notes, session summaries and so on), and a LaunchAgent with `WatchPaths` pointed at Downloads seemed like the obvious fit.

It loaded and fired when a file arrived, but it converted nothing. Run by hand, the script worked perfectly. The most likely explanation is macOS privacy controls: Downloads is a protected folder, and a background job running `/bin/bash` doesn't automatically get permission to see inside it. I never fully confirmed that from the logs, but the behaviour fitted.

## The malware warning

Then CleanMyMac popped up and flagged my brand new script as `Generic.Adware`.

That was a slightly uncomfortable moment, but it made sense once I thought about it. "Generic" means a pattern match, not a known threat. The pattern was a background job that silently runs a shell script whenever your Downloads folder changes, and that's exactly how a lot of adware keeps itself running. My script was harmless: no network access, nothing installed, no settings changed. But from the outside it looked suspicious.

The fix is to choose **Ignore** (ideally "always ignore") rather than **Remove Threats**, which would delete the script. It's a good reminder, though, that automations you build yourself can look a lot like the things security tools are designed to catch. It's worth knowing what's running on your machine and why, so you can tell the difference when the alert appears.

## Attempt two: Folder Actions

Folder Actions are one of those macOS features that have been around forever and that hardly anyone remembers. You attach an AppleScript to a folder, and macOS runs it whenever items are added. They were switched off system-wide on my Mac, so step one was turning them back on.

The AppleScript is tiny. It just hands the folder over to the shell script and logs the output:

```applescript
on adding folder items to this_folder after receiving added_items
	do shell script "/bin/bash $HOME/dotfiles/utilities/heic-to-jpeg.sh " & quoted form of POSIX path of this_folder & " >> /tmp/heic-to-jpeg.log 2>&1"
end adding folder items to
```

This version worked first time. I tested two cases:

1. **A file copied straight into Downloads**, which converted within a second or two.
2. **A file saved under a temporary name and then renamed**, which is how Chrome saves downloads. This also converted, which mattered more than I'd expected.

With that working, I removed the old LaunchAgent so there weren't two things watching the same folder.

## What I'd tell you if you want to do the same

1. **Put the logic in a shell script and keep the trigger thin.** That way you can swap launchd for Folder Actions (or Hazel, or Shortcuts) without rewriting anything.
2. **Make the script idempotent.** Triggers fire more often than you'd think, so "skip if done, clean up if failed" saves you a lot of hassle.
3. **Reach for Folder Actions when you're watching a user folder.** launchd is great for scheduled jobs, but for reacting to files in Downloads, Folder Actions fitted far better.
4. **Expect your security tools to notice.** If they do, read what you've built before you click anything.
5. **Log to somewhere obvious.** `/tmp/heic-to-jpeg.log` is the first place I'll look when it inevitably stops working one day.

To switch it off, right-click Downloads in Finder and go to Services → Folder Actions Setup.

The launchd approach was reasonable, it just wasn't right for this job, and dropping it early saved me an evening of digging through permissions. I built the whole thing with Claude Code in a single session. Small automations like this are some of my favourite things to build. They take a minute of friction out of my day, every day, and I'll never think about them again until a drive refuses a photo and I realise it hasn't happened in months.
