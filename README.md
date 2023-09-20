DAY -1:


How to Talk to Computers

    First we look at the introduction to the RISC-V ISA(Instructiion Set Architecture). Supposing we need to execute a C program on a particular hardware. First the C-program is converted into Assembly Code( here for RISC-V processor). Then the assembly code is converted into binary. An RTL implements this code for the particular layout of the RISC-V processor and the output is visible.
    An application running on a system is usually written with the help of a high level language such as C,C++,Python etc. The code of these applications are compiled with the help of compilers running on a system software(OS). The compiler converts the high level code into assembly intructions for the particular processor. The assembler then converts the instructions into binary which is fed into the layout of the chip that processes every pattern of bits and the program is hence run.

SoC Design and OpenLANE

What is a PDK?

    PDK stands for Process Design Kit.
    It is a collection of files used to model a fabrication process for the EDA tools used to design an IC
        Process Design Rules.
        Device Models
        Digital Standard Cell Libraries
        I/O Libraries

A simplified RTL to GDSII Flow is :

    Synthesis -> Floor/Power Planning -> Placement -> Clock Tree Synthesis -> Routing -> Signoff

    Synthesis - Converts RTL to a ciruit, out of compomments from the standard cell library.

    Floor and Power Planning - Obejctive here is to plan the silicon area and create robust power distribution network to power the chip.
        Chip Floor Planning - Partition the chip die between different system building blocks and place the I/O pads.
        Macro Floor Planning - We define the macro dimensions, pin locations and rows are defined.
        Power Planning - The power distribution network is contructed.

    Placement - Placing the cells on the floorplan rows, aligned with the sites. There are 2 steps: Global and Detailed.

    Clock Tree Synthesis - To deliver the clock to all sequential elements.

    Routing - Implement the interconnect using the available metal layers.

    Sign Off - Perform physical verification such as DRC(Design Rule Check) and LVS(Layout vs Synthesis). Also perform STA(Static Timiing Analysis).

OpenLANE ASIC Flow
![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/8c4e84f4-0765-405d-82ad-665e96e59e8d)

Getting Familiar with the Open Source EDA Tools:

1. Design Preparation Step
   
file:///home/vsduser/Pictures/Screenshot%20from%202023-09-20%2013-47-46.png![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/58ff01f3-d38c-4886-85d1-41de2c767910)

file:///home/vsduser/Pictures/Screenshot%20from%202023-09-20%2013-49-52.png![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/ccb6f137-02b4-4563-9519-8ba35ad96da1)

file:///home/vsduser/Pictures/Screenshot%20from%202023-09-20%2013-50-17.png![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/22b9d872-5c51-4457-9600-1c56bf3fbbd6)

file:///home/vsduser/Pictures/Screenshot%20from%202023-09-20%2013-50-26.png![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/57e15b5d-a2c6-4fa9-9966-be5c7cb5f462)

file:///home/vsduser/Pictures/Screenshot%20from%202023-09-20%2013-51-02.png![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/0b00dace-1f86-4599-94f8-9aaf549a51a2)

file:///home/vsduser/Pictures/Screenshot%20from%202023-09-20%2013-51-37.png![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/a4ea9904-2b30-481d-80e2-80706b434057)


file:///home/vsduser/Pictures/Screenshot%20from%202023-09-20%2013-51-13.png![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/8402cf65-3fb2-497b-a8c6-0831a728aeac)


the commands used for the design  is are as follows:

1..  cd Desktop/work/tools/
2..  cd openlane_working_dir/openlane/
3..  ./flow.tcl -interactive
4..  package require openlane 0.9
5..  prep -design picorv32a
6..  run_synthesis




The flop ratio can be calculated by using:

No. of flops/No. of cells = 1613/14876 = 0.108


In percentage there is 10.8% of the total number of cells are Flops
   





    







   
   
