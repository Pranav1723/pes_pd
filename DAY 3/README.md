# Designing of library cell using Magic layout and ngsspice characterisation

To effectively simulate and understand the behavior of standard cells, the creation of a SPICE deck is a crucial step for our CMOS inverter cell. The SPICE deck should encompass the following essential information:

- **Component Connectivity**: This section defines the interconnections of components within the inverter, including substrate taps that influence MOS transistor threshold voltages.

- **Component Values**: Specify the values of critical components in the inverter, such as PMOS and NMOS transistors, load capacitance, input gate voltage, and supply voltage.

- **Node Names**: Clearly define node names used in the inverter circuit, which are essential for creating an accurate SPICE netlist.

- **Switching Threshold**: This parameter represents the voltage at which the inverter transitions between different operational modes, typically defined at the intersection of Vin = Vout.

Creating a SPICE deck is essential for simulating the electrical behavior of standard cells, enabling us to predict their performance and identify potential issues. This process is fundamental to ensure the correct operation of the cell within the broader context of circuit design.

![image](https://github.com/Pranav1723/pes_pd/assets/78376336/80b7f91c-ff32-406b-9aef-3cd0f0b0c67a)


![image](https://github.com/Pranav1723/pes_pd/assets/78376336/9c1ec3fa-568f-496e-bbf9-25140c081a98)

# Inverter Layout using Magic

We need to first git clone the following repository and do so in the Home directory and to get there just type cd in your main terminal. This is the command to git clone this particular repository:

- git clone https://github.com/nickson-jose/vsdstdcelldesign.git

After git cloning this repository we need to go into the directory vsdstdcelldesign and to that just use this command:

- ~/Desktop/work/tools/openlane_working_dir/openlane$ cd vsdstdcelldesign

Now in this directory to view the layout just use the following command:

- magic -T sky130A.tech sky130_inv.mag &

This is what we get:

![image](https://github.com/Pranav1723/pes_pd/assets/78376336/6077d8e6-8835-4c6f-a247-8ca3461443a8)

![image](https://github.com/Pranav1723/pes_pd/assets/78376336/bee17af5-f1f5-438c-ac15-95b3b1c4acaa)

# How to explore the layout further in Magic

In the Magic software, you have the capability to navigate the layout by choosing specific layers and devices. You can employ the 's' key to iteratively select objects until you've pinpointed your intended object. Here's a step-by-step guide on how to achieve this:

To retrieve information pertaining to the selected area, adhere to these instructions:

1. Highlight a specific region within the layout.
2. Navigate to the console window and input the command 'what' to access details about the selected area.

![image](https://github.com/Pranav1723/pes_pd/assets/78376336/86ffe89b-acd4-42a9-9584-59b2cc332197)

![image](https://github.com/Pranav1723/pes_pd/assets/78376336/52495523-89eb-4528-b9e2-91ad279455a8)

# Extracting PEX to SPICE with Magic

To extract PEX (parasitic extraction) data to a SPICE netlist in Magic, use the appropriate commands within Magic. We use the command:

-  pwd

-  extract all

-  ext2spice cthresh 0 rthresh 0

-  ext2spice

![image](https://github.com/Pranav1723/pes_pd/assets/78376336/49d8b33b-8b63-426e-84ca-8d34524bd9e9)

To view the .spice and .ext files go to file explorer and go to the required folder to view the files

![image](https://github.com/Pranav1723/pes_pd/assets/78376336/cda6db82-8ab3-4e5f-96a6-c1ece52c0a8f)

This is the unmodified .spice file:

![image](https://github.com/Pranav1723/pes_pd/assets/78376336/e26ce1e1-e0c4-432f-aa2e-71656bea6b48)

This is the modified .spice file:

![image](https://github.com/Pranav1723/pes_pd/assets/78376336/1e947cdd-da7b-40b2-879f-95753ba82eef)

# Modified SPICE netlist

To run the SPICE netlist and analyze the results we must follow these steps and run the following commands:

- sudo apt install ngspice
- ngspice sky130_inv.spice
- plot y vs time a

This is what we get

![image](https://github.com/Pranav1723/pes_pd/assets/78376336/10fd22c8-a534-4a59-9408-eab46e80b1e3)


Results obtained from the simulation:

    Rise Transition: 0.0395 ns
    Fall Transition: 0.0282 ns







