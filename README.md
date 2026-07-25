# AI Teleprompter

**Repository:** [https://github.com/Willmo103/AI-Teleprompter.git](https://github.com/Willmo103/AI-Teleprompter.git)

## What is this?

It is a teleprompter that actually listens to you.

Standard teleprompters are just dumb, scrolling text. If you go off on a tangent, you lose your place and the script leaves you behind. This project is a digital co-host that tracks what you are saying in the room against what you *planned* to say. If you cover a topic naturally, it checks it off. If you start rambling, it generates a quick, 2-3 sentence prompt on the screen to get you back on track.

## The Goals

* **The Ramble Catcher:** You do not have to perfectly read a script. You can just talk. If you get lost in the weeds for too long, the prompter flashes a lifeline to help you pivot--like, *"Wrap up the database talk and introduce the next topic."*
* **Zero Cloud Tax:** You should not have to pay a tech giant a monthly fee just to turn on a microphone. By leveraging Rust and running models locally, this handles the heavy lifting entirely on your own hardware. No API keys, no subscriptions.
* **Vibe-Based Strictness:** Some things (like exact quotes or ad reads) need to be read word-for-word. Other things just need to hit the right concepts. You can set a "creative liberty" slider for different parts of your script, and the engine knows the difference between a required exact match and a general idea.
* **Editing on Easy Mode:** Because the app is constantly comparing your audio to the script, it saves a detailed log of the timestamps. When you go to edit the podcast or video later, you do not have to scrub through an hour of raw tape--you already have an automated map of when you actually nailed the key points.

---

## Roadmap

This roadmap tracks the development from foundation to the first stable, end-to-end local application suite. Hardware and SaaS integration are deferred to `v0.1.0+`.

### v0.0.1 - Foundation & Core State Machine

* Initialize Cargo workspace and `core` crate (`#![no_std]` ready).
* Define the `Script` and `Block` structs (Verbatim vs. Concept points).
* Implement serialization/deserialization for JSON (Editor) and Postcard (Embedded).
* Build the Core State Machine: Logic to transition blocks from `pending` -> `active` -> `completed`.
* Write unit tests for strictness/creative liberty thresholds using dummy text inputs.

### v0.0.2 - The Sensory Layer (Audio & STT)

* Initialize `audio` crate using `cpal` to capture microphone input into rolling buffers.
* Initialize `local_ai` crate and integrate `whisper-apr` (or `whisper-rs`).
* Connect the audio buffer to the local STT model.
* Output a continuous, timestamped text stream to standard out.

### v0.0.3 - The Intelligence Loop (Local Evaluation)

* Integrate local LLM bindings (e.g., `llama.cpp` Rust bindings) into the `local_ai` crate.
* Build the Evaluation Loop: Feed STT chunks + Active Script Block to the local LLM.
* Implement string-distance matching for Verbatim blocks.
* Implement LLM prompt logic to generate pivot prompts.
* Emit state-change events (e.g., `BlockCompleted`, `OffScriptWarning`).

### v0.0.4 - The CLI Harness (End-to-End Test)

* Build `cli_harness` app to run the full pipeline in the terminal.
* Load a sample `.json` script from disk.
* Run the audio capture, STT, and LLM evaluation concurrently.
* Print generated pivot prompts and script progress visually in the console.

### v0.0.5 - The Editor Application (MVP)

* Initialize `editor` Tauri application.
* Build basic UI to add, reorder, and edit script blocks.
* Implement "Creative Liberty" sliders for concept blocks.
* Implement Save/Load functionality (exporting to JSON and Postcard binary).

### v0.0.6 - The Prompter Application (MVP)

* Initialize `prompter` Tauri application.
* Import the full `core`, `audio`, and `local_ai` crates as the backend engine.
* Build the Presenter UI: Large, readable scrolling blocks.
* Implement real-time UI updates based on core engine events.

### v0.0.7 - Polish & Pipeline Optimization

* Optimize the async loops to ensure STT and LLM inference do not block audio capture.
* Refine the UI/UX based on actual testing.
* Finalize the internal API boundaries of the `core` crate.
* Lock dependencies and tag `v0.0.7`.
