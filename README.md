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


