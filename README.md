# ⬡ Pluton SDK & Language Specification

**Official Website:** [https://plutondev.online](https://plutondev.online)  
**Architecture & Cloud Documentation:** [https://plutondev.online/about](https://plutondev.online/about)  
**Contact:** `contact@plutondev.online` · `artur@plutondev.online`

---

## Overview

**Pluton** is an independent real-time systems programming language and neural runtime created by **Artur**. It is architected to eliminate multi-layer interpreter and FFI overhead by uniting native vector primitives, hardware-locked 60 FPS 2D/3D presentation, binary TCP packet serialization, and native foundation model (`Pluton-LLM`) execution in a single unified runtime.

> **Repository Scope:** The core Pluton compiler/runtime and distributed `Pluton-LLM` training engine are maintained in private repositories. This public repository provides the **Pluton Language Specification**, **Standard Library API reference**, and **verified `.pluto` / `.pluton` reference scripts**.

---

## Key Capabilities

* **First-Class 2D/3D Vector Math:** Tuple vectors `(x, y)` support native arithmetic without wrapper allocations.
* **Plutonium & Plutonium3D Engine:** Built-in 60 FPS hardware-timed 2D/3D graphics pipeline (`draw_cube`, `draw_pyramid`, `draw_grid_3d`, dynamic lighting, camera matrices, and 2D HUD overlays).
* **PlutoNET & Laser Protocol Stack:** Low-level TCP sockets and `ByteStream` binary packet framing for real-time multiplayer and telemetry workloads.
* **Hardware Introspection (`hardware`):** Direct GPU discovery and VRAM telemetry via `hardware.is_available()` and `hardware.gpu(0)`.
* **Pluton-LLM Native Architecture:** Autoregressive Transformer forward attention pass and training supervision hooks accelerated by **Google Cloud (Cloud GPUs / TPUs)** and **Frontier Google AI**.

---

## Repository Structure

```text
pluton-sdk/
├── README.md                        # Overview & CLI Toolchain Reference
├── docs/
│   └── SPECIFICATION.md             # Grammar, AST Nodes & Standard Library Reference
└── examples/
    ├── pluton_llm.pluto             # Native Transformer Attention & Training Loop
    ├── cyberpunk_3d.pluto           # 60 FPS 3D Scene on Plutonium3D Engine
    ├── snake_2d.pluto               # 60 FPS 2D Arcade Game on Plutonium
    ├── network_stream.pluto         # Binary TCP Handshake with PlutoNET & ByteStream
    └── vectors_gpu.pluton           # Native Vector Arithmetic & GPU VRAM Introspection
```

---

## Standard CLI Toolchain

| Command | Description |
| :--- | :--- |
| `pluton run <script.pluto>` | Launches the Pluton runtime, initializes hardware/graphics contexts, and executes the script. |
| `pluton check <script.pluto>` | Runs the front-end AST parser and static validator without executing side-effects. |
| `pluton train --model <cfg>` | Starts the native `Pluton-LLM` training supervisor with GPU telemetry and loss logging. |

---

## Concrete Syntax Reference

| Construct | Syntax Sample | Semantic Description |
| :--- | :--- | :--- |
| Immutable Binding | `val author = "Artur"` | Immutable identifier; cannot be mutated or reassigned. |
| Mutable State | `mut step = 0` | Mutable variable; eligible for in-place reassignments. |
| Console Output | `echo("Status:", step)` | Variadic output to stdout. |
| Native Vector Math | `(10, 20) + (5, -2)` | First-class tuple vector addition, subtraction, and scaling. |
| Conditional Guard | `when (cond) { … } otherwise { … }` | Structured alternative branch control. |
| Classical Branching | `if (a && b) { … } else { … }` | Boolean conditional logic with short-circuiting. |
| Runtime Loop | `loop (Plutonium.is_open()) { … }` | Guarded iteration block for 60 FPS rendering and training steps. |
| Range Iteration | `for i in range(0, n) { … }` | Deterministic integer sequence traversal. |
| List Operations | `xs.len · xs.prepend(val) · xs.drop_last()` | Dynamic list primitives. |
| Module Import | `use Plutonium; use hardware;` | Standard library namespace binding. |
| Hardware Access | `hardware.gpu(0).vram` | Direct introspection of available GPU accelerator memory. |

---

## License & Inquiries

Copyright © 2026 Pluton Development Team (created by Artur).  
For enterprise licensing, cloud partnerships, or technical inquiries, contact **artur@plutondev.online** or visit [https://plutondev.online](https://plutondev.online).
