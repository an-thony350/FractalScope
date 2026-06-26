# Processing System

The processing system is the control and application layer of FractalScope. It keeps the FPGA focused on high-throughput fractal computation while the PS handles interaction, UI, scenes, register programming, framebuffer management, and benchmarking.

## PS Responsibilities

| Area | Responsibility |
|---|---|
| Input abstraction | Convert controller packets and keyboard fallback into shared events. |
| Scene management | Route events through guided scenes, menus, free-roam modes, and CPU comparison. |
| View state | Track centre, width, iteration depth, fractal mode, Julia parameter, palette, and HUD state. |
| Register programming | Convert state into AXI-Lite writes for scheduler, writer, and palette controls. |
| Framebuffer management | Allocate PYNQ buffers, manage cache coherency, commit rendered frames to display. |
| HUD composition | Draw overlays, labels, menus, formulae, and status panels in software. |
| CPU comparison | Run a CPU renderer and compare throughput with the PL path. |

## Event Model

Both controller and keyboard inputs are mapped to common events:

| Event group | Examples |
|---|---|
| Navigation | Next, back, menu, quit |
| View control | Pan, zoom, reset |
| Rendering control | Iteration depth, palette |
| Scene-specific control | Action, function |

This made the application testable without the physical controller and prevented separate controller/keyboard paths from leaking into every scene.

## Register Interface

The PS wrote hardware-friendly values to the PL:

- Q4.22 x/y pixel steps,
- Q4.22 top-left coordinate,
- Julia parameter,
- fractal mode,
- maximum iteration count,
- render scale,
- framebuffer base address,
- expected pixel count,
- palette selection and scaling.

Floating-point view state was kept in Python for readability, then converted to fixed-point immediately before programming the FPGA.

## Framebuffer Path

The system used 32-bit packed framebuffers at 1280 x 720. The FPGA wrote completed pixels into DDR, the PS handled overlay composition, and the VDMA scanned the display framebuffer to HDMI.

The final PS flow used a fixed display-buffer commit path to avoid tearing and left-edge wrap-around issues that could appear when switching VDMA frame-store addresses during active display.

## User-Facing Modes

- Guided educational walkthrough.
- Mandelbrot and Julia PL demonstrations.
- Menu-based free-roam modes.
- CPU-vs-hardware comparison.
- Keyboard fallback for development and robustness.

## Why This Split Worked

The UI, controller mappings, menu flow, educational scenes, and overlays changed often during development. Keeping those in Python made iteration fast. The hardware interface stayed compact: the FPGA received numeric view parameters and render commands rather than needing to understand text rendering, scene transitions, or menu logic.

