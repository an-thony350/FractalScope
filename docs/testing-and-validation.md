# Testing and Validation

Testing was split across RTL simulation, PYNQ hardware bring-up, processing-system tests, and CPU baseline comparison.

## RTL Simulation

SystemVerilog testbenches were used for major hardware blocks before full integration.

| Block | Tested behaviour |
|---|---|
| Tile scheduler | Tile order, pixel indices, render scale behaviour, coordinate generation. |
| Iteration core | Escape iteration correctness, valid/ready behaviour, pixel-index preservation. |
| Iteration core array | Parallel dispatch and result return across multiple cores. |
| Colour palette | Iteration-to-RGB mapping, palette scaling, palette selection, index preservation. |
| Pixel write engine | Indexed framebuffer address calculation, AXI write responses, soft reset, status counters. |
| Performance counters | Render status and debug visibility. |

## Hardware Bring-Up

Jupyter notebooks on the PYNQ-Z1 were used before the final application was complete. This allowed direct interaction with the bitstream and HWH metadata:

- discover memory-mapped IP blocks,
- write AXI-Lite registers,
- allocate PYNQ framebuffers,
- start render passes,
- poll writer counters,
- inspect write errors,
- compare hardware output against software references.

## Processing-System Tests

The PS was also used as an integration diagnostic layer. It helped isolate:

- coordinate conversion errors,
- RGB byte-order issues,
- palette scaling problems,
- framebuffer/cache coherency bugs,
- VDMA stride/size mistakes,
- controller packet parsing problems,
- menu and scene-transition regressions.

## CPU Baseline

A C++ CPU renderer was integrated to provide a comparison point. The final project reported up to 53x throughput speedup over the multi-threaded CPU baseline at a maximum iteration count of 2048.

## Validation Philosophy

The project was debugged from small units outward:

1. Test hardware blocks in simulation.
2. Bring up registers and framebuffers in notebooks.
3. Validate visual output on HDMI.
4. Integrate the full PS application.
5. Compare the PL renderer with software/CPU output.

