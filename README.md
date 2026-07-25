---
rev: 0.0.1
author: "William E. Morris"
date: 2026-07-25 03:10:13 AM
version: 0.0.1
---

# AI Teleprompter (Name TBD)

## What is this?

It’s a teleprompter that actually listens to you.

Standard teleprompters are just dumb, scrolling text. If you go off on a tangent, you lose your place and the script leaves you behind. This project is a digital co-host that tracks what you are saying in the room against what you *planned* to say. If you cover a topic naturally, it checks it off. If you start rambling, it generates a quick, 2-3 sentence prompt on the screen to get you back on track.

## The Goals

* **The Ramble Catcher:** You don't have to perfectly read a script. You can just talk. If you get lost in the weeds for too long, the prompter flashes a lifeline to help you pivot—like, *"Wrap up the database talk and introduce the next topic."*
* **Zero Cloud Tax:** You shouldn't have to pay a tech giant a monthly fee just to turn on a microphone. By leveraging Rust and running models locally, this handles the heavy lifting entirely on your own hardware. No API keys, no subscriptions.
* **Vibe-Based Strictness:** Some things (like exact quotes or ad reads) need to be read word-for-word. Other things just need to hit the right concepts. You can set a "creative liberty" slider for different parts of your script, and the engine knows the difference between a required exact match and a general idea.
* **Editing on Easy Mode:** Because the app is constantly comparing your audio to the script, it saves a detailed log of the timestamps. When you go to edit the podcast or video later, you don't have to scrub through an hour of raw tape—you already have an automated map of when you actually nailed the key points.
