




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
   Qflow - It is provided to ease the total design process for the complete flow of RTL to GDSII 
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
-   abc : Performs technology mapping to standard cells described in the PDK. We can adjust synthesis techniques using different integrated abc scripts to get desired results
-   OpenSTA : Performs static timing analysis on the resulting netlist to generate timing reports
-   Fault : Scan-chain insertion used for testing post-fabrication. Supports ATPG and test patterns compaction

#### 2.   Floorplan and PDN
-   Init_fp - Defines the core area for the macro as well as the rows (used for placement) and the tracks (used for routing)
-   Ioplacer - Places the macro input and output ports
-   PDN - Generates the power distribution network
-   Tap cell - Inserts well tap and decap cells in the floorplan
-   Placement – Placement is done in two steps, one with global placement in which we place the designs across the chip, but they will not be legal placement with some standard cells overlapping each other, to fix this we perform a detailed placement which legalizes the design and ensures they fit in the standard cell rows
-   RePLace - Performs global placement
-   Resizer - Performs optional optimizations on the design
-   OpenPhySyn - Performs timing optimizations on the design
-   OpenDP - Performs detailed placement to legalize the globally placed components

#### 3. CTS
-   TritonCTS - Synthesizes the clock distribution network

#### 4.   Routing
-   FastRoute - Performs global routing to generate a guide file for the detailed router
-   TritonRoute - Performs detailed routing from global routing guides
-   SPEF-Extractor - Performs SPEF extraction that includes parasitic information

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

Adter running the prep command wait for the design preparation to complete, it might take some time based on the configuration and the design file.

