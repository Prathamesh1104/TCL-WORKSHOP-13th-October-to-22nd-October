
## Example:

```tcl
# TCL Automation for Yosys Synthesis
set DesignName "alu"
set OutputDirectory "./output"
set NetlistDirectory "./netlist"
set LateLibraryPath "./lib/sky130.lib"

# Create Yosys script dynamically
set ys_file "$OutputDirectory/$DesignName.ys"
set fid [open $ys_file w]

# Load the Liberty library
puts $fid "read_liberty -lib ${LateLibraryPath}"

# Load all Verilog design files
foreach f [glob -dir $NetlistDirectory *.v] {
    puts $fid "read_verilog $f"
}

# Run synthesis
puts $fid "synth -top $DesignName"
puts $fid "write_verilog $OutputDirectory/$DesignName.synth.v"

close $fid

# Execute Yosys
exec yosys -s $ys_file
