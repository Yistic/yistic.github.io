---
layout: home
---

I am Jane Doe, a systems programmer. I write C for a living and C for fun,
which turns out to be the same activity performed under different lighting.
This site is where I keep the long-form version of whatever I am currently
taking apart.

The recurring subjects are Linux systems programming, graphics written
without a graphics library, CPU emulation, and retrocomputing. Every post is
written after the thing was actually built, which means the interesting part
is usually the bug, not the design.

## Elsewhere

- [GitHub](https://github.com/janedoe)
- [LinkedIn](https://rs.linkedin.com/in/beli02)

## Projects

**[framebuffer-demo](https://github.com/janedoe/framebuffer-demo)** — Drawing
directly to /dev/fb0 with no X11, no Wayland, and no SDL. Roughly four hundred
lines, most of them about pixel formats.

**[tiny6502](https://github.com/janedoe/tiny6502)** — A cycle-accurate MOS 6502
emulator with a stepping debugger, written to find out what "cycle-accurate"
actually costs.

**[peekaboo](https://github.com/janedoe/peekaboo)** — A minimal ptrace(2)
debugger. Sets breakpoints, reads registers, and demonstrates why the
`PTRACE_ATTACH` race is worse than the man page implies.
