# Project Contributions

FractalScope was a team project. This public dossier focuses on the parts I worked on most directly: FPGA hardware/extensions and the processing system.

## My Main Contribution Areas

| Area | Contribution |
|---|---|
| FPGA hardware | Worked on the render pipeline, fixed-point datapath decisions, iteration-core scaling, tile scheduling, and timing/resource tradeoffs. |
| Hardware extensions | Implemented or helped integrate progressive rendering, dirty rectangles, periodicity checking, Mariani-Silver acceleration, and runtime palette selection. |
| Pixel write path | Helped move the design toward indexed DDR writes instead of a reorder-buffer constrained stream path. |
| Processing system | Built and integrated the Python-side scene/application layer, hardware backend, register programming, framebuffer/HUD handling, and free-roam modes. |
| PS/PL integration | Connected mathematical view state to Q4.22 hardware registers, render-control sequencing, writer polling, and HDMI display commits. |
| Debugging/testing | Used RTL simulation, PYNQ notebooks, status counters, visual checks, and CPU reference paths to isolate integration problems. |

## Other Team Areas

Other team members contributed to areas including controller hardware/firmware, CPU baseline work, documentation, mechanical enclosure work, and additional project integration. This repository does not claim sole authorship of the full system.

## Skills Demonstrated

- SystemVerilog hardware design.
- Fixed-point arithmetic and DSP budgeting.
- AXI-style register and memory-write integration.
- FPGA timing/resource tradeoff analysis.
- Python hardware control on PYNQ.
- Framebuffer and HDMI display integration.
- Hardware/software co-design.
- Testbench and hardware bring-up workflows.

