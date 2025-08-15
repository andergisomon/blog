+++
title = 'My projects'
date = 2024-07-30T13:44:00+08:00
lastmod = 2025-08-14T10:54:04+08:00
draft = false
+++

This post details some of my current ongoing projects.

## Major projects

### <span style="color: green;">[Active]</span> Pimato font project - Taarau
Pimato is a constructed writing system I've been working on since the last 7 years. I've been planning to make a font 3 years ago but only got around doing it 2 months ago.

[Taarau](https://github.com/andergisomon/taarau) is the name of the first font for Pimato, it comes from the word *arau* which means to rush. I've been intending to rush the development of the font as I believed as long as it looks close enough to my vision, it doesn't matter. But as the weeks ago by I can't help but scrutinize its tiny details. Professional fonts typically take 2 years to develop, I'm hoping that this font won't be a professional one because I need to start making materials with it.

> **Update** (17 Oct 2024): This project is crawling, but alive.

> **Update 2** (27 April 2025): This project will be done timely, but some orthographical compromises were made.

> **Update 3** (11 August 2025): The [repo](https://github.com/andergisomon/taarau) has been up since May 11, 2025.


### <span style="color: red;">[Abandoned]</span> Kayan TTS/ASR transfer learning from related Apo-Duat language model
I've been wanting to finetune a pretrained Apo-Duat language model from Meta's MMS suite of [ASR/TTS models](https://github.com/facebookresearch/fairseq/tree/main/examples/mms "Title") for a year now but have never found the time to do it. This semester break I intend on actually working on it. More specifically, I want to see if it's possible to reduce the compute requirements by repurposing the Penan (`pez`) or Lundayeh (`lnd`) weights.

> **Update** (17 Oct 2024): This project is abandoned. I can't find the time to create the dataset, and it would require community engagement to turn this into an actual project instead of a side passion project for a hobby.

## Planned Projects
This section lists projects that have some level of planning, but not enough material work has been put into realizing them yet.

### Soft PLC Platform - Taob
This is meant to be a rewrite and spiritual continuation of [Gipop](https://github.com/andergisomon/gipop), a hastily made proof-of-concept soft PLC following the example of the control platform developed by [QiTech GmbH](https://github.com/qitechgmbh/control), generously made open source by Philipp Schmechel.

CODESYS, OpenPLC, and Beremiz are the only available soft PLC platforms out there. CODESYS has gained significant foothold in industry. OpenPLC is still a huge WIP, and Beremiz is unmaintained.

OpenPLC currently depends on an unmaintained IEC 61131-3 transpiler backend, MATIEC. There is a new promising IEC 61131-3 Structured Text backend, [RuSTy](https://github.com/PLC-lang/rusty), currently being worked on by a duo, [Ghaith Hachem](https://github.com/ghaith) and [Mathias Rieder](https://github.com/riederm) from Bachmann Electronic.

I plan to write parts of the runtime in Zig and Rust for the following reasons:

1. RuSTy exposes a (planned) Rust API, so using Rust is a no-brainer.
2. Rust and Zig are cool languages.

There are other practical reasons for adding Zig into the mix. I like the verbosity and explicitness that the language enforces. For other parts I can see how Rust's abstractions and rich type system can be convenient. It's ok to like more than one thing, everyone.

As for why even bother working on this, I have a few reasons:

1. I hate how PLCs are locked down; I generally dislike being constrained to use ugly and closed software.
2. I'm not running/working for an integrator.

**Actionable goals:**
(In decreasing order of importance)
1. Online code changes (Hot reload)
2. Online variable read/writes (Debugger + Variable Table UI)
3. Protocol-agnostic data layer
4. Structured Text (ST) support

As to why I put ST support last, well it's because RuSTy is still too early in its development. They're still working on implementing core specifications from the IEC standard (and CODESYS extensions). Plus, I personally have no problems with programming a PLC in C, Rust or even Zig only given that goals **1.** and **2.** are met.

The first two goals are crucial features in industrial automation.

**Notes to self:**

Maybe fork [gdbgui](https://www.gdbgui.com/)? It claims Rust support. `gdbui` uses [pygdbmi](https://cs01.github.io/pygdbmi/) to interface with `gdb`. Maybe just use that and roll our web UI from scratch? [NiceGUI](https://nicegui.io/) would be nice for that. Thanks to [jeffective](https://github.com/jeffective) for bringing it to my attention.

### Zig Firmware Rewrite for the Cytron IRIV IO
The default firmware from Cytron relies on MicroPython. Will be interesting to see if there's gonna be any performance improvements with rewriting the whole stack in Zig + C.

I also want to see how far I can get with hacking OPC UA PubSub to do firm real-time, with careful programming of the PLC and the RP2350A inside the IRIV IO, treating it like EtherCAT with its own reserved NIC on the PLC.

### Mixing Zig and Rust in Embedded
This came to mind after discovering the [embedded-graphics](https://github.com/embedded-graphics/embedded-graphics) crate, which to my surprise was started and maintained by the same guy behind [EtherCrab](https://github.com/ethercrab-rs/ethercrab), James Waples.

I've got some ideas on how to make it work: The binary that will be flashed will be built with Zig (using [MicroZig](https://github.com/ZigEmbeddedGroup/microzig)), so the `app_main()` loop would be within the Zig program. Presumably I won't bother with the Espressif Second Stage Bootloader and Partition Table, given that by default MicroZig will just install out the direct boot image which can be flashed directly with `esptool.py`.

I'll make a dummy Rust driver for the SH1106 that wraps the MicroZig SH1106 driver. This dummy driver will implement the [`DrawTarget`](https://docs.rs/embedded-graphics-core/latest/embedded_graphics_core/draw_target/trait.DrawTarget.html) trait. We'll instantiate a [`Framebuffer`](https://docs.rs/embedded-graphics/latest/embedded_graphics/framebuffer/struct.Framebuffer.html) that the rest of the `embedded-graphics` API will talk to. The Rust program will then export a function that will be called from Zig's `app_main()`.

The dummy driver should probably just be a small module that wraps C data structures (for interop with Zig). After all, `DrawTarget` is only a few methods. The exported Rust function will just mutate a `Framebuffer` that the actual Zig driver will send to the display over I2C.

**Hardware needed:**
* esp32c3 devboard
* SH1106 OLED


*Last updated 15 August 2025*