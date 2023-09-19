# Good floorplan vs a Bad floorplan and introduction to Library Cells
## Chip Floorplannig considerations
# Semiconductor Design Overview

This repository provides a concise overview of key concepts in semiconductor design, focusing on core aspects such as die structure, utilization factors, pre-placed cells, decoupling capacitors, power planning, and pin placement.

## Die and Core

- **Die**: A semiconductor structure that houses the fundamental circuit, typically composed of a small semiconductor material.

- **Core**: A component within the die containing primary logic and functional elements.

Utilization Factor is a critical metric: `Utilization Factor = Area Occupied by the Netlist / Area of the Core (usually 50%-70%)`.

Aspect Ratio: `Aspect Ratio = Height / Width` (1 for square, others for rectangles).

## Pre-Placed Cells

Pre-placed cells include memories, clock gating cells, comparators, muxes, etc. These components are manually arranged on the chip in a process known as **floorplanning** before automated placement and routing. Automated tools handle the placement of remaining logical cells.

## Decoupling Capacitors

Large circuits with numerous resistors can lead to voltage drops, affecting the charging of logic capacitors. Decoupling capacitors, placed near combinational logic, act as a power supply during switching activities, ensuring reliable operation.

## Power Planning

Power planning is essential during floorplanning to minimize noise caused by voltage droop and ground bounce. Proper Power Distribution Networks (PDNs) with numerous power strap taps are crucial to maintain low resistance and noise levels.

## Pin Placement

Pin placement optimization is a vital part of floorplanning. Input pins are usually placed on the left, output pins on the right. Clock pins have larger sizes to minimize resistance and efficiently drive multiple cells. Placement blockages ensure logic isn't placed in pin areas.

# Floorplan
To view the placement type run_placement

![image](https://github.com/Pranav1723/pes_pd/assets/78376336/4789644c-d683-4e23-a328-651c183ac6f5)

To open the floor plan we need to first go to the required directory
- vsduser@vsdsquadron:~/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/18-09_17-17/results/floorplan$ 

Next we need to type this command:
- magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &

This is what we get after running the above command

![image](https://github.com/Pranav1723/pes_pd/assets/78376336/d5551e71-ea88-41e9-bf5a-45428ae6a56e)

![image](https://github.com/Pranav1723/pes_pd/assets/78376336/4f82a7ea-092c-4864-91f9-45be46a79ba5)

# Library binding and placement
## Bind the netlist with physical cells
In the domain of semiconductor design, our comprehensive library encompasses a wide array of cells, each characterized by distinct attributes, including size, configuration, flavor, and comprehensive timing, power, and delay specifications.
As you embark on your semiconductor design journey armed with your floorplan, netlist, and component representations from our library, the paramount objective is the meticulous placement of these components. The overarching goal is to uphold precise timing and, simultaneously, achieve a judicious distribution of these elements for an optimized semiconductor design.

## Optimization of placement
In the context of semiconductor design, it is imperative to address the issue of signal integrity, particularly concerning the considerable distance that some components may be situated from their respective inputs. As the length of interconnecting wires increases, so does the RC value, which poses a potential threat to signal quality.
To mitigate this concern, the deployment of repeaters, often implemented as a series of buffers, becomes necessary to counteract signal degradation. However, it's essential to acknowledge that this remedy does come at the cost of increased area utilization.
Assuming the ideal operation of all clock signals, a critical aspect of the design process entails conducting thorough timing analysis to evaluate the effectiveness of the current component placement. This analysis aids in determining whether the design meets the desired timing specifications, thus ensuring optimal performance.

## Placement
To view the placement type the command:
run_placement
![image](https://github.com/Pranav1723/pes_pd/assets/78376336/90ebf583-b71a-490c-93c9-f3158074ba6d)

Type the following command:
- magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def

![image](https://github.com/Pranav1723/pes_pd/assets/78376336/1a04896d-3229-426f-8c41-3df76c272302)

![image](https://github.com/Pranav1723/pes_pd/assets/78376336/b89e99e7-beb4-40ef-a901-f3bdd9db3c7e)

# Semiconductor Cell Design and Characterization Flow

This repository provides insights into the comprehensive process of semiconductor cell design and characterization, outlining key steps, inputs, and outputs involved in the process. Additionally, it offers details on timing characterization parameters.

## Cell Design Flow

**Inputs:**
- Process Design Kits (PDKs) containing DRC and LVS rules, SPICE models, libraries, and user-defined specifications.

**Design Steps:**
1. Circuit Design
2. Layout Design (Euler Path and Stick Diagram)
3. Characterization

**Outputs:**
- CDL (Circuit Description Language)
- GDSII
- LEF (Library Exchange Format)
- Extracted SPICE netlist (.cir)

## Characterization Flow

This section specifically addresses the characterization process for an inverter.

**Characterization Steps:**
1. Read the model files.
2. Read the extracted SPICE netlist.
3. Recognize the behavior of the buffer.
4. Attach the necessary power sources.
5. Apply the stimulus (input signal) to the circuit.
6. Read the sub-circuit of the inverter.
7. Provide the necessary output capacitances.
8. Specify the essential simulation commands.

## Timing Characterization

The following parameters are crucial for timing characterization:

- `slew_low_rise_thr`: 20%
- `slew_high_rise_thr`: 80%
- `slew_low_fall_thr`: 20%
- `slew_high_fall_thr`: 80%
- `in_rise_thr`: 50%
- `in_fall_thr`: 50%
- `out_rise_thr`: 50%
- `out_fall_thr`: 50%

Propagation Delay:
- `Propagation delay`: Time(`out_fall_thr`) - Time(`in_rise_thr`)

Transition Time:
- On Rise: Time(`slew_high_rise_thr`) - Time(`slew_low_rise_thr`)
- On Fall: Time(`slew_high_fall_thr`) - Time(`slew_low_fall_thr`)






