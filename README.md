# Advanced-Physical-Design-using-OpenLANE-Sky130-Overview

![work2](https://user-images.githubusercontent.com/20563301/123817565-e71e5f00-d915-11eb-8fa1-ba4fb781980c.PNG)

This repository contains the usage of tools like iverilog, gtkwave and yosys for open-source RTL Design. The content is documentation of tasks carried out during VSD "RTL Design Using Verilog With SKY130 Technology".

SKY130 is the hardware industry's first open-source process design kit (PDK) released by SkyWater Technology Foundry in collaboration with Google giving all hardware design experts and aficionados, a worldwide access to their IP functions and open source ASICs. More details [here.](https://github.com/google/skywater-pdk).

This particular workshop covers the various aspects of design in Verilog HDL both theoretically and practically with labs using open-source softwares through their VSD-IAT portal. Beginning with an introduction to digital design using Verilog HDL and various libraby, the instructors cover digital design steps that include design, functional simulation, test bench based validation of the design functionality and logic Synthesis with optimization. Further, we learn about efficient verilog coding styles that result in a predictable logic in Silicon.

## Table of Contents

- [Day 1 Introduction to Verilog RTL Design and Synthesis](#Day-1-Introduction-to-Verilog-RTL-Design-and-Synthesis)
  * [Setup the lab instance with libraries and verilog files](#Setup-the-lab-instance-with-libraries-and-verilog-files)
    - [OpenLANE Initialization](#openlane-initialization)
  * [Labs using iverilog and gtkwave](#Labs-using-iverilog-and-gtkwave)
  * [Introduction to Yosys and Logic synthesis](#Introduction-to-Yosys-and-Logic-synthesis)
  * [Labs using Yosys and Sky130 for 2x1 Multiplex](#Labs-using-Yosys-and-Sky130-for-2-x-1-Multiplex)
- [Day 2 Timing libs Hierarical vs Flat Synthesis and efficient Flop Coding Styles](#Day-2-Timing-libs-Hierarical-vs-Flat-Synthesis-and-efficient-Flop-Coding-Styles)
  * [Introduction to timing .libs](#Introduction-to-timing-.libs)
  * [Hierarchical vs Flat Synthesis](#Hierarchical-vs-Flat-Synthesis)
  * [Efficient Flip-flop coding styles and Optimizations](#Efficient-Flip-flop-coding-styles-and-Optimizations) 
- [Day 3 Combinational and sequential optimization](#Day-3-Combinational-and-sequential-optimization)  
  * [Introduction to optimizations](#Introduction-to-optimizations)
  * [Combinational logic optimizations (Labs)](#Combinational-logic-optimizations-(Labs))
  * [Sequential logic optimizations (Labs)](#Sequential-logic-optimizations-(Labs))
  * [Sequential optimzations for unused outputs](#Sequential-optimzations-for-unused-outputs)
- [Day 4 GLS blocking vs non blocking and Synthesis Simulation mismatch](#Day-4-GLS-,blocking-vs-non-blocking-and-Synthesis-Simulation-mismatch)
  * [GLS, Synthesis-Simulation mismatch and Blocking/Non-blocking statements](#GLS,-Synthesis-Simulation-mismatch-and-Blocking/Non-blocking-statements)
  * [Labs on GLS and Synthesis-Simulation Mismatch](#Labs-on-GLS-and-Synthesis-Simulation-Mismatch)
  * [Labs on synth-sim mismatch for blocking statement](#Labs-on-synth-sim-mismatch-for-blocking-statement)
- [Day 5 If, case, for loop and for generate](#Day-5-If-case-for-loop-and-for-generate)
   * [If Case constructs](#If-Case-constructs)
   * [Labs on "Incomplete If Case"](#Labs-on-"Incomplete-If-Case")
   * [Labs on "Incomplete overlapping Case"](#Labs-on-"Incomplete-overlapping-Case")
   * [for loop and for generate](#for-loop-and-for-generate)
   * [Labs on "for loop" and "for generate"](#Labs-on-"for-loop"-and"-for-generate")
- [Acknowledgements](#Acknowledgements)
- [References](#References)


# About Google SkyWater PDK
  Google and SkyWater Technology Foundry in collaboration have released a completely open-source Process Design Kit(PDK) in May, 2020. The current release target to a SKY130 (i.e. 130 nm) process node is available as [SkyWater Open Source PDK](https://github.com/google/skywater-pdk). The PDK provides Physical VLSI Designer with a wide range of flexibility in design choices. All the designs and simulations listed in this repository are carried out using the same SkyWater Open Source PDK.

# List of All Open-Source Tools Used
  | Name of Tool | Application / Usage |
  | --- | --- |
  | [Yosys](https://github.com/YosysHQ/yosys) | Synthesis of RTL Design |
  | ABC | Mapping of Netlist |
  | [OpenSTA](https://github.com/The-OpenROAD-Project/OpenSTA) | Static Timing Analysis |
  | [OpenROAD](https://github.com/The-OpenROAD-Project/OpenROAD) | Floorplanning, Placement, CTS, Optimization, Routing |
  | [TritonRoute](https://github.com/The-OpenROAD-Project/TritonRoute) | Detailed Routing |
  | [Magic VLSI](http://opencircuitdesign.com/magic/) | Layout Tool |
  | [NGSPICE](https://github.com/imr/ngspice) | SPICE Extraction and Simulation |
  | SPEF_EXTRACTOR | Generation of SPEF file from DEF file |
  
# Setting Up Environment
  The above list of tools shows that, many different tools are required for various tasks in Physical VLSI Design. Each tool in itself have number of system requirements and require various supporting tools to be installed. Installing each tool one-by-one seems in-efficient. This is made easy by some custom scripts that setup the required tools and environment for them in just a few easy steps. To install all the required tools, one can refer to the below mentioned repositories:
  - [VSDFlow](https://github.com/kunalg123/vsdflow) - Installs Yosys, Magic, OpenTimer, OpenSTA and some other supporting tools
  - [OpenLANE Build Scripts](https://github.com/nickson-jose/openlane_build_script) - Install all required OpenROAD and some supporting tools
  
  # Day 1 Introduction to Verilog RTL Design and Synthesis
  
   ## 	OpenLANE Initialization
  
