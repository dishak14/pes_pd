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

* All the wires are a 16 bit bus. We cant put decoupling capacitors in between two large macros , this creates a problem of voltage drop when the distance between the power supply and the macro is large.

  
![image](https://github.com/dishak14/pes_pd/assets/92496153/451561ab-e76b-4b36-b2c4-5a0da6aad0f3)

* When we say that a particular bit in a 16 bit bus is logic 1, then the capacitor of that purticular bit is charged to Vdd and when we say its logic 0 , the capacitor is discharged to 0.
  
![image](https://github.com/dishak14/pes_pd/assets/92496153/49422a28-2022-45bc-a1bb-c1db7349cb35)

![image](https://github.com/dishak14/pes_pd/assets/92496153/392fe12e-ff5c-4070-a7d0-27bdedc03142)

* When this ground bump exceeds the noise margin, it becomes logic 1 which means we will get the wrong output.

  ![image](https://github.com/dishak14/pes_pd/assets/92496153/a816b54a-46d7-4237-a92a-ef70463e92dd)

* When the voltage droop falls below noise margin, it becomes a problem again.

* The solution to this problem is that we need to give multiple power supplies.

   ![image](https://github.com/dishak14/pes_pd/assets/92496153/efd8f7e7-e8a1-4784-b96b-67a8a4f141c7)

 * A power mesh is created.

   ![image](https://github.com/dishak14/pes_pd/assets/92496153/475d3d98-1116-49ae-ba24-7f13d7e242e9)


# LAB

``` /Desktop/work/tools/openlane_working_dir/openlane ```

``` docker```

``` ./flow.tcl -interactive ```

``` package require openlane 0.9 ```

```prep -design picorv32a ``` this creates a new runs file in ```Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a```

```run_synthesis ``` in openlane shell . This creates a new netlist in ```picorv32a/runs/synthesis```

```run_floorplan``` in openlane shell.

In ``` /Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/runs/17-09_16-02/results/floorplan``` , run the following command : ``` magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.floorplan.def &```


![layout](https://github.com/dishak14/pes_pd/assets/92496153/3f83afb9-50e5-4137-92f8-281039b1a9fc)


```run_placement``` in openlane shell.

``` cd ../placement ``` in the terminal.

```magic -T /home/vsduser/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/magic/sky130A.tech lef read ../../tmp/merged.lef def read picorv32a.placement.def & ```


![placement](https://github.com/dishak14/pes_pd/assets/92496153/a542ee78-2771-4d5c-ba35-3535d865720a)


# Cell Design and characterization flow


*INPUTS* ---> Process Design Kits (PDKs) ; DRC and LVS rules, SPICE models, library and user defined specs.

*DESIGN STEPS* ---> Circuit design, Layout design (Art of layout Euler's path and stick diagram), Extraction of parasitics, Characterization (timing, noise, power)

*OUTPUTS* ---> CDL (circuit description language), LEF, GDSII, extracted SPICE netlist (.cir), timing, noise and power .lib files


# General Timing characterization parameters

Timing defintion | Value
------------ | -------------
slew_low_rise_thr  | 20% value
slew_high_rise_thr |  80% value
slew_low_fall_thr | 20% value
slew_high_fall_thr | 80% value
in_rise_thr | 50% value
in_fall_thr | 50% value
out_rise_thr | 50% value
out_fall_thr | 50% value


delay =  time(out_fall_thr) - time(in_rise_thr)

Rise transition time = time(slew_high_rise_thr) - time (slew_low_rise_thr)

Fall transition time = time(slew_high_fall_thr) - time (slew_low_fall_thr)


</details>

<details><summary> DAY 3 </summary>

# Labs for CMOS inverter ngspice simulation

```git clone https://github.com/nickson-jose/vsdstdcelldesign.git```

The magic software we need is in ```/Desktop/work/tools/openlane_working_dirpdks/sky130A/libs.tech/magic/``` directory.

we copy it and paste it into the vsdstdcelldesign directory using ```cp sky130A.tech /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign```

Now we go to the vsdstdcelldesign directory and we can run magic without giving the absolute address.

```magic -T sky130A.tech sky130_inv.mag &```

![celldesign](https://github.com/dishak14/pes_pd/assets/92496153/28b872b9-e0a0-413d-8ee6-db6fd8ddca9e)

Use the following commands in tkcon window.


```extract all ```
```ext2spice cthresh 0 rethresh 0```
```ext2spice```



This creates a new file in vsdstadesigncell directory


![spice](https://github.com/dishak14/pes_pd/assets/92496153/c371a8e3-b8ca-447d-b963-c16077219be7)

![spice2](https://github.com/dishak14/pes_pd/assets/92496153/cbcfaa70-cfc3-4e99-a1c7-f5702ebb445b)


![now](https://github.com/dishak14/pes_pd/assets/92496153/9f8373ad-11e5-4359-a328-0d14fa1de1b4)

![Screenshot from 2023-09-19 06-05-49](https://github.com/dishak14/pes_pd/assets/92496153/4e2d653f-d5ba-437c-b91e-3490d8d9c9d3)

![inverter](https://github.com/dishak14/pes_pd/assets/92496153/15778405-6572-491e-b748-5daff6ac2d49)

 To download magic tool

```  wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz ```

```tar xfz drc_tests.tgz```

``` cd drc_tests```

``` ls -ltr ```

![drctest1](https://github.com/dishak14/pes_pd/assets/92496153/7b46f949-2cd8-4fc6-8aa8-5d9b2f143625)

In the same directory open the magic tool using

```magic -d XR ```

After the new magic window opens click on ```file -> open -> met1.mag ```

![met1mag](https://github.com/dishak14/pes_pd/assets/92496153/b57d65aa-20ee-4fc1-b8dc-45d0abc295bb)

![met1mag1](https://github.com/dishak14/pes_pd/assets/92496153/cde8f218-8b71-452a-8e51-d0224047549e)

type ```drc why ``` in tkcon window

![drcwhy1](https://github.com/dishak14/pes_pd/assets/92496153/2893010f-ca30-4ad3-81c2-28cd4cc5ca97)



</details>

<details><summary> DAY 4</summary>

# LAB

Converting grid info to track info

```cd Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/openlane/sky130_fd_sc_hd/```

``` less track.info```

![tracksinfo](https://github.com/dishak14/pes_pd/assets/92496153/5955244c-5b43-4382-b6e7-61209ded978c)

Track info is used during routing stage.

type ```grid 0.46um 0.34um 0.23um 0.17um``` for convergence of grid and track.

## Standard cell LEF generation

to make an .lef file type this in the tckon terminal

``` lef write ```

then come back to the terminal and type 


```less sky130_vsdinv.lef ```

![lefgen](https://github.com/dishak14/pes_pd/assets/92496153/1f0c92cb-8fe9-4ba4-858c-46fa444b6c15)

``` cp sky130_vsdinv.lef /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src ```

```cp sky130_fd_sc_hd__* //home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/designs/picorv32a/src```

![src](https://github.com/dishak14/pes_pd/assets/92496153/21ef80f2-460a-4432-bd40-e50f3c86b00a)

```gedit config.tcl```

![geditconfig](https://github.com/dishak14/pes_pd/assets/92496153/460ed2f1-d5c0-4963-9f15-5eeb4359491b)

![idklol](https://github.com/dishak14/pes_pd/assets/92496153/8bf75ed6-b684-46f6-acfe-55e37e66357f)



# Timing analysis using OpenSTA

create ``` pre_sta.conf ``` in openlane directory 

![preconf](https://github.com/dishak14/pes_pd/assets/92496153/50072f32-ed76-41e1-b235-1f8bcd9010ba)

create ```my_base.sdc``` in openlane/designs/picorv32a/src/ directory.

![mybase](https://github.com/dishak14/pes_pd/assets/92496153/3433683e-e788-4156-b8a5-0afaaf7705fd)

we get the following results after doing ```sta pre_sta.conf```

![cooo](https://github.com/dishak14/pes_pd/assets/92496153/49efb127-bebc-490f-8003-6e9402269104)
</details>

<details> <summary> DAY5
</summary>
 
OpenLANE uses the TritonRoute tool for routing. There are 2 stages of routing:

Global routing: Routing region is divided into rectangle grids which are represented as course 3D routes (Fastroute tool)
Detailed routing: Finer grids and routing guides used to implement physical wiring (TritonRoute tool)
Features of TritonRoute:

Honouring pre-processed route guides
Assumes that each net satisfies inter guide connectivity
Uses MILP based panel routing scheme
Intra-layer parallel and inter-layer sequential routing framework

</details>









































