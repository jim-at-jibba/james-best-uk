---
layout: ../../layouts/BlogLayout.astro
title: "The Raspberry Pi Thin Client That Solved My Hotel Room Problem"
description: "How a Pi 4, a USB SSD, and Tailscale became my favourite way to access my home lab from anywhere"
tags: ["homelab", "raspberry-pi", "linux", "self-hosted", "tailscale"]
time: 6
featured: true
timestamp: 2026-03-18T09:00:00+00:00
filename: raspberry-pi-thin-client
type: essay
---

I travel with work occasionally. When I do, I have my work laptop with me — but that's for work. When the day is done and I'm back in the hotel room, I want to work on personal projects. My home lab is sitting at home, humming away. What I needed was a clean, reliable way to get into it without dragging another machine across the country.

The answer turned out to be a Raspberry Pi 4 and about an afternoon of setup.

## The Problem With the Obvious Options

The obvious solution is to just SSH in from the work laptop. I didn't want to do that. Work machine is for work. I'm fairly deliberate about that boundary — mixing contexts is a reliable way to make both feel worse.

I briefly considered whether my Samsung S23 Ultra could cover it. Samsung DeX gives you a proper desktop-like environment over USB-C — it's genuinely impressive for what it is. But it's still Android, and what I actually wanted was a proper Linux machine I could sit down at properly. A real terminal, a real window manager, a real keyboard. The phone felt like a workaround rather than a solution.

What I already had: a Raspberry Pi 4 with 8GB RAM, a monitor, a Bluetooth keyboard and mouse, and an old SATA SSD in a USB enclosure. Everything I needed was already there.

## Pi OS Lite and i3

My first instinct was to grab the standard Raspberry Pi OS with desktop. It works, but it ships with LXDE — a full desktop environment that made sense when the Pi was an educational device but feels heavy for a machine whose only job is to be a window into something else.

Pi OS Lite is the better starting point. No desktop at all — just a clean base you build up from. Install only what you actually need. For a thin client, that list is short.

For the window manager I went with i3. If you haven't used it: i3 is a tiling window manager that's almost entirely keyboard-driven. Windows tile automatically, workspaces are managed with keyboard shortcuts, and the config file is straightforward text. I kept mine fairly vanilla — the main thing was making the keybindings feel close to Vim. `h/j/k/l` for navigation, muscle memory transfers.

The result is a setup that uses almost none of the Pi's resources on the window manager itself. All 8GB is available for actual work — SSH sessions, a browser for dashboards, remote desktop when I need a full GUI on the home lab.

## Booting From USB Instead of SD

One thing I changed early: I'm not booting from the SD card. The Pi 4 supports USB boot, and a cheap SATA SSD in a USB enclosure is meaningfully faster and far more reliable.

SD cards wear out. They're fine for experimenting but for a device you want to just work every time you sit down, repeated writes will eventually cause problems. The USB SSD eliminates that concern entirely. Boot times are faster too.

Setup is straightforward — enable USB boot in the Pi's bootloader config, flash your OS image to the SSD instead of the SD card, and you're done.

## Tailscale Is the Part That Makes It Actually Work

The networking piece is where this could have got complicated. Port forwarding, dynamic DNS, firewall rules — the kind of yak shaving that turns a fun project into a weekend of frustration.

Tailscale made it trivial.

Install Tailscale on the Pi, on the home lab machine, and on anything else you want on the same network. They all appear on a private tailnet. Encrypted peer-to-peer connections, no configuration beyond the initial install. From a hotel room on a completely different network, my Pi connects to my home lab as if they're sitting next to each other.

I can SSH directly into the home lab from the Pi's terminal. For anything that needs a full desktop — tools that aren't built for the terminal, admin interfaces — Remmina handles remote desktop over RDP or VNC. Both work cleanly over Tailscale.

## The Bluetooth Gotcha Worth Knowing

One friction point worth mentioning: Pi OS Lite doesn't always ship with everything you need for Bluetooth to work out of the box. On first boot I ran into RF-Kill soft-blocking the Bluetooth adapter — the system had disabled it and it needed manually unblocking.

The practical consequence: you need a wired keyboard for the initial setup. Bit of a chicken-and-egg situation if you've only got Bluetooth peripherals. Grab a cheap USB keyboard for the first boot, get everything configured, then switch to Bluetooth once it's working.

## What the Setup Actually Feels Like

Back in the hotel room, work laptop closed. Pi booted, Tailscale connected, SSH session open into the home lab within about thirty seconds. i3 workspaces for different contexts — one for the terminal, one for the browser, one for remote desktop if I need it.

It feels like sitting at a proper machine. Because in a meaningful sense, I am — just not the one physically in front of me.

The Pi handles display and input. The home lab does the actual work. It's the right separation. The Pi never breaks a sweat; everything computationally interesting happens on the server at home.

## The Stack

For reference, everything that makes this work:

- **Hardware:** Raspberry Pi 4 8GB, cheap SATA SSD in USB enclosure, Bluetooth keyboard and mouse, monitor
- **OS:** Raspberry Pi OS Lite
- **Window Manager:** i3 (Vim-style keybindings)
- **Terminal:** Kitty
- **Browser:** Firefox ESR
- **Remote Desktop:** Remmina
- **Networking:** Tailscale
- **App Launcher:** dmenu

Total cost beyond what I already had: close to nothing. The SSD enclosure was a few quid. The Pi and peripherals were already sitting there.

## Worth Doing

If you have a home lab and find yourself wanting to access it away from your desk — whether that's a hotel room, another room in the house, or anywhere else — a dedicated thin client is a cleaner solution than it might sound. You're not giving up a machine you'd otherwise use. You're repurposing hardware that was already idle into something that earns its keep every time you travel.

The Raspberry Pi 4 is more than capable. The setup takes an afternoon. And once Tailscale is running, the network complexity just disappears.

