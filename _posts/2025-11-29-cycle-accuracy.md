---
layout: post
title: "Cycle Accuracy Is a Budget, Not a Property"
date: 2025-11-29
description: "Why per-cycle 6502 emulation costs more than per-instruction, and when the accuracy actually buys you something."
tags: [c, emulation]
---

Emulator authors talk about cycle accuracy as though it were a boolean. It is
closer to a spending decision, and the bill arrives in the inner loop.

## Two shapes of interpreter

The per-instruction interpreter fetches an opcode, does the whole thing, and
adds the documented cycle count to a counter:

```c
while (cpu->cycles < budget) {
    uint8_t op = read8(cpu, cpu->pc++);
    dispatch[op](cpu);
    cpu->cycles += cycle_table[op];
}
```

The per-cycle interpreter advances one tick at a time and keeps the
instruction's progress in the machine state:

```c
while (cpu->cycles < budget) {
    step_one_cycle(cpu);
    cpu->cycles++;
}
```

The second form is several times slower and much harder to write, because
every instruction becomes a small state machine rather than a function.

## What the extra cycles buy

Nothing, for most software. The 6502 programs that care are the ones that
observe the bus between an instruction's cycles — typically raster effects
that reprogram a video register mid-scanline. If the emulated CPU applies its
write at instruction boundaries, the effect lands on the wrong scanline and
the display tears.

The read-modify-write instructions are the clearest case. `INC $D020` does not
perform one write. It writes the old value back before writing the
incremented one, and hardware that reacts to writes sees both. Emulate it as
a single store and a small but real class of programs breaks.

## Picking a point on the curve

The useful question is not whether to be cycle accurate but which bus events
need correct ordering. Most projects can run a per-instruction core and
special-case the read-modify-write group, which recovers most of the
compatibility for almost none of the cost.

Start there. Move to a per-cycle core when you have a specific program that
fails and you have confirmed the failure is timing rather than a bug in your
addressing modes, which it usually is.
