


# Advanced-Physical-Design-using-OpenLANE-and-Sky130
Workshop on: Advanced Physical Design using OpenLANE Sky130

Openlane is a package of tools that consists of many tools needed for the overall process from Design to GDSII
location of the Openlane is in openlane_build_script/work/tools/openlane_working_dir/openlane

The basic idea of Openlane is to have a complete flow

- [About The Project](#Day-1)
- [Physical Design Flow](#Day-1)
- [Opensource Tools used for RTL to GDSII](#Day-1)
- [Installing the vsdflow Tool](#Day-1)
- [Complete Flow of OpenLane](#Day-1)
- [Different steps in VLSI Flow](#Day-1)
   - [Synthesis](#Day-1)
   - [Floorplan and PDN](#Day-1)
   - [CTS ](#Day-1)
   - [Routing](#Day-1)
   - [GDSII Generation](#Day-1)
   - [Checks](#Day-1)
- [LAB Day 1](#Day-1)
- [LAB Day 2](#Day-1)
- [LAB Day 3](#Day-1)
- [LAB Day 4](#Day-1)
- [LAB Day 4](#Day-1)
## About The Project

This project gives you an overall idea of Openlane opensource PDK a tool developed from complete automated flow from RTL to GSDII based on several components like OpenROAD, Yosys, Magic, Netgen, Fault, OpenPhySyn, etc. OpenLANE uses Skywater 130nm open-source PDK and can be used to produce hard macros and chips.

## Physical Design Flow
![](https://upload.wikimedia.org/wikipedia/commons/thumb/0/0d/PhysicalDesign.png/1024px-PhysicalDesign.png)
Image Source : [wikipedia](https://en.wikipedia.org/wiki/Physical_design_(electronics))

The main steps in the ASIC (Application-specific integrated circuit)  physical design flow are:
-   Design Netlist (after synthesis)
-   Floorplanning
-   Partitioning
-   Placement
-   Clock-tree Synthesis (CTS)
-   Routing
-   Physical Verification
-   Layout Post Processing with Mask Data Generation

###  Opensource Tools used for RTL to GDSII
```
   YOSYS- Logic synthesis
   GREYWOLF- Placement 
   QROUTER- routing
   OPEN_TIMER- Static timing analysis
   MAGIC - layout viewer
   eSPICE - For SPICE simulations with schematically capturing the responses and functionality.
   Qflow - It is provided in order to ease the total design process for complete flow of RTL to GDSII 
```
### Installing the vsdflow Tool
```
  git clone https://github.com/kunalg123/vsdflow.git
  cd vsdflow
  chmod 777 opensource_eda_tool_install.sh
  ./opensource_eda_tool_install.sh
```
### Complete Flow of OpenLane
![asd](https://raw.githubusercontent.com/chyavanphadke/Physical-Design_using_OpenLANE_and_Sky130/main/Images/openlane.flow.1.png)

OpenLANE can also be run as interactively or as fully automated.

#### Different steps in VLSI Flow:
#### 1.  Synthesis
-   Yosys : Performs RTL synthesis using GTech mapping
-   abc : Performs technology mappin to standard cells described in the PDK. We can adjust synthesis techniques using different integrated abc scripts to get desired results
-   OpenSTA : Performs static timing analysis on the resulting netlist to generate timing reports
-   Fault : Scan-chain insertion used for testing post fabrication. Supports ATPG and test patterns compaction

#### 2.   Floorplan and PDN
-   Init_fp - Defines the core area for the macro as well as the rows (used for placement) and the tracks (used for routing)
-   Ioplacer - Places the macro input and output ports
-   PDN - Generates the power distribution network
-   Tapcell - Inserts welltap and decap cells in the floorplan
-   Placement – Placement is done in two steps, one with global placement in which we place the designs across the chip, but they will not be legal placement with some standard cells overlapping each other, to fix this we perform a detailed placement which legalizes the design and ensures they fit in the standard cell rows
-   RePLace - Performs global placement
-   Resizer - Performs optional optimizations on the design
-   OpenPhySyn - Performs timing optimizations on the design
-   OpenDP - Perfroms detailed placement to legalize the globally placed components

#### 3. CTS
-   TritonCTS - Synthesizes the clock distribution network

#### 4.   Routing
-   FastRoute - Performs global routing to generate a guide file for the detailed router
-   TritonRoute - Performs detailed routing from global routing guides
-   SPEF-Extractor - Performs SPEF extraction that include parasitic information

#### 5.  GDSII Generation
-   Magic - Streams out the final GDSII layout file from the routed def

#### 6.  Checks
-   Magic - Performs DRC Checks & Antenna Checks
-   Netgen - Performs LVS Checks

## LAB Day 1
#### File structure inside openLane directory
![](https://raw.githubusercontent.com/chyavanphadke/Physical-Design_using_OpenLANE_and_Sky130/main/Images/fileStructure.png)

First step is to set the package required using:
```
pakage require openlane 0.9
```
Then design preparation is done using the following command:
```
prep -design designFolder -tag userDefinedOutputFolderName
```
![](https://raw.githubusercontent.com/chyavanphadke/Physical-Design_using_OpenLANE_and_Sky130/main/Images/design%20preparation.png)

Adter running the prep command wait for the design preparaion to complete, it might take some time based on the configuration and the design file.

![](https://raw.githubusercontent.com/chyavanphadke/Physical-Design_using_OpenLANE_and_Sky130/main/Images/preparation%20completed.png)

wait for the "[INFO]: Preparation completed" conformation. The next step is to start the synthesis. The following command is used to start the synthesis.
```
run_synthesis
```
Synthesis takes some time based on the size and complexity of the design. Completion of the synthesis is displayed by "[INFO]: Synthesis is completed" message.
![](https://raw.githubusercontent.com/chyavanphadke/Physical-Design_using_OpenLANE_and_Sky130/main/Images/synthesis%20completed.png)
## LAB Day 3
### Tools Installed 
- Static Timing Analysis tool succesfully in place.
![](https://raw.githubusercontent.com/chyavanphadke/Physical-Design_using_OpenLANE_and_Sky130/main/Images/staSuccess.png)

- Yosys installed succesfully
![](https://raw.githubusercontent.com/chyavanphadke/Physical-Design_using_OpenLANE_and_Sky130/main/Images/yosysSuccess.png)

- OpenTimer installed and working check
![](https://raw.githubusercontent.com/chyavanphadke/Physical-Design_using_OpenLANE_and_Sky130/main/Images/opentimerSuccess.png)

- GrayWolf tool inplace
![](https://raw.githubusercontent.com/chyavanphadke/Physical-Design_using_OpenLANE_and_Sky130/main/Images/graywolfSuccess.png)

- Qflow GUI
![](https://raw.githubusercontent.com/chyavanphadke/Physical-Design_using_OpenLANE_and_Sky130/main/Images/qflowSuccess.png) 

## LAB Day 3
#### What is Slack
-   It is difference between the desired arrival times and the actual arrival time for a signal.
-   Slack time determines [for a timing path], if the design is working at the desired frequency.
-   Positive Slack indicates that the design is meeting the timing and still it can be improved.
-   Zero slack means that the design is critically working at the desired frequency.
-   Negative slack means , design has not achieved the specified timings at the specified frequency.
-   Slack has to be positive always and negative slack indicates a violation in timing.

Positive slack is required for the design to work properly. Here in taken example we have a slack of 1.27. So slack requirements are fulfilled.

### IC Planning
 IC Plannning or also called as Chip planning is the crutual step in Physical design flow. The important aspects like the area of the core, utilisation factor, Powe planning and cell placement are taken care in this stage.

### Height and width of core
-   Core is the section of chip where the fundamental logic is placed
-   Die consists of core and it is a ssemiconductor material on which the circuit is fabricated.
-   Utilisation factor is the ratio of Area occupied by netlist and the Total Area of core. The 100% utilisation refers to Utilisation factor being 1. However, in the practical scenarios only 50-60% utilisation is considered in order to provide place for other routing and filler cells etc.
-   Aspect Ratio is the ratio o the heught and width of the core. The Aspect ratio of 1 refers to a square chip.

### Pre-placed Cells
-   Pre-placed cells are those which are implemented once and instantiated many times. The arrangement of these IPs in the chip is referred to as Floorplanning.
-   These IPs/blocks have user defined locations and hence are placed in chip before the automated placement and routing.

### Decoupling Capacitors
-   Large complex circuits will have high amount of switching current.
-   Noise mArgin specs define the logic'0' and logic '1' valid voltages and undefined regions.
-   The high switching current demand can be solved by addition of decoupling capacitors in parallel with the circuit.

### Power Planning
-   The power planning should be done in a way that the driver and load be close to each other in the 'L' sense.
-   The improper power planning i.e., single power and Ground lines can lead to 'Ground bounce' and 'Voltage Drrop'.
-   So the plan should have multiple 'VDD', 'VSS' lines running through the circuit.

### Pin Placement
-   The conectivity of the chip to the outside world.
-   The placement of the pins is dependent on the position (near/far) but not on the ordering.
-   The clock ports are found to be bigger than the general data ports in order to necessitate for less resistance.
- 
### Placement and Routing
-   Bind the netlist with the physical cells i.e., library cells
-   Placement of the logic
-   optimise the placement by inserting repeater

#### Placement is run using the following command
The command to invoke the picorv32 design in the QFLOW manager is
```
Qflow gui &
```
![](https://raw.githubusercontent.com/chyavanphadke/Physical-Design_using_OpenLANE_and_Sky130/main/Images/lab3_Placement.png)

The layout of the picorv32 design is displayed using the following command
```
qflow display picorv32 &
```
The tkcon window and the magic window will open with the layout in it and the 'box' command gives the area estimation of the design.
![](https://raw.githubusercontent.com/chyavanphadke/Physical-Design_using_OpenLANE_and_Sky130/main/Images/lab3_layout.png)

## LAB Day 4
![](https://raw.githubusercontent.com/chyavanphadke/Physical-Design_using_OpenLANE_and_Sky130/main/Images/day4_pic2.png)

![](https://raw.githubusercontent.com/chyavanphadke/Physical-Design_using_OpenLANE_and_Sky130/main/Images/day4_pic3.png)

![](https://raw.githubusercontent.com/chyavanphadke/Physical-Design_using_OpenLANE_and_Sky130/main/Images/day4_pic5.png)

![](https://raw.githubusercontent.com/chyavanphadke/Physical-Design_using_OpenLANE_and_Sky130/main/Images/day4_pic6.png)
