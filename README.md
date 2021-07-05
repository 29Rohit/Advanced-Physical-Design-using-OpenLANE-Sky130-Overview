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
        - [Floorplanning using Magic](#Floorplanning-using-Magic)
      - [Placement](#placement)
        - [Placement and Optimization](#placement-and-optimization)
        - [Placement using OpenLANE](#placement-using-openlane)
     - [Cell Design and Characterization Flows](#cell-design-and-characterization-flows)
        - [Cell Design Flow](#cell-design-flow)
        - [Characterization Flow](#characterization-flow)
  - [Day 3 - Design library cell using Magic Layout and ngspice characterization](#day-3-design-library-cell-using-magic-layout-and-ngspice-characterization)
    - [CMOS inverter using ngspice simulations](#CMOS-inverter-using-ngspice-simulations)
       - [I/O Placer ](#I/O-Placer)
       - [Spice Desk creation and simulation for CMOS invertor](#Spice-Desk-creation-and-simulation-for-CMOS-invertor)
       - [CMOS invertor using Design using Magic](#CMOS-invertor-using-Design-using-Magic)
    - [CMOS fabrication process](#CMOS-fabrication-process)
    - [Sky130 Tech File Labs](#Sky130-Tech-File-Labs)
       - [Extract SPICE Netlist from Standard Cell Layout](#Extract-SPICE-Netlist-from-Standard-Cell-Layout)
       - [Transient Analysis using NGSPICE](#Transient-Analysis-using-NGSPICE) 
  - [Day 4 - Pre-layout timing analysis and importance of good clock tree](#day-4---pre-layout-timing-analysis-and-importance-of-good-clock-tree)
    - [Formation of LEF and Timings modelling using delay table](#Formation-of-LEF-and-Timings-modelling-using-delay-table)
    - [Timing Analysis using OpenSTA](#timing-analysis-using-opensta)
    - [Clock Tree Synthesis using TritonCTS](#clock-tree-synthesis-using-tritoncts)
  - [Day 5 - Final steps for RTL2GDS](#day-5---final-steps-for-rtl2gds)
    - [Generation of Power Distribution Network](#generation-of-power-distribution-network)
    - [Routing using TritonRoute](#routing-using-tritonroute)
    - [SPEF File and GDSII Generation](#spef-file-and-GDSII-generation)
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

# Day 1 - Inception of open-source EDA, Open LANE and Sky130 PDK

##	How to talk to computers

### Basic IC Design Terminologies

![1 (3)](https://user-images.githubusercontent.com/20563301/124388801-12cc8b00-dd02-11eb-9143-b0554aeb25c4.PNG)


-	During the Physical Designing, one will come across multiple terminologies that are frequently used. Some of them are mentioned below:
-	Package: It is a case that surrounds the circuit material to protect it from physical damage or corrosion and allow mounting of the electrical contacts connecting it to the printed circuit board (PCB). The below snippet shows an IC with 48 pins and Quad Flat No-Leads (QFN) package.
-	Die: A die is a small block of semiconducting material on which a given functional circuit is fabricated.
-	Core: It is the actual area of the IC where the logic resides.
-	Pads: These are the interfaces between the internal signals of a chip and the external pins for transmitting signals.
-	Chip: It is an integrated circuit or small wafer of semiconductor material which is embedded with integrated circuitry.
-	Foundry IP’s (Intellectual Property): It means any and all information and inventions, which information or inventions relate to the design, genetic engineering, measurement or analysis of microbial host cells, small-scale fermentation, and all intellectual.


### Introduction to RISC-V

![1 (1)](https://user-images.githubusercontent.com/20563301/124388808-1bbd5c80-dd02-11eb-9b6c-a9516b008579.PNG)

RISC-V is a new ISA that's available under open, free and non-restrictive licenses. RISC-V ISA delivers a new level of free, extensible software and hardware freedom on architecture.


-	It is far simpler and smaller than other commercial ISAs available.
-	It avoids micro-architecture or technology dependent features.
-	It has small standard base ISA and multiple standard extensions.
-	It supports variable-length instruction encoding.
-	It convert a C file program into a Layout.

### 	From Software Applications to Hardware

![1 (4)](https://user-images.githubusercontent.com/20563301/124388811-211aa700-dd02-11eb-8728-480445db9463.PNG)

-	The Application Software (Apps) like Microsoft office act like an input and the system software help it to work on a hardware design (Chip Layout) like laptop.
-	The System software contain OS which converts the apps into its assembly language file and then to its binary language file. 
-	The Complier converts the C file from input into its respective instruction set file which depends upon the CPU and the instruction set file act like interface between the C file and hardware.
-	The instruction set depending upon its specification will create a RTL netlist and then the physical implementation of netlist is done into the hardware. 
-	The Assembler which converts the instruction into its binary format which is understand by the given hardware (Chip Layout).


## SoC design and Open LANE

### Introduction to all components of open-source digital basic design

a.	Open Source Digital ASIC Design Diagram


![9](https://user-images.githubusercontent.com/20563301/124388818-2aa40f00-dd02-11eb-93b4-ea0bbcce2dfd.PNG)


Above diagram shows components for Open Source Digital ASIC Design.

b.	Why 130 nm is used? Two Reasons
-	Skywater130 does not need advanced chips.
-	Fabrication of 130 nm is cheaper.



c.	What is PDK?
-	PDKs are interface between foundary and design engineers. 
-	PDKs contains set of files to model fabrication process for the design tools used to design IC like device models, DRC, LVS, Physical extraction, layers, LEF, standard cell libraries, timing libraries etc.


![3 (2)](https://user-images.githubusercontent.com/20563301/124388927-a30ad000-dd02-11eb-848c-66b7ce835078.PNG)



About Google SkyWater PDK
-	Google and SkyWater Technology Foundry in collaboration have released a completely open-source Process Design Kit(PDK) in May, 2020. 
-	The current release target to a SKY130 (i.e. 130 nm) process node is available as [SkyWater Open Source PDK](https://github.com/google/skywater-pdk). 
-	The PDK provides Physical VLSI Designer with a wide range of flexibility in design choices. All the designs and simulations listed in this repository are carried out using the same SkyWater Open Source PDK.


![12](https://user-images.githubusercontent.com/20563301/124389001-ebc28900-dd02-11eb-8638-d05ecd790cc5.PNG)



### 	Introduction To RTL to GDSII Flow

![10](https://user-images.githubusercontent.com/20563301/124388840-40b1cf80-dd02-11eb-85e8-f7df4c3eb665.PNG)


-	RTL to GDSII Flow refers to the all the steps involved in converting a logical Register Transfer Level (RTL) Design to a fabrication ready GDSII format. GDSII is a database file format which is an industry standard for data exchange of IC layout artwork.
-	The RTL to GSDII flow consists of following steps
-	 RTL Synthesis
-	 Static Timing Analysis (STA)
-	Design for Testability (DFT)
-	Floor planning
-	Placement
-	Clock Tree Synthesis (CTS)
-	Routing
-	GDSII Streaming

  All the steps are further discussed in details in the repository.


### Introduction to Open LANE detailed ASIC design flow

![11](https://user-images.githubusercontent.com/20563301/124388850-47d8dd80-dd02-11eb-86ec-05bd334a2c4a.PNG)



-	[Open LANE](https://github.com/efabless/openlane) is an automated RTL to GDSII flow which includes various open-source components such as OpenROAD, Yosys, Magic, Fault, Netgen, and SPEF-Extractor.
-	 It also facilitates to add custom design exploration and optimization scripts.

-	There are Two modes of operation of OpenLane 
a.	Autonomous: It figures the flow and push the bottom flow and wait for time based on design size and get the finalGDS reports.
b.	Interactive: it peforms the flow one at a time.

-	The detailed diagram of the Open LANE architecture is shown below:




-	Open LANE flow consists of several stages. By default all flow steps are run in sequence. Each stage may consist of multiple sub-stages. Open LANE can also be run interactively as shown here.

  1. Synthesis
      1. `yosys` - Performs RTL synthesis
      2. `abc` - Performs technology mapping
      3. `OpenSTA` - Performs static timing analysis on the resulting netlist to generate timing reports
  2. Floorplan and PDN
      1. `init_fp` - Defines the core area for the macro as well as the rows (used for placement) and the tracks (used for routing)
      2. `ioplacer` - Places the macro input and output ports
      3. `pdn` - Generates the power distribution network
      4. `tapcell` - Inserts welltap and decap cells in the floorplan
  3. Placement
      1. `RePLace` - Performs global placement
      2. `Resizer` - Performs optional optimizations on the design
      3. `OpenPhySyn` - Performs timing optimizations on the design
      4. `OpenDP` - Perfroms detailed placement to legalize the globally placed components
  4. CTS
      1. `TritonCTS` - Synthesizes the clock distribution network (the clock tree)
  5. Routing *
      1. `FastRoute` - Performs global routing to generate a guide file for the detailed router
      2. `TritonRoute` - Performs detailed routing
      3. `SPEF-Extractor` - Performs SPEF extraction
  6. GDSII Generation
      1. `Magic` - Streams out the final GDSII layout file from the routed def
  7. Checks
      1. `Magic` - Performs DRC Checks & Antenna Checks
      2. `Netgen` - Performs LVS Checks   
## Open-Source EDA Tools

### Open LANE Initialization 
-	For invoking OpenLANE in Linux Ubuntu, we should first run the docker everytime we use OpenLANE. This is done by using the following script:
```
docker run -it -v $(pwd):/openLANE_flow -v $PDK_ROOT:$PDK_ROOT -e PDK_ROOT=$PDK_ROOT -u $(id -u $USER):$(id -g $USER) openlane:rc6
```
-	A custom shell script or commands can be generated to make the task simpler.
•	To invoke OpenLANE run the ./flow.tcl script.
•	OpenLANE supports two modes of operation: interactive and autonomous.
•	To use interactive mode use -interactive flag with ./flow.tcl


![3 (1)](https://user-images.githubusercontent.com/20563301/124388881-68a13300-dd02-11eb-9a2e-42a2bbf0646a.PNG)



### Design Preparation
-	The first step after invoking OpenLANE is to import the openlane package of required version. This is done using following command. Here 0.9 is the required version of OpenLANE.
```
package require openlane 0.9
```
-	The next step is to prepare our design for the OpenLANE flow. This is done using following command:


```
prep -design <design-name>
```
-	Some additional flags that can be used while preparation are:

-tag <name-for-current-run> - All the files generated during the flow will be stored in a directory named <name-for-current-run>
-overwrite - If a directory name mentioned in -tag already exists, it will be overwritten.
-	During the design preparation the technology LEF and cell LEF files are merged together to obtain a merged.lef file. The LEF file contains information like the layer information, set of design rules, information about each standard cell which is required for place and route.
  
  
### Design Synthesis and Results
The first step in OpenLANE flow is RTL Synthesis of the design loaded. This is done using the following command.
```
run_synthesis
```
Directory to see the synthesis report
  
```
cd designs/picorv32a/runs/02-07_09-05/reports/synthesis
```
  
![3 (1)](https://user-images.githubusercontent.com/20563301/124389093-4a880280-dd03-11eb-85c5-c0e568f6d98e.PNG)
  
![13](https://user-images.githubusercontent.com/20563301/124389106-57a4f180-dd03-11eb-874c-4b83a63665f6.PNG)
  
 
  
  
# Day 2 - Good floorplan vs bad floorplan and introduction to library cells
  
##	Chip Floor planning

Chip Floor planning is the arrangement of logical block, library cells, pins on silicon chip. It makes sure that every module has been assigned an appropriate area and aspect ratio, every pin of the module has connection with other modules or periphery of the chip and modules are arranged in a way such that it consumes lesser area on a chip.

### Utilization Factor and Aspect Ratio
-	Utilization Factor is ratio of the area occupied by netlist to the total core area. The utilization factor is generally kept in the range of 0.5-0.7 i.e. 50% - 60%. Maintaining a proper utilization factor facilitates placement and routing optimization.
-	Aspect Ratio is ratio of Height to Width of dice. If it is 1 then it is square dice.
  
###	Pre Placed Cells
-	These are cells which contain macros and IP which is a part of complex logic which is executed once and use multiple times in a netlist.
-	The arrangement of these IP in a chip is referred as Floor Planning.
-	Automated placement and routing tools does not change the location of pre placed cells in the design onto chip.


###	De-Coupling Capacitors
-	These capacitors are connected to switching circuits of pre placed cells which can causes output go to undefined region in Noise margin (ie if input is 1 then output is 0) due to voltage drop causes by the wire in circuit. 
-	These capacitors charge/discharge according to switching operation of pre placed cells.

### Power Planning
-	Consider if a numbers of Black boxes of logic are connected to each other in 16 bit bus and a wire is connected between a driver box and load box.
-	Since a decoupling capacitor cannot be connected between them hence there is a voltage drop between them due to single voltage source.
-	If the 16 bit bus is connected to an inverter then all capacitors which were charged to `V(1)’ volts will be discharge to `0’ volts through a single ground tap point. This will create a bump in `Ground’ tap point and if is greater then Noise margin then it will leads to undesired region.
-	If the vice versa happens i.e. all capacitors which were 0 volts will have to charge to `V’ through a single Vdd tap pin .This will cause a voltage drop in circuit.
-	The above problem can be solved if the individual black boxes is connected to VDD and VSS.

### Pin Placement

Pin placement is a important part of floorplanning as the timing delays and number of buffers required is dependent on the position of the pin. There are multiple pin placement option available such as equidistant placement, high-density placement.


### Floorplanning using Open Lane
The following commands are used to perform Floorpalnning:
  
a.	To see the I/O pins in Floorplanning
```
•	run_floorplan
•	cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/01-07_05-54/logs/floorplan less 4-ioPlacer.log
```
b.	To see the Floorplanning in OpenLane

```
•	cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/01-07_05-54/results/floorplan
•	less picorv32a.floorplan.def
```
![5](https://user-images.githubusercontent.com/20563301/124389189-b23e4d80-dd03-11eb-944e-b9797da92a44.PNG)
   
  

### Floorplanning using Magic

Magic tool provide a very easy to use interface to design various layers of the layout. It also has an in-built DRC check fetaure

```
•	run_floorplan
  
•	cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/01-07_05-54/results/floorplan
  
•	magic -T /home/rohit/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &  
```
![6](https://user-images.githubusercontent.com/20563301/124389198-bd917900-dd03-11eb-94b4-9255f818a7a4.PNG)
 
![7](https://user-images.githubusercontent.com/20563301/124389203-c1250000-dd03-11eb-9439-18a2ea1c4ce2.PNG)
  
![4](https://user-images.githubusercontent.com/20563301/124389213-cda95880-dd03-11eb-9bf3-37f3f6004646.PNG)
  
  
Priority of .tcl files are like: sky130A_sky130 fd_sc_hd.config.tcl  > config.tcl(reports) > floorplan.tcl(default value).
  
  <table border="0">
  <tr>
    <td><img src="https://user-images.githubusercontent.com/20563301/124389309-21b43d00-dd04-11eb-80c6-1fb136016cdb.PNG"> </td>
    <td> <img src="https://user-images.githubusercontent.com/20563301/124389330-35f83a00-dd04-11eb-9aa2-271207214c1e.PNG"> </td>
  </tr>
  <tr>
    <td><img src="https://user-images.githubusercontent.com/20563301/124389351-4c9e9100-dd04-11eb-9233-0392c785a54a.PNG"> </td>
   </tr>
  </table> 
  


## Placement

### Placement and Optimization
-	First the given netlist is convert into physical cells of proper dimension and the library contains all these cells and its different flavors.
-	The cells are placed in the flooring such that it has minimum delay with output and are not be placed in pre placed cells area.
-	Due to limited space in chip, sometimes the cells are placed far away from input which creates a delay between them.
-	In order to overcome such problem, Optimize Placement is used.
-	 It is a stage which estimates the wire length and capacitance and based on them repeaters are used to maintain the signal integrity. 
-	Due to this more area is used and if the cell is too far away then more wire length and more capacitance value which will create bad stew.
-	In order to have minimum delays between the cells, the cells are abutted.


### Placement using Open Lane

-	Placement in OpenLANE is done using the following command 
  
 ```
    run_placement
```
   
-	The DEF file created during floorplan is used as an input to placement. Placement in OpenLANE occurs in two stages:
  
   a. Global Placement: It is placement which forcefully placed the standard cells in different rows and are not abutt to each other.
  
   b. Detailed Placement: It is placement which legality placed the standard cells in standard rows and are abutt to each other.

-	Placement is carried out as an iterative process till the value of overflow converges to 0.
-	Placement is done in magic by following command
```
-	run_placement
-	cd Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/01-07_05-54/results/placement
-	magic -T/home/rohit/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def &

```
  
![9](https://user-images.githubusercontent.com/20563301/124389440-b7e86300-dd04-11eb-9480-ac1fdc979d99.PNG)
  

![10](https://user-images.githubusercontent.com/20563301/124389450-c0409e00-dd04-11eb-992a-a0913c7f7088.PNG)
  
  
![11](https://user-images.githubusercontent.com/20563301/124389454-c59de880-dd04-11eb-97c0-961a64183282.PNG)
  
  
  
  
## Cell Design and Characterization Flows
  
### Cell Design Flow
 

-	Library is the collections of gates or standard cells in given area which are model in such a way that Open EDA tools understand.
-	Library has cells of different functionality and of different sizes and also contain cells with different threshold voltages.
-	The Cell Design Flow contains of 3 parts which are as follows:
  
  
 ![12](https://user-images.githubusercontent.com/20563301/124389486-f1b96980-dd04-11eb-929b-d27a34e26ee1.PNG)
 
  

  
### Characterization Flow
Standard Cell Characterization
Standard Cell Libraries consist of cells with different functionality/drive strengths. These cells need to be characterized by liberty files to be used by synthesis tools to determine optimal circuit arrangement. The open-source software GUNA is used for characterization.
Characterization is a well-defined flow consisting of the following steps:
1.	Link Model File of CMOS containing property definitions
2.	Specify process corner(s) for the cell to be characterized
3.	Specify cell delay and slew thresholds percentages
4.	Specify timing and power tables
5.	Read the parasitic extracted netlist
6.	Apply input or stimulus
7.	Provide necessary simulation commands
  
  
# Day 3 - Design library cell using Magic Layout and ngspice characterization

## CMOS inverter using ngspice simulations


### I/O Placer 
The following commands are used to change the I/O placer in floorplan
  
```
•	cd Desktop/work/tools/openlane_working_dir/openlane
•	docker
•	./flow.tcl -interactive
•	package require openlane 0.9
•	prep -design picorv32a 
•	run_synthesis
•	run_floorplan
•	cd configuration
•	less floorplan.tcl
•	set ::env(FP_IO_MODE) 1
•	set ::env(FP_IO_MODE) 2
•	run_floorplan
•	cd designs/picorv32a/runs/02-07_09-05/results/floorplan
•	magic -T /home/rohit/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &

```
  
  
 ![14  i o placer change](https://user-images.githubusercontent.com/20563301/124389532-2fb68d80-dd05-11eb-960a-be9b02611637.PNG)



###	Spice Desk creation and simulation for CMOS invertor
-	Spice Desk is the connectivity information of netlist. It consists of varies components like gates, component values and many more.
-	Syntax for transistor in Spice is `transistor name drain gate source substrate transistor type W L’
-	Syntax for pulse in Spice is `initial value final value risetime falltime pulsewidth completecyclewidth` 
-	The following commands are used for DC/static characteristics simulation in Spice

```
•	cd [directory]
•	source .cir file
•	run
•	setplot
•	display
•	plot out  VS in

```
-	Depending upon the W/L paraments ,CMOS invertor static characteristics is simulated in Spice
-	Switching Threshold is a point in static characteristics where Vin =Vout and prove the CMOS invertor is robust device.
-	Dynamic characteristics gives the delay in circuit through the rising and falling time of ideal and practical pulse.

  

### CMOS invertor using Design using Magic
  
-	The inverter design is done using Magic Layout Tool. It takes the technology file as an input (`sky130A.tech` in this case). Magic tool provide a very easy to use interface to design various layers of the layout. It also has an in-built DRC check feature.
-	The following commands is used for simulation
```
•	git clone https://github.com/nickson-jose/vsdstdcelldesign.git
•	cd Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic
•	cp sky130A.tech ~/Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign/
•	magic -T sky130A.tech sky130_inv.mag &
```
-	The snippet below shows a layout for CMOS Inverter with and without design rule violations.
  
 ![4](https://user-images.githubusercontent.com/20563301/124389583-7906dd00-dd05-11eb-8672-1e9a6fcece43.PNG)
  
![5](https://user-images.githubusercontent.com/20563301/124389590-7dcb9100-dd05-11eb-8146-dfd423789e02.PNG)
 



## CMOS fabrication process
  
The 16-mask CMOS Fabrication process is carried out in following ways:
1.	Selecting a substrate
2.	Creating active region for transistors
3.	Formation of N –Well and P-Well 
4.	Formation of gate terminal
5.	Formation of lightly doped drain(LDD)
6.	Formation of Source and Drain terminal
7.	Formation of contacts and interconnects
8.	Metallization
 

## Sky130 Tech File Labs

###	Extract SPICE Netlist from Standard Cell Layout

To simulate and verify the functionality of the standard cell layout designed, there is a need of SPICE netlist of a given layout. To mention in brief, "Simulation Program with Integrated Circuit Emphasis (SPICE)" is an industry standard design language for electronic circuitry. SPICE model very closely models the actual circuit behavior. Extraction of SPICE model for a given layout is done in two stages. 
  
```
•	extract all : Extract the circuit from the layout design.
•	ext2spice cthresh 0 rthresh 0 : Convert the extracted circuit to SPICE model.
•	ext2spice
```

![6](https://user-images.githubusercontent.com/20563301/124389603-9340bb00-dd05-11eb-890a-148cff67cb31.PNG)
 
  
### Transient Analysis using NGSPICE
         Few modifications needs to be done in spice deck file
-	Scale needs to be aligned with the layout grid size and check the model name from pshort.lib and nshort.lib
-	Specify power supply
-	Apply stimulus
-	Perform transient analysis
-	The SPICE netlist generated in previous step is simulated using the NGSPICE tool. NGSPICE is an open-source mixed-level/mixed-signal electronic spice circuit simulator. The command used to invoke NGSPICE is shown below.

`
 cd Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign/ ngspice sky130_inv.spice

`
![8](https://user-images.githubusercontent.com/20563301/124389632-af445c80-dd05-11eb-9878-9bc6ab41b479.PNG)
  
  
Following command is used to plot waveform in ngspice tool.
```
ngspice 1 -> plot y vs time a

``` 
Below figure shows the waveform of Inverter output vs input w.r.t. time. Many timing parameters like rise time delay, fall time delay, propagation delay are calculated using this waveform.
  
![9](https://user-images.githubusercontent.com/20563301/124389664-c6834a00-dd05-11eb-9cc9-23783bcff68b.PNG)
  
  

# Day 4 - Pre-layout timing analysis and importance of good clock tree
  
  
In order to use a design of standard cell layout in OpenLANE RTL2GDS flow, it is converted to a standard cell LEF. LEF stands for Library Exchange Format. The entire design has to be analyzed for any timing violations after addition or change in the design.

## Formation of LEF and Timings modelling using delay table
  

i.	Magic Layout to Standard Cell LEF
-	Before creating the LEF file we require some details about the layers in the designs. This details are available in a tracks.info as shown below. It gives information about the offset and pitch of a track in a given layer both in horizontal and vertical direction. The track information is given in below mentioned format.

```
<layer-name> <X-or-Y> <track-offset> <track-pitch>
```
 
![1](https://user-images.githubusercontent.com/20563301/124389694-e155be80-dd05-11eb-8217-f945eeeb549b.PNG)
  
  
-	There are some rules which should be follow for proper LEF
  
a.	The Input and Output ports must lie on intersection of vertical and horizontal track.
  
b.	Width of standard cell should be in odd multiple of X track pitch and height should be in odd multiple of Y track pitch.


![2](https://user-images.githubusercontent.com/20563301/124389721-0ea26c80-dd06-11eb-85ee-03af1e07c674.PNG)
  
  
- The following commands are used to create and extract LEF from magic
```
•	cd Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign/

•	magic -T sky130A.tech sky130_inv.mag &

•	grid 0.46um 0.34um 0.23um 0.17um

•	save sky130_vsdinv.mag 

•	lef write
```
  
  
  
The following commands are used to see the delay, synthesis and Placement for a modified LEF file
  
```
•	Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign/ cp sky130_vsdinv.lef ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/  
  
•	Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign/libs cp sky130_fd_sc_hd_*  ~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src/
  
•	Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a vim config.tcl
  
```
 Edit the config.tcl according to below file
![3](https://user-images.githubusercontent.com/20563301/124389828-87092d80-dd06-11eb-960e-c5bdbc2a2819.PNG)
  
Magic output with modification file
  
 ![4](https://user-images.githubusercontent.com/20563301/124389873-c8014200-dd06-11eb-84f6-7928680aba57.PNG)


 

ii.	Delay Table
-	In order to save the Switching and short circuit power, gates are used to enable/disable the clock pulse. This is called Clock gatering. All the other paraments like pulse, width remain same.
-	Due to this it can be used in big and complex circuit. If a buffer is connected in levels to produce clock pulse and then the clock tree is not constant.
-	This is because of two reasons 
a.	input transition time is varying
b.	output load is varying    Hence delay table is used
-	The input transition time is varied for limited time (20ps-80ps) to output load time which also varied for limited time (10fF-110fF) and delay is found in the form of a table for different kinds of gates and cells of different sizes.
-	If the sizes of PMOS and NMOS are varying then the resistance is varying and hence the delay is also varying.
-	For a particular input transition time if the output load time is not given in delay table then it can be found out by finding the equation of delay table and putting the values in it.
-	If identical buffers are connected in same level then the input transition time and output load time will be same. Hence it will have same delay which will be skew=0.
-	If identical buffers are connected in same level but will different output load time then delay for both the buffer will be different which will led to non-zero skew.
-	If buffers of different sizes are connected in same level then delay for both the buffer will be different which will led to non-zero skew.
-	Hence for perfect timing analysis 
a.	Identical buffer are use at same level
b.	At every level, each node should drive the same load.
  
  
## Timing Analysis using OpenSTA
  
-	The Static Timing Analysis(STA) of the design is carried out using the OpenSTA tool. The analysis can be done in to different ways.
  
i. Inside OpenLANE flow: This is by invoking openroad command inside the OpenLANE flow. In the openroad OpenSTA is invoked.

ii. Outside OpenLANE flow: This is done by directly invoking OpenSTA in the command line. This requires extra configuration to be done to specific the verilog file, constraints, clcok period and other required parameters.
OpenSTA is invoked using the below mentioned command.
```
sta sta.conf
```
  
![6](https://user-images.githubusercontent.com/20563301/124389917-f67f1d00-dd06-11eb-94ff-579220e3c25f.PNG)
  
  
-	The above command gives an Timing Analysis Report which contains:
1.	Hold Time Slack
2.	Setup Time Slack
3.	Total Negative Slack (= 0.00, if no negative slack)
4.	Worst Negative Slack (= 0.00, if no negative slack)
  
  
-	If the design produces any setup timing violaions in the analysis, it can be eliminated or reduced using techniques as follows:
a.	Increase the clock period (Not always possible as generally operating frequency is freezed in the specifications)
b.	Scaling the buffers (Causes increase in design area)
c.	Restricting the maximum fan-out of an element.
  
 
![8](https://user-images.githubusercontent.com/20563301/124389933-0d257400-dd07-11eb-9a89-357ec638a798.PNG)



## Clock Tree Synthesis using TritonCTS
  
-	Clock Tree Synthesis(CTS) is a process which makes sure that the clock gets distributed evenly to all sequential elements in a design. The goal of CTS is to minimize the clock latency and skew. There are several CTS techniques like:
a.	H - Tree
b.	X - Tree
c.	Fish bone
  
-	Buffering in CTS IS such that it add repeaters in between the flops that only difference is that it have equal rise and fall time.
-	Clock Net Shielding is a stage where it shield the wires from both the sides and is connected to VDD and GND.
-	It prevents two important problems
  
a.	Glitch: It happens when a high signal alter the polarity of switching value which a error in circuit.
  
b.	Crosstalk: It happens due to glitch in switching activity which creats a delay in waveform and amplify according to the numbers if elements.

-	The command used for running CTS in OpenLANE is given below.
```
run_cts
```
 ![9](https://user-images.githubusercontent.com/20563301/124389962-229a9e00-dd07-11eb-8837-133c64a22f21.PNG)
  
 
Setup Timings and Hold Analysis
-	Setup time delay is the time taken by the capture Flop for the input to settle at the center of flop ie internal delay due first MUX.
-	This delay not only resist and but always is less than combinational delay
-	Jitter is the temporary variation of Clock period by real chip/PLL to flip flops.
-	It can be solved by introducing a setup uncertainty before the setup time.
-	Hold time delay is the time taken by the capture flop to send the input data to outside of the flop ie internal delay of second MUX.
  
  
  
  
Further analysis of CTS in done in openROAD which is integrated in openLANE flow using openSTA tool.
```
% openroad
```
In openROAD the timing analysis is done by creating a db file from `lef` and `def` files. `lef` file won't change as it a tecnology file, `def` file changes when a new is added.

```
% read_lef /openLANE_flow/designs/picorv32a/runs/test1/tmp/merged.lef
% read_def /openLANE_flow/designs/picorv32a/runs/test1/results/cts/picorv32a.cts.def
% write_db picorv32a_cts.db
```
  
![11](https://user-images.githubusercontent.com/20563301/124388458-aa30de80-dd00-11eb-89d1-5ad1775cdbd8.PNG)
 

This creates db file in `$OPENLANE_ROOT` directory.

```
•	% read_db picorv32a_cts.db
•	% read_verilog /openLANE_flow/designs/picorv32a/runs/test1/results/synthesis/picorv32a.synthesis_cts.v
•	% read_liberty -max $::env(LIB_SLOWEST)
•	% read_liberty -min $::env(LIB_FASTEST)
•	% read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc
•	% set_propagated_clock [all_clocks]
•	% report_checks -path_delay min_max -format full_clock_expanded -digits 4
```

We have done pre-CTS timing analysis to get setup and hold slack and post-CTS timing analysis to get setup and hold slack. 
For typical corners (`LIB_SYN_COMPLETE` env variable which points to typical library) setup and hold slack are met.

[horizontal]
`hold slack`:: 0.0167 ns
`setup slack`:: 4.5420 ns

```
•	% echo $::env(CTS_CLK_BUFFER_LIST)
•	sky130_fd_sc_hd__clkbuf_1 sky130_fd_sc_hd__clkbuf_2 sky130_fd_sc_hd__clkbuf_4 sky130_fd_sc_hd__clkbuf_8
```

Trying removing `sky130_fd_sc_hd__clkbuf_1` from clock tree and do post cts timing analysis
```
•	% set ::env(CTS_CLK_BUFFER_LIST) [lreplace $::env(CTS_CLK_BUFFER_LIST) 0 0]
•	sky130_fd_sc_hd__clkbuf_2 sky130_fd_sc_hd__clkbuf_4 sky130_fd_sc_hd__clkbuf_8
•	% echo $::env(CTS_CLK_BUFFER_LIST)
•	sky130_fd_sc_hd__clkbuf_2 sky130_fd_sc_hd__clkbuf_4 sky130_fd_sc_hd__clkbuf_8
```

```
•	% echo $::env(CURRENT_DEF)
•	/openLANE_flow/designs/picorv32a/runs/test1/results/cts/picorv32a.cts.def
•	% 
•	% set ::env(CURRENT_DEF) /openLANE_flow/designs/picorv32a/runs/test1/results/placement/picorv32a.placement.def
```

Now run openROAD and do a timing analysis as mentioned above.
[horizontal]
`hold_slack`:: 0.1840 ns
`setup_slack`:: 4.7490 ns
Including large size clock buffers in clock path improves slack but area increases.

To check the clock skew
```
•	% report_clock_skew -hold
•	Clock clk
•	Latency      CRPR       Skew
•	_35319_/CLK ^
•	   1.31
•	_34316_/CLK ^
•	   0.80      0.00       0.51

•	% report_clock_skew -setup
•	Clock clk
•	Latency      CRPR       Skew
•	_35319_/CLK ^
•	   1.31
•	_34316_/CLK ^
•	   0.80      0.00       0.51

```  
# Day 5 - Final steps for RTL2GDS

 ## Generation of Power Distribution Network
  
  
![2](https://user-images.githubusercontent.com/20563301/124387367-f2013700-dcfb-11eb-8482-5d95d93f5977.PNG)
  
  

-	In a normal RTL to GDSII flow the generation of power distribution network is done before the placement step, but in the OpenLANE flow generation of PDN is carried out after the Clock Tree Synthesis(CTS). This step generates all the tracks, rails required for routing power to entire chip. Generation of power distribution network is done using following command.
`
-	gen_pdn
`
  
![1](https://user-images.githubusercontent.com/20563301/124387384-09d8bb00-dcfc-11eb-8b85-6f7f015b7e0c.PNG)
  
  
  
## Routing using TritonRoute
  
  OpenLANE uses TritonRoute, an open source router for modern industrial designs. The router consists of several main building blocks, including pin access analysis, track assignment, initial detailed routing, search and repair, and a DRC engine. The routing process is implemented in two stages:
1.	Global Routing - Routing guides are generated for interconnects
2.	Detailed Routing - Tracks are generated interatively. TritonRoute 14 ensures there are no DRC violations after routing.
The following command is used for routing.
`
run_routing
`
 [horizontal]
`*FastRoute*`:: Performs global routing to generate a guide file for the detailed router
`*CU-GR*`:: Another option for performing global routing.
`*TritonRoute*`:: Performs detailed routing
`*SPEF-Extractor*`:: Performs SPEF extraction
  
![3](https://user-images.githubusercontent.com/20563301/124387942-0cd4ab00-dcfe-11eb-9377-7467cbed6425.PNG)
  
![4](https://user-images.githubusercontent.com/20563301/124387950-13632280-dcfe-11eb-95ce-562f2b359981.PNG)


  

After routing magic tool can be used to get routing view
```
 /home/rohit//work/tools/openlane_working_dir/openlane/designs/picorv32a/runs$ magic -T $PDK_ROOT/sky130A/libs.tech/magic/sky130A.tech lef read test1/tmp/merged.lef def read test1/results/routing/picorv32a.def &
```
![8](https://user-images.githubusercontent.com/20563301/124390819-e10bf200-dd0a-11eb-9a2f-fdc90291066a.PNG)
  
![5](https://user-images.githubusercontent.com/20563301/124390824-e5d0a600-dd0a-11eb-8616-131b22e604b6.PNG)


  
## SPEF File and GDSII Generation
  After routing has been completed interconnect parasitics can be extracted to perform sign-off post-route STA analysis. The parasitics are extracted into a SPEF file using SPEF-Extractor.

`spef` file will be generated after `run_routing` command at location 
`/home/rohit/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/test1/results/routing/picorv32a.spef`
  
![9](https://user-images.githubusercontent.com/20563301/124390863-24666080-dd0b-11eb-958e-745ccbb721f1.PNG)


GDSII
  
GDSII files are usually the final output product of the IC design cycle and are given to silicon foundries for IC fabricationIt is a binary file format representing planar geometric shapes, text labels, and other information about the layout in hierarchical form.

To generate GDSII file, type the below command in openlane after the routing
```
% run_magic
```
![10](https://user-images.githubusercontent.com/20563301/124390866-27f9e780-dd0b-11eb-839e-679ef9e48d5d.PNG)


`gds` file will be generated at location `/home/rohit/Desktop/designs/picorv32a/runs/test1/results/magic/picorv32a.gds`


 # Acknowledgements 
  - Kunal Ghosh , Co-founder (VSD Corp. Pvt. Ltd) 
  - Mansi Mohapatra
  - Milli Anand
  # References
  - https://www.vlsisystemdesign.com/advanced-physical-design-using-openlane-sky130/
  - https://github.com/The-OpenROAD-Project/OpenLane/blob/master/configuration/README.md
  - https://gitlab.com/gab13c/openlane-workshop
  - https://github.com/29Rohit/OpenSource_Physical_Design.git
  
 
  
  
  
