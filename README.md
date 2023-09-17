# pes_pd

# Advanced Physical Design using OPENLANE/SKY130 




<details><summary> DAY 1 </summary>



# Introduction to QFN -48 Package, chip, pads, core, die and IPs

* A QFN( Quad Flat No leads )  - 48 package

* PADS (peripheral devices ) act as a connection with which we can send signals inside and outside the chip.

* Core is the functional block of circuitry, it is where all the digital logic of our chip is placed.

* Die is the entire silicon wafer which contains the chip.

* The core consists of SOC, SRAM, ADC, DAC, PLL, SPI blocks.

* The SRAM, ADC, DAC, PLL are called as foundary IPs. A foundary is a factory which manufactures chips. It is also an Intelectual Property.

* The RISC V SOC and SPI blocks are called the macros. Basic difference between the macros and foundary IPs are that macros are purely digital circuits while Foundary IPs need some kind of unique design.


 ![padsdiecore](https://github.com/dishak14/pes_asic_class/assets/92496153/4f456f72-af50-449b-96e2-6b93ee4e0874)


![foundrymacros](https://github.com/dishak14/pes_asic_class/assets/92496153/7f142761-9192-4760-a1e7-4c008299476a)




# Introduction to RISC V

* RISC V is an Instruction Set Architecture.

* It is language of the computer i.e. we can interact with the computer using RISC V.

* C program --> RISC V assembly level code --> HDL --> RTL --> runs on layout.


![riscvss](https://github.com/dishak14/pes_asic_class/assets/92496153/70fa2db2-d2c9-4005-814d-73156995f273)


# From software application to Hardware 

* Application software enters into a block called system software.

* System software consists of various blocks:
 
1. Operatin system : which deals with the input/output operations, handles memory.
2. Compiler : converts the high level language into assembly level instructions.
3. Assembler : converts the assembly level instruction to binary which is known as the machine level code.

* After all this our application software will be ready to run on a hardware.

![astohardware](https://github.com/dishak14/pes_asic_class/assets/92496153/58705226-b6f7-4046-9d3d-eec3df602e0a)


# Simplified RTL2GDS flow


![rtl2gds](https://github.com/dishak14/pes_asic_class/assets/92496153/f62e4831-34f5-442d-be3b-0c2b4cd61c00)

* Designing a digital ASIC requires :
  1. RTL IPs (in HDL)
  2. EDA Tools
  3. PDK (Process desgin kits) data

 * PDK acts as an interface between FABs (manufacturing plants) and the designers.

 * Synthesis is converting of the HDL design is converted to its corresponding gate lebel netlist (RTL).

 * Floor Planning : it involves determining the placement of various functional blocks and components within the chip's layout to meet specific design goals and constraints.

 * Power Planning : focuses on efficiently delivering power to all components and functional blocks on the integrated circuit.
 
 * Macro Floor Planning :  It focuses on the high-level placement of large functional blocks, also known as macros, within the chip's layout. These macros often represent major functional units or intellectual property (IP) blocks that are pre-designed and optimized for specific functions.

 * Placement : refers to the process of determining the physical locations of various components, such as logic gates, memory cells, or functional blocks, within the chip's layout. Proper placement is essential for optimizing chip performance, power consumption, and overall functionality. There are two types of placements :
   1. Global Placement : also known as initial placement or coarse placement, is the first stage of placement in IC physical design. It focuses on determining the approximate locations of major components and functional blocks on the chip's layout without worrying about the detailed positions of individual cells.
   2. Detailed Placement : also known as fine placement, follows global placement and focuses on refining the placement of individual cells or components within the chip's layout. It involves determining the precise coordinates and positions of each cell.
  
 *  Clock Tree Synthesis is used for delivering clock to all the sequential elements of the IC. We need to have minimum skew in the clock ( as 0 skew is impossible to obtain) and it is usually in a tree form ( H, X etc).

 * Routing : it involves determining the paths for electrical connections (wires or traces) between the various components, such as transistors, gates, and memory cells, to establish the desired functionality of the electronic circuit. Routing is a crucial aspect of chip and PCB design, as it impacts the circuit's performance, signal integrity, and manufacturability. There are two types of routing :
   1. Global routing : Global routing is the first step in the routing process and focuses on finding high-level routes for interconnections. It determines which layers of the chip or PCB will be used for routing and estimates the approximate paths for connections. It is basically just a routing guide.
   2. Detailed routing :  Detailed routing follows global routing and involves specifying the exact placement of wires or traces, including their widths, spacings, and via locations. It considers detailed physical constraints and ensures compliance with design rules.
  
* Sign off : refers to the final approval or verification stage of the design process before it is sent for manufacturing. It is a critical step to ensure that the design meets all specifications, design rules, and requirements. DRC checking and LVS (Layout VS Scheme) is used for physical verification. Static Timing Analysis (STA) is done for timing verification.


# Introduction to openLANE and strive chipsets

* OpenLANE is an open-source digital ASIC design flow and toolchain that aims to automate the process of designing and manufacturing custom silicon chips.

* There is family of SoC's called as strive which is and Open PDK,Open EDA,Open RTL.

![image](https://github.com/dishak14/pes_pd/assets/92496153/5ae681d6-db0e-4aa8-99f2-e610ad0c221d)

* The main goal of openLANE is to produce clean GDSII flow with no human intervention and without any Layout VS Schematic ( LVS), DRC or timing voilations.

* There are essentially two modes of operations :
  1. Autonomous : also called as the push button flow which means we press a button and after a while a netlist is generated.
  2. Interactive : we can run the commands/ steps one by one.
 
 * openLANE also has design space exploration which is basically used to find the best flow configuration.

# openLANE Directory structure in detail


![dirstruct](https://github.com/dishak14/pes_pd/assets/92496153/559ee677-429c-4b46-b021-9063dc7416e0)



# Design Preparation Step 

``` docker ```

``` ./flow.tcl -interactive ``` 

``` package require openlane 0.9 ```

we need to do these 3 steps everytime.

![openlane](https://github.com/dishak14/pes_pd/assets/92496153/faa9e0a4-ea82-41c9-ab7f-b98ad40fa15e)


``` less config.tcl ```  this is setting of picorv32a file 

![configtcl](https://github.com/dishak14/pes_pd/assets/92496153/b81d6b3f-384f-4b0c-a549-0946065b5384)

``` prep -design picorv32a ```

![prepdesign](https://github.com/dishak14/pes_pd/assets/92496153/a5bd2ac8-6149-4fbb-9858-f1d1669b2a3f)


# Review files after design prep and run synthesis 

* We have a new folder called runs in picrov32a, inside this run folder another folder with today's date is created.


![todaysdate](https://github.com/dishak14/pes_pd/assets/92496153/c17c3540-884b-4f99-9df3-f04600aaafaa)

* Contents inside each of the file in run folder:


![each](https://github.com/dishak14/pes_pd/assets/92496153/402da3e5-ad56-4d58-91d9-ed233c8da7ba)

* ```run_synthesis``` for running the synthesis which will take some time


* Calculating flop ratio after running the synthesis :

  
![ffratio](https://github.com/dishak14/pes_pd/assets/92496153/6a9eeefe-b9fa-455a-a2d5-429f58b00c7b)

</details>

<details><summary> DAY 2 </summary>

# Utilization factor and aspect ratio

* The first step in physical design flow is to define the width and the height of the die and core.

* To determine the dimensions of a chip we need to focus on the dimensions of the logic gate, which is directly depended on the dimentions of the standard cells.

* Put all the standard cells side by side and find the area.

* Utilization factor = area occupied by netlist / total area of core

* If the utilization factor = 1, then the core is completely occupied. Practically, we need 0.5/0.6 utilization factor.

* Aspect ratio = height/width.

* If aspect ratio = 1, it signifies the chip is a square. If it is anything other than 1, chip is a rectangle.


# Concept of pre placed cells 

* The second step in the physical design process is the placement of pre placed cells.

* If we have a big circuit with a lot of logic gates, we cut the circuit into parts and implement both of them separately by extending the I/O(input/output) pins.

* Thes separated circuit blocks are made into a black box which act as different IPs or modules. We can reuse these modules multiple times.

* These black boxes are placed before automated placing/ routing and hence are called pre placed cells.

* The remaining cells are placed onto the chip without touching the already placed pre placed cells.


# De-Coupling Capacitors

* The third step in the Physical design process is to surround the pre placed cells with decoupling capacitors.

* When the input/output of any logic gate needs to change from 0 to 1 it needs to completely charge the intermediate capacitor. The voltage needed to charge the capacitor is drawn from a supply voltage.

* When it changes from 1 to 0, we need to discharge the intermediate capacitor which should be handled by the ground line of the power supply.

* When the charge is draw from the power supply to the logic gate circuit it is impossible to have the same voltage from the starting(Vdd) to the end destination(Vdd') of the wire due to multiple resistance, inductance etc present in the physical wire

* So the switching of logic 0 to 1 cant exceed Vdd'. And if Vdd' goes below the logic 1 the output of the circuit will not be detected as logic 1.

* We can solve this by adding a de coupling capacitor, parallel with the circuit.

* The voltage is stored in the de-coupling capacitor and it supplies the voltage to the logic circuit.

* Whenever there is a switching process, the de coupling capacitor loses its charge to the circuit and whenever there is no switching process it spends time replinishing its own charge

* All the pre placed cells need to be surrounded by de coupling capacitor which takes care of the local communication between these individual modules.


# Power Planning 

</details>

