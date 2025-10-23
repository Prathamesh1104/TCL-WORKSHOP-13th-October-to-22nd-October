# VSD Workshop Tools Documentation

This document provides a **detailed overview of all tools** used in the VSD – TCL Programming for Synthesis & STA Automation workshop. The tools covered are:

- Yosys  
- OpenTimer  
- Netgen  
- Qrouter  
- Magic  

These tools form an **end-to-end open-source VLSI design flow**, from RTL synthesis to STA, routing, and layout verification.

---

## 1. **Yosys (Open-Source RTL Synthesis)**

**Purpose:**  
Yosys converts RTL (Verilog) designs into gate-level netlists compatible with standard cell libraries. It is widely used in FPGA prototyping and open-source ASIC flows.

**Key Functions:**
- RTL Parsing → builds abstract syntax tree from Verilog.
- Elaboration → resolves parameters and hierarchy.
- Synthesis → maps high-level logic to gates or LUTs.
- Optimization → logic minimization, constant propagation, dead code elimination.
- Technology Mapping → targets standard cell libraries using Liberty files.
- Netlist Output → produces Verilog, BLIF, or EDIF netlists.

**Input / Output:**
- **Inputs:** Verilog files (*.v), Liberty files (*.lib), optional SDC constraints.  
- **Outputs:** Synthesized netlist (*.synth.v), technology-mapped netlist, logs.

**Integration & Automation:**  
- TCL scripts can automate reading multiple Verilog files, applying synthesis constraints, generating reports, and error handling.

**TCL Automation Example:**
```tcl
set ys_file "$OutputDirectory/$DesignName.ys"
set fid [open $ys_file w]
puts $fid "read_liberty -lib ${LateLibraryPath}"
foreach f [glob -dir $NetlistDirectory *.v] {
    puts $fid "read_verilog $f"
}
puts $fid "synth -top $DesignName\nwrite_verilog $OutputDirectory/$DesignName.synth.v"
close $fid
exec yosys -s $ys_file
