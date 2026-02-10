# RV32E-Mini-CPU

This project implements a tiny RV32E-based RISC-V CPU entirely in Logisim. It’s mainly built as a learning project, so the whole design stays intentionally small and readable. The core only supports a minimal set of instructions, which makes it easier to follow the datapath, control logic, and memory behavior without getting lost in details.

## Supported Instructions

The CPU currently supports the following 8 instructions:

- jalr
- add
- addi
- sw
- lbu
- sb
- lw
- lui

This is not a complete RISC-V implementation. The goal is to keep a tiny but usable subset that is enough to run simple test programs and demos. Since there are no conditional branches (like `BEQ`), control flow is handled strictly via jumps. It’s a raw experience.

## Features

- **RV32E-based core in Logisim**
   The processor follows the RV32E register convention and is fully built with Logisim components. Everything is visible in the schematic, so it’s easy to inspect or modify.

- **24-bit address ROM and RAM**
   Both ROM and RAM use 24-bit address width. This gives enough space for experiments without making the circuit too large or slow to simulate.

- **RGB image support (256×256)**
   The system includes a simple RGB display device with a fixed resolution of 256×256. You can load image data into memory and let the CPU write pixel values to the display.

  ## RGB Display Format

  The RGB display is configured as follows:

  - **Resolution:** 256 × 256
  - **Color model:** 888 RGB (24-bit color, 8 bits per channel)
  - **Pixel format:** 1 pixel = 24 bits (R, G, B)
  - **Cursor:** No Cursor
  - **Reset behavior:** Asynchronous

  Each pixel is written as a 24-bit RGB value. When the CPU writes to the memory-mapped display region (`0x20000000` ~ `0x20040000`), the data will be interpreted as pixel data for the RGB screen. This allows the program to directly draw images or patterns by writing RGB values into the frame buffer area.

- **Single-cycle, minimal design**
   The CPU is single-cycle and focuses on clarity rather than performance. No pipeline, no cache, just the basics for learning and experimentation.

## How to Use

1. Open the `main.circ` file with Logisim or Logisim Evolution.
2. Load your program into ROM (right click ROM → Load Image).
3. If you want to test graphics output, prepare image or pixel data and write to the memory-mapped RGB address ranges in your program.
4. Run the clock manually or automatically and observe registers, memory, and the RGB display.

This project is mainly for learning, experimenting, and having fun with a very small RISC-V-like CPU. It’s not meant to be complete or fast, but it’s a nice playground if you’re curious about how CPUs and memory-mapped devices work at the circuit level.

## Notes & Contributions

This is a personal project and still pretty rough in some places. If you spot bugs, design issues, or have ideas (like adding more instructions or peripherals), feel free to open an issue or PR.
 Suggestions and improvements are always welcome.