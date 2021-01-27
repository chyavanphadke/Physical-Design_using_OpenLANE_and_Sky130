
# Advanced-Physical-Design-using-OpenLANE-and-Sky130
Workshop on: Advanced Physical Design using OpenLANE Sky130

Openlane is a package of tools that consists of many tools needed for the overall process from Design to GDSII
location of the Openlane is in openlane_build_script/work/tools/openlane_working_dir/openlane

The basic idea of Openlane is to have a complete flow

- [About The Project](#Day-1)
- [Opensource Tools used for RTL to GDSII](#Day-1)
- [Day 2](#Day-2)
- [Day 3](#Day-3)
- [Day 4](#Day-4)
- [Day 5](#Day-5)

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
## Day-1
## Day-2
## Day-3
## Day-4
## Day-5
