# Advanced-Physical-Design-using-OpenLANE-Sky130-Overview

![work2](https://user-images.githubusercontent.com/20563301/123817565-e71e5f00-d915-11eb-8fa1-ba4fb781980c.PNG)

This repository contains the usage of tools like iverilog, gtkwave and yosys for open-source RTL Design. The content is documentation of tasks carried out during VSD "RTL Design Using Verilog With SKY130 Technology".

SKY130 is the hardware industry's first open-source process design kit (PDK) released by SkyWater Technology Foundry in collaboration with Google giving all hardware design experts and aficionados, a worldwide access to their IP functions and open source ASICs. More details [here.](https://github.com/google/skywater-pdk).

This particular workshop covers the various aspects of design in Verilog HDL both theoretically and practically with labs using open-source softwares through their VSD-IAT portal. Beginning with an introduction to digital design using Verilog HDL and various libraby, the instructors cover digital design steps that include design, functional simulation, test bench based validation of the design functionality and logic Synthesis with optimization. Further, we learn about efficient verilog coding styles that result in a predictable logic in Silicon.

# Table of Contents
  - [List of All Open-Source Tools Used](#list-of-all-open-source-tools-used)
  - [Setting Up Environment](#setting-up-environment)
  - [Day 1 - Inception of open-source EDA, OpenLANE and Sky130 PDK](#day-1-inception-of-open-source-eda-openlane-and-sky130-pdk)
    - [How to talk to computers](#How-to-talk-to-computers)
       - [Basic IC Design Terminologies](#basic-IC-design-terminologies)
       - [Introduction To RISC-V](#introduction-to-risc-v)
       - [From Software Applications to Hardware](#from-software-applications-to-hardware)
     - [Introduction to all components of open-source digital basic design](#introduction-to-all-components-of-open-source-digital-basic-design)
        - [Open Source Digital ASIC Design Diagram](#open-source-digital-ASIC-design-diagram)
        - [Introduction To RTL to GDSII Flow](#introduction-to-RTL-to-GDSII-flow)
        - [Introduction to Open LANE detailed ASIC design flow](#introduction-to-open-LANE-detailed-ASIC-design-flow)
     - [Open-Source EDA Tools](#Open-Source-EDA-Tools)
         - [Open LANE Initialization](#open-LANE-initialization)
         - [Design Preparation](#design-preparation)
         - [Design Synthesis and Results](#design-synthesis-and-results)
   - [Day 2 - Good floorplan vs bad floorplan and introduction to library cells](#day-2---good-floorplan-vs-bad-floorplan-and-introduction-to-library-cells)
     - [Chip Floorplanning](#chip-floorplanning)
        - [Utilization Factor and Aspect Ratio](#utilization-factor-and-aspect-ratio)
        - [Pre Placed Cells](#Pre-Placed-Cells)
        - [De-Coupling Capacitors](#De-Coupling-Capacitors)
        - [Power Planning](#power-planning)
        - [Pin Placement](#pin-placement)
        - [Floorplan using OpenLANE](#floorplan-using-openlane)
        - [vii.	Floorplanning using Magic](#Floorplanning-using-Magic)
      - [Placement](#placement)
        - [Placement and Optimization](#placement-and-optimization)
        - [Placement using OpenLANE](#placement-using-openlane)
     - [Cell Design and Characterization Flows](#cell-design-and-characterization-flows)
        - [Cell Design Flow](#cell-design-flow)
        - [Characterization Flow](#characterization-flow)
  - [Day 3 - Design library cell using Magic Layout and ngspice characterization](#day-3-design-library-cell-using-magic-layout-and-ngspice-characterization)
    - [CMOS Inverter Design using Magic](#cmos-inverter-design-using-magic)
    - [Extract SPICE Netlist from Standard Cell Layout](#extract-spice-netlist-from-standard-cell-layout)
    - [Transient Analysis using NGSPICE](#transient-analysis-using-ngspice)
  - [Day 4 - Pre-layout timing analysis and importance of good clock tree](#day-4---pre-layout-timing-analysis-and-importance-of-good-clock-tree)
    - [Magic Layout to Standard Cell LEF](#magic-layout-to-standard-cell-lef)
    - [Timing Analysis using OpenSTA](#timing-analysis-using-opensta)
    - [Clock Tree Synthesis using TritonCTS](#clock-tree-synthesis-using-tritoncts)
  - [Day 5 - Final steps for RTL2GDS](#day-5---final-steps-for-rtl2gds)
    - [Generation of Power Distribution Network](#generation-of-power-distribution-network)
    - [Routing using TritonRoute](#routing-using-tritonroute)
    - [SPEF File Generation](#spef-file-generation)
  - [References](#References)
  - [Acknowledgement](#Acknowledgement)



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
  
