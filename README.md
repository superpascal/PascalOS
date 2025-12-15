# PascalOS

PascalOS is an **educational operating system** inspired by **OS-9**, designed to run on a **65C816-based computer** with a **CPLD-based MMU**. It completes the SuperPascal ecosystem by providing a real, inspectable OS capable of running **applications and games written entirely in SuperPascal**.

This repository targets **students, educators, and systems enthusiasts** who want to understand operating system design **end-to-end** — from bootloader to multitasking OS — without black boxes.

---

## Why PascalOS exists

Most operating systems used in education today are either:

* too large and opaque (Linux, BSD), or
* too minimal to demonstrate real OS concepts

PascalOS occupies a deliberate middle ground:

* small enough to understand completely
* powerful enough to demonstrate real OS mechanisms
* tightly coupled to transparent hardware

It is designed to be:

* **used by high-school students (13–18)** as part of learning SuperPascal and computer architecture
* **studied and extended by university students** in OS and systems courses

---

## Key characteristics

* **CPU:** WDC 65C816 (24-bit, up to 16MB physical RAM)
* **MMU:** External CPLD-based DAT-style MMU (no FPGA)
* **Scheduling:** Cooperative (explicit yield)
* **Language:** SuperPascal (assembly only where unavoidable)
* **Memory model:**

  * 64KB logical address space per process
  * 8KB pages
  * Per-process page tables
* **Design goals:** determinism, clarity, inspectability

This is **not** a Unix clone and **not** POSIX compatible by design.

---

## Repository structure (planned)

```
PascalOS/
├── README.md
├── docs/
│   ├── PRD.md                 # Product Requirements Document
│   ├── architecture/          # OS and MMU design docs
│   ├── boot/                  # Boot sequence documentation
│   └── education/             # Curriculum & teaching notes
├── src/
│   ├── boot/                  # Minimal assembly bootloader
│   ├── kernel/                # Kernel (mostly SuperPascal)
│   ├── mmu/                   # MMU interface & abstractions
│   ├── scheduler/             # Cooperative scheduler
│   ├── ipc/                   # Message passing & IPC
│   ├── modules/               # Module loader & runtime
│   └── drivers/               # Device drivers
├── programs/                  # Example user programs
├── games/                     # Example games built with SuperPascal
└── tools/                     # Build tools, image builders, utilities
```

Structure may evolve as the system matures.

---

## Design philosophy

### OS-9 inspired, not OS-9 compatible

PascalOS borrows the *ideas* of OS-9:

* relocatable modules
* per-process address spaces
* strong modularity

It intentionally does **not** replicate OS-9 APIs or ABIs. This keeps the system modern, readable, and suitable for teaching.

### Cooperative scheduling by design

Preemption is deliberately avoided.

* Context switches happen only at explicit yield points
* Kernel invariants are easy to reason about
* Debugging is dramatically simpler

This choice aligns with both **educational clarity** and **SuperPascal’s language semantics**.

### Hardware + language working together

Instead of relying solely on hardware enforcement:

* the CPLD MMU provides coarse isolation and traps
* SuperPascal enforces discipline at compile time

This demonstrates how **language design and hardware design complement each other**.

---

## What PascalOS provides

* Bootloader → kernel bring-up
* Cooperative multitasking
* Per-process memory isolation
* Relocatable module system
* Message-passing IPC
* Modular device drivers
* A stable platform for SuperPascal applications and games

---

## What PascalOS intentionally omits

* Preemptive multitasking
* Virtual memory / swapping
* POSIX compatibility
* Hidden firmware or SoC abstractions

These are conscious trade-offs in favor of clarity and determinism.

---

## Educational progression

PascalOS is designed to be learned and built in phases:

1. **Single-task kernel** (no MMU)
2. **Cooperative multitasking**
3. **MMU-enabled process isolation**
4. **Module loader and drivers**
5. **Applications and games ecosystem**

Each phase is usable on real hardware.

---

## Target audience

* Secondary students learning systems programming
* University OS and architecture courses
* Educators building hands-on curricula
* Retro-computing and hardware enthusiasts

---

## Status

PascalOS is currently in the **design and early implementation phase**.

Key documents:

* `docs/PRD.md` — Formal Product Requirements Document
* Architecture and MMU design docs in `docs/architecture/`

---

## Contributing

This project values:

* clarity over cleverness
* documentation over shortcuts
* explainable design decisions

Contributions should:

* include rationale
* preserve inspectability
* respect the educational goals

A `CONTRIBUTING.md` will follow.

---

## License

License to be defined. The intent is to keep PascalOS open and usable for education.

---

## Final note

PascalOS is designed to answer a simple question:

> *What would an operating system look like if it were built first and foremost to be understood?*

If that question interests you, you’re in the right place.
