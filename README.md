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



