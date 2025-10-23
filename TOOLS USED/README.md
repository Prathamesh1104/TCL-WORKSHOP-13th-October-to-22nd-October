# VSD Workshop Tools Documentation

This document provides a **detailed overview of all tools** used in the VSD – TCL Programming for Synthesis & STA Automation workshop. The tools covered are:

- Yosys  
- OpenTimer  
- Netgen  
- Qrouter  
- Magic  

These tools form an **end-to-end open-source VLSI design flow**, from RTL synthesis to STA, routing, and layout verification.

---

# 🧠 Yosys – Open Source RTL Synthesis Tool

Yosys is an **open-source RTL synthesis framework** that plays a key role in digital design automation (EDA). It converts high-level hardware description language (HDL) code — typically **Verilog** — into **gate-level netlists** suitable for FPGA or ASIC implementation. Yosys is the foundation of the open-source hardware synthesis flow and is frequently used with tools like **OpenTimer, Netgen, Qrouter,** and **Magic**.

---

## 📘 Overview

Yosys provides a complete set of commands for reading, elaborating, optimizing, and synthesizing HDL code. It supports **RTL-to-gate synthesis**, **technology mapping**, and **custom scripting through TCL**.  

It is particularly valuable for:
- FPGA design prototyping  
- ASIC design synthesis  
- Teaching and research in VLSI  
- Integration in open-source EDA flows (e.g., OpenLANE, Qflow)

---

## ⚙️ Key Features

### 🧩 1. RTL Parsing
- Reads Verilog HDL files and constructs an **Abstract Syntax Tree (AST)**.  
- Supports structural and behavioral Verilog.  
- Handles parameterized modules, generate blocks, and hierarchy resolution.

### 🔧 2. Elaboration
- Expands module instances and parameters.
- Builds a fully connected design hierarchy for analysis and synthesis.

### ⚙️ 3. Logic Synthesis
- Translates high-level logic into **generic logic gates (AND, OR, NOT, DFF, etc.)**.  
- Supports multiple synthesis passes such as:
  - `proc` – process extraction  
  - `opt` – logic optimization  
  - `fsm` – finite state machine extraction and optimization  
  - `memory` – RAM/ROM inference and mapping  

### 🧮 4. Optimization
- Constant propagation and dead-code elimination.  
- Logic simplification and redundant gate removal.  
- Timing-driven optimization via constraints.  

### 🏭 5. Technology Mapping
- Maps generic logic to **target standard cells** using **Liberty (`.lib`) files**.  
- Produces a gate-level netlist compatible with backend tools like OpenTimer or Magic.

### 🧾 6. Netlist Generation
- Exports the synthesized design to formats like:
  - **Verilog (.v)**
  - **BLIF**
  - **EDIF**
- Provides human-readable synthesis logs and statistics.

---

## 🧰 Input and Output Files

| Type | Description | Example Extension |
|------|--------------|------------------|
| **Input** | RTL Verilog Source | `.v` |
| **Input** | Liberty Cell Library | `.lib` |
| **Input** | Timing Constraints (optional) | `.sdc` |
| **Output** | Synthesized Netlist | `.synth.v` |
| **Output** | Synthesis Reports and Logs | `.log` |

---

## 🧠 Typical Yosys Workflow

The Yosys synthesis flow consists of several automated stages:

```text
Verilog Source (.v)
     ↓
[read_verilog]
     ↓
Elaboration (proc, flatten)
     ↓
Optimization (opt, fsm, memory)
     ↓
Technology Mapping (abc, techmap)
     ↓
Netlist Generation (write_verilog)

