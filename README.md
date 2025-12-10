# Taryon Suite

[![License: CC BY-NC-ND](https://img.shields.io/badge/License-CC--BY--NC--ND-lightgrey.svg)](https://creativecommons.org/licenses/by-nc-nd/4.0/)

A next-generation, professional-grade HDL toolchain for Verilog (IEEE-1364). Taryon Suite provides a unified, high-performance environment for simulation, synthesis, and formal verification, engineered to meet the rigorous demands of modern ASIC and FPGA design flows.

---

## Overview

Taryon Suite is a comprehensive collection of three tightly integrated tools, each a powerhouse in its own right:

*   **Taryon Simulus:** A blazing-fast, standards-compliant Verilog simulator.
*   **Taryon Synthara:** An advanced RTL synthesis engine with superior optimization capabilities.
*   **Taryon Veritas:** A robust formal verification platform for exhaustive design validation.

Designed for engineers who demand precision, performance, and reliability, Taryon Suite bridges the gap between open-source accessibility and commercial-grade functionality.

---

## Key Features

*   **100% IEEE-1364 Compliant:** Full support for the Verilog-2005 standard, ensuring maximum portability and correctness.
*   **Unified Toolchain:** Seamless interoperability between simulation, synthesis, and formal verification.
*   **High-Performance Core:** Multi-threaded and optimized algorithms for handling today's massive designs.
*   **Professional Workflow:** Compatible with industry-standard practices and file formats (SDC, Liberty, EDIF, VCD, FST).
*   **Cross-Platform:** Built and tested on Linux, macOS, and Windows.
*   **Extensible Architecture:** Plugin support for custom libraries, verification IP, and tool integration.

---

## Toolset Deep Dive

### Taryon Simulus - High-Performance Verilog Simulator

Taryon Simulus is a state-of-the-art simulator that delivers the speed of compiled simulators with the flexibility of interpretive ones. It is designed for both rapid interactive debugging and massive regression testing.

**Core Capabilities:**

*   **Multiple Execution Modes:**
    *   **Interpretive Mode:** Fast compilation, ideal for interactive testbench development and debugging, similar to Icarus Verilog.
    *   **Optimized Compiled Mode:** Generates a high-performance C++ model for cycle-accurate simulation, offering speeds comparable to Verilator.
    *   **Hybrid Mode:** A unique blend allowing designers to compile performance-critical modules while keeping others in interpretive mode for maximum flexibility.
*   **Advanced Debugging:**
    *   Full-featured GUI and command-line interface.
    *   Waveform dump in VCD and FST formats.
    *   Interactive breakpoints, signal watching, and code execution tracing.
    *   Comprehensive code coverage analysis (line, toggle, branch, FSM).
*   **Language & API Support:**
    *   Complete support for all Verilog-1364 constructs, including generate blocks, UDPs, and specify blocks.
    *   Full PLI/VPI (Programming Language Interface) support for C/C++ co-simulation and custom tool development.
*   **Performance:**
    *   Multi-threaded kernel for parallel simulation on multi-core systems.
    *   Optimized memory management for handling designs with hundreds of millions of gates.

### Taryon Synthara - Advanced RTL Synthesis Engine

Taryon Synthara is a superior RTL synthesis tool that transforms high-level Verilog descriptions into optimized gate-level netlists. It leverages cutting-edge algorithms to achieve results that surpass open-source alternatives and rival industry leaders.

**Core Capabilities:**

*   **Comprehensive Optimization:**
    *   **Timing-Driven Synthesis:** Meets aggressive clock frequency targets with advanced timing analysis and optimization.
    *   **Resource & Area Optimization:** Intelligent resource sharing, logic minimization, and gate-sizing to reduce footprint.
    *   **Power Optimization:** Multi-Vth and clock-gating insertion for dynamic and static power reduction.
    *   **Advanced FSM Synthesis:** Automatic state encoding (one-hot, binary, Gray, Johnson) and optimization.
*   **Target Technology Support:**
    *   **FPGA:** Dedicated optimizations and library support for major FPGA families (e.g., Xilinx, Intel Microsemi).
    *   **ASIC:** Full support for standard cell libraries in Liberty (.lib) format.
*   **Constraint & Language Support:**
    *   Full support for Synopsys Design Constraints (SDC) for precise control over timing, area, and power.
    *   Reads and synthesizes all synthesizable Verilog-1364 constructs.
*   **Analysis & Reporting:**
    *   Detailed post-synthesis reports for area, timing (slack analysis), and power consumption.
    *   Generates netlists in Verilog, EDIF, and JSON for downstream flows.

### Taryon Veritas - Formal Verification Platform

Taryon Veritas provides exhaustive, mathematical proof of your design's correctness, uncovering bugs that are impossible to find with simulation alone. It ensures your design behaves as intended under all possible conditions.

**Core Capabilities:**

*   **Property-Based Checking:**
    *   A powerful model checking engine based on advanced SAT/SMT solvers.
    *   Supports assertions defined using a Verilog-compatible property language or embedded in comments.
    *   Exhaustively proves properties like safety, liveness, and absence of deadlocks.
*   **Equivalence Checking:**
    *   Mathematically proves that two versions of a design are functionally identical.
    *   Ideal for validating that a post-synthesis or post-layout netlist is equivalent to the original RTL source code.
*   **Debugging & Analysis:**
    *   Automatic counter-example (trace) generation for failing properties.
    *   Traces can be viewed in waveform viewers to easily understand the root cause of a bug.
    *   Cone-of-influence analysis to focus verification efforts on relevant parts of the design.
*   **Integration:**
    *   Reads designs, libraries, and constraints from the same sources as Simulus and Synthara, ensuring a smooth verification flow.

---

## Getting Started

### Prerequisites

*   A C++17 compliant compiler (e.g., GCC 9+, Clang 10+).
*   CMake 3.15 or newer.
*   Make or Ninja.
* (Optional) GTK+ 3.0 for the graphical waveform viewer.

### Installation

```bash
# Clone the repository
git clone https://github.com/your-org/taryon-suite.git
cd taryon-suite

# Create a build directory
mkdir build && cd build

# Configure and build
cmake .. -DCMAKE_BUILD_TYPE=Release
make -j$(nproc)

# (Optional) Install system-wide
sudo make install
```

---

## Quick Start Example

Let's simulate a simple "Hello, World!" module.

**1. Create the Verilog file (`hello_world.v`):**

```verilog
// hello_world.v
module hello_world;
  initial begin
    $display("Hello, Taryon Suite World!");
    $finish;
  end
endmodule
```

**2. Simulate with Taryon Simulus:**

```bash
# Compile and run the simulation
taryon-simulus -i hello_world.v

# Expected Output:
# Hello, Taryon Suite World!
# VCD info: dumpfile sim.vcd opened for output.
```

**3. Synthesize with Taryon Synthara (for an FPGA target):**

```bash
# Synthesize the design
taryon-synthara -i hello_world.v -p generic_fpga -o hello_world_synth.v

# The output file 'hello_world_synth.v' will contain the gate-level netlist.
```

**4. Formally Verify with Taryon Veritas:**

While this example has no properties to check, a typical command would look like this:

```bash
# Check properties defined in the design
taryon-veritas -i my_design.v -t my_top_module -c properties.sdc
```

---

## Documentation

For in-depth guides, API references, and tutorials, please visit our official documentation:

**[https://taryon-suite.readthedocs.io/](https://taryon-suite.readthedocs.io/)**

---

## Contributing

We welcome contributions from the community! Whether you're fixing a bug, adding a feature, or improving documentation, your help is appreciated.

Please see our [Contributing Guidelines](CONTRIBUTING.md) for more details.

---

## License

Taryon Suite is licensed under the MIT License. See the \[LICENSE\](LICENSE) file for more information.

---

## Acknowledgments

The Taryon Suite was inspired by the pioneers of both commercial and open-source EDA tools. We stand on the shoulders of giants like Cadence, Synopsys, Siemens EDA, as well as the dedicated communities behind Icarus Verilog, Verilator, and Yosys.