![](https://raw.githubusercontent.com/chyavanphadke/Physical-Design_using_OpenLANE_and_Sky130/main/Images/preparation%20completed.png)

wait for the "[INFO]: Preparation completed" confirmation. The next step is to start the synthesis. The following command is used to start the synthesis.
```
run_synthesis
```
Synthesis takes some time based on the size and complexity of the design. Completion of the synthesis is displayed by "[INFO]: Synthesis is completed" message.
![](https://raw.githubusercontent.com/chyavanphadke/Physical-Design_using_OpenLANE_and_Sky130/main/Images/synthesis%20completed.png)
## LAB Day 3
### Tools Installed 
- Static Timing Analysis tool successfully in place.
![](https://raw.githubusercontent.com/chyavanphadke/Physical-Design_using_OpenLANE_and_Sky130/main/Images/staSuccess.png)

- Yosys installed successfully
![](https://raw.githubusercontent.com/chyavanphadke/Physical-Design_using_OpenLANE_and_Sky130/main/Images/yosysSuccess.png)

- OpenTimer installed and working check

![](https://raw.githubusercontent.com/chyavanphadke/Physical-Design_using_OpenLANE_and_Sky130/main/Images/opentimerSuccess.png)

- GrayWolf tool inplace
![](https://raw.githubusercontent.com/chyavanphadke/Physical-Design_using_OpenLANE_and_Sky130/main/Images/graywolfSuccess.png)

- Qflow GUI
![](https://raw.githubusercontent.com/chyavanphadke/Physical-Design_using_OpenLANE_and_Sky130/main/Images/qflowSuccess.png) 

## LAB Day 3
#### What is Slack
-   It is the difference between the desired arrival times and the actual arrival time for a signal.
-   Slack time determines [for a timing path], if the design is working at the desired frequency.
-   Positive Slack indicates that the design is meeting the timing and still it can be improved.
-   Zero slack means that the design is critically working at the desired frequency.
-   Negative slack means, the design has not achieved the specified timings at the specified frequency.
-   Slack has to be positive always and negative slack indicates a violation in timing.

Positive slack is required for the design to work properly. Here is taken example, we have a slack of 1.27. So slack requirements are fulfilled.

### IC Planning
 IC Planning or also called Chip planning is the crucial step in Physical design flow. The important aspects like the area of the core, utilization factor, Powe planning, and cell placement are taken care of in this stage.

### Height and width of the core
-   Core is the section of the chip where the fundamental logic is placed
-   Die consists of a core and it is a semiconductor material on which the circuit is fabricated.
-   Utilisation factor is the ratio of Area occupied by netlist and the Total Area of the core. The 100% utilization refers to the Utilisation factor being 1. However, in the practical scenarios, only 50-60% utilization is considered to provide a place for other routing and filler cells, etc.
-   Aspect Ratio is the ratio o the height and width of the core. The Aspect ratio of 1 refers to a square chip.

### Pre-placed Cells
-   Pre-placed cells are those which are implemented once and instantiated many times. The arrangement of these IPs in the chip is referred to as Floorplanning.
-   These IPs/blocks have user-defined locations and hence are placed in the chip before the automated placement and routing.

### Decoupling Capacitors
-   Large complex circuits will have a high amount of switching current.
-   Noise mArgin specs define the logic'0' and logic '1' valid voltages and undefined regions.
-   The high switching current demand can be solved by the addition of decoupling capacitors in parallel with the circuit.

### Power Planning
-   The power planning should be done in a way that the driver and load be close to each other in the 'L' sense.
-   The improper power planning i.e., single power and Ground lines can lead to 'Ground bounce' and 'Voltage Drop'.
-   So the plan should have multiple 'VDD', 'VSS' lines running through the circuit.

### Pin Placement
-   The connectivity of the chip to the outside world.
-   The placement of the pins is dependent on the position (near/far) but not on the ordering.
-   The clock ports are found to be bigger than the general data ports to necessitate less resistance.
- 
### Placement and Routing
-   Bind the netlist with the physical cells i.e., library cells
-   Placement of the logic
- optimize the placement by inserting a repeater

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

Static timing analysis and concepts of clock tree synthesis.
First timing analysis is done using delay tables, then using ideal clocks, then using real clocks.

Finding the Switching threshold
```
cd
cd ngspice_labs
ngspice inv.spice
run
setplot dc1
```
![](https://raw.githubusercontent.com/chyavanphadke/Physical-Design_using_OpenLANE_and_Sky130/main/Images/day4_pic3.png)

The expanded plot of the above graph
![](https://raw.githubusercontent.com/chyavanphadke/Physical-Design_using_OpenLANE_and_Sky130/main/Images/day4_pic6.png)

Layout view of s small area. Polysilicon strips are highlighted with nmos and pmos
![](https://raw.githubusercontent.com/chyavanphadke/Physical-Design_using_OpenLANE_and_Sky130/main/Images/day4_pic2.png)

### Timing Modeling
Timing modeling is performed with the use of delay tables. Depending upon the input slew and output load we can get the delay for the buffer or any other gate.

To model timing for clock tree structures, is necessary to take care with:
-   at every level, each node drive the same load;
-   identical buffers need to be used at the same level.

### Timing analysis (with ideal clock)
If T is the clock period and td is the combinational logic delay, then T>td.
If the setup time for the capture flipflop is S, the T > td + S. Otherwise there will be a setup time violation.

If the jitter is considered then T > td + S + SU. Otherwise, there will be a violation.
Jitter is a temporary timing problem that can be removed if the semiconductor temperature and power noise are maintained correctly.

### Clock Tree Synthesis (CTS)
The main reason for performing CTS is to remove clock skew. Ideally, it should be 0.
Some techniques are used to achieve a good CTS

-   H-Tree technique (midpoints to derive clock)
-   Using buffers (since H-Tree do not avoid long paths, we need to put buffers)
-   Net shielding (to avoid crosstalk/glitches)


## LAB Day 5
On day 5 the main concentration was on Routing and finishing up the Design.

### Adding grids and Routing

1.  Routing involves generating metal wires to connect the pins of the same signal while obeying manufacturing design rules.
2.  Before routing is performed on the design, cell placement has to be carried out wherein the cells used in the design are placed.
3.  The connections between the pins of the cells about the same signal need to be made. At the time of placement, there are only logical connections between these pins.
4.  The physical connections are made by routing. More generally speaking, routing is to locate a set of wires in the routing space to connect all the nets in the netlist taking into consideration routing channels’ capacities, wire widths, and crossings, etc.
5.  The objective of routing is to minimize total wire length and number of vias and that each net meets its timing budget. The tools that perform routing are termed routers.
6.  You typically provide them with a placed netlist along with a list of timing critical nets. These tools, in turn, provide you with the geometry of all the nets in the design.

The Maze Algorithm is also known as Lee´s Algorithm
-   This algorithm creates a routing grid
-   It finds the best route from a source to a target
-   It is an automated process


### DRC (Design Rule Check)
DRC is a major step during physical verification signoff on the design, which also involves LVS (layout versus schematic) checks, XOR checks, ERC (electrical rule check), and antenna checks. The importance of design rules and DRC is greatest for ICs, which have micro- or nano-scale geometries; for advanced processes, some fabs also insist upon the use of more restricted rules to improve yield.

#### Types of DRCs
-   Minimum width and spacing for metal
-   Minimum width and spacing for via
-   Fat wire Via keep out Enclosure
-   End of Line spacing
-   Minimum area
-   Over Max stack level
-   Wide metal jog
-   Misaligned Via wire
-   Different net spacing
-   Special notch spacing
-   Shorts violation
-   Different net Via cut spacing
-   Less than min edge length


### Parasitics Extraction
Parasitic extraction is the calculation of the parasitic effects in both the designed devices and the required wiring interconnects of an electronic circuit: parasitic capacitances, parasitic resistances, and parasitic inductances, commonly called parasitic devices, parasitic components, or simply parasitics.
