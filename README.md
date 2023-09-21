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


In percentage there is 10.8% of the total number of cells are Flops.


   file:///home/vsduser/Pictures/Screenshot%20from%202023-09-21%2009-43-26.png![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/231a6580-bca6-457c-9647-b570dd8e5f66)




DAY -2:



Chip Floor Planning Considerations

Utilization Factor and Aspect Ratio:
![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/fe3c8e2a-9a4d-4b77-aacf-52951ef8adb9)


    We consider a simple netlist with a Launch and Capture Flop. It also has an AND and OR gate.
    We then convert it into squares since we need appropriate dimensions


   
   ![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/a27297e9-ca7b-4e47-af2a-4b926a19933a)

Let us consider the areas of the gates and Flops as 1 sq unit

![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/4d2d0a2d-b200-4627-810f-3d54d3bb2502)



    Clubbing them together we get an area of 4 sq units

    The 'core' section of a chip is where the fundamental logic design is placed.

    The 'die' area contains the core and is a small semiconductor are on which the fundamental circuit is fabricated.



![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/536519bf-386f-476e-8c56-968a2dc2664f)
    




    Now we put the netlist in the 'core' area and check the utilization.
    Here

Utilization Factor = Area Occupied by the Netlist/Total Area of the Core

    As we can see here, there is 100% utilization and Utilization Factor = 1.
    In practical scenarios we don't go for such a high utilization factor.
    The 'Aspect Ratio = Height/Width = 1'.



Concept of Pre Placed Cells
   
   ![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/e3a9bdaa-a7c2-4ee0-b55d-147ffa838058)

![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/d22a02e7-c2f8-464a-bf23-e4c468dfa38b)
![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/ecc34335-34fe-4793-92c7-3da5168c6453)
We split the circuit into two parts, block 1 and block 2 as shown above



https://user-images.githubusercontent.com/142299140/267054839-6a468eae-b0f1-4eb7-ad74-0ba8ba42626d.png




    We extend the I/O pins and black box the boxes.
    Now we separate the boxes and the get their respective I/O ports.
    The use of doing this is that the users can use the blocks multiple times and form the required final circuit with ease.
    They only need to implement the design once and it can be reused.
    These kind of IPs have user defined locations and are placed in the chip before automated placement and routing takes place. These are called pre-placed cells.
Surrounding Pre-Placed Cells with Decoupling Capacitors



![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/e25ae4ca-1c86-4434-841a-4fa2e867592f)

    Huge capacitor filled with charge. The equivalent voltage across the capacitor is similar to what the power supply produces.
    We add the capacitor in parallel to the circuit.
    Everytime the circuit switches it draws current from the decoupling capacitor, whereas the outer network with the power supply and other componets is used to re-charge the capacitor

Pin Placement

    In pin placemnt step we use the HDL netlist to determine where a specific pin should be placed in the circuit.
    We join the common pins and try to keep the connections as effecient as possible.
    Pins are placed in the Die area.



Library Binding and Placement

Netlist Binding and Initial Place Design

![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/b27842a2-21a5-4616-9492-83959b334687)


    In real life, the logic gates and cells do not have shapes, but are present in the form of rectangles and squares.
    Hence they have dimensions to them and the space where they are placed must be utilized carefully
    The above picture shows an example of a library.
    Library consists of various kinds of cells which have different shapes and sizes, flavours and different timing information.

![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/037ee1d0-a6ae-4086-a3d2-a83fac601115)


    The components of the netlist are placed in the core area.
    They are placed according to the convenience of distance from the pins.
    When sending signal from FF1 to FF2, according to the circuit requirements, there has to be a very fast propogation of signals. Hence, they are placed very close and buffers are added since there is a small delay for the signal from the pin to reach FF1. The buffers maintain signal integrity.




LAB:

 file:///home/vsduser/Pictures/Screenshot%20from%202023-09-21%2009-54-06.png![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/716bcac4-a529-419f-9598-391e3fcacdd7)

file:///home/vsduser/Pictures/Screenshot%20from%202023-09-21%2009-54-23.png![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/d0c90a7f-d7f7-46df-bc18-4434f84db6e0)

file:///home/vsduser/Pictures/Screenshot%20from%202023-09-21%2009-55-06.png![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/fb107d6f-c6e0-4e3a-83d3-d4001da46358)

file:///home/vsduser/Pictures/Screenshot%20from%202023-09-21%2009-56-25.png![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/07a5f4ca-6a6b-4955-89a0-7655ba092727)

file:///home/vsduser/Pictures/Screenshot%20from%202023-09-21%2009-57-19.png![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/1a441ec1-3978-46cf-b363-b2e613432fe4)

file:///home/vsduser/Pictures/Screenshot%20from%202023-09-21%2009-58-17.png![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/41942d4b-250b-4f2a-931d-82576d8f75f0)
    
file:///home/vsduser/Pictures/Screenshot%20from%202023-09-21%2009-58-39.png![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/32e744fe-a22a-4742-b445-10f9d1c7f6de)

file:///home/vsduser/Pictures/Screenshot%20from%202023-09-21%2009-59-33.png![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/94051eb2-ef75-46b2-bd82-f78e6f4d08a0)

file:///home/vsduser/Pictures/Screenshot%20from%202023-09-21%2009-59-43.png![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/b95649fe-8a1e-44de-82b3-8c8914bda5a8)

file:///home/vsduser/Pictures/Screenshot%20from%202023-09-21%2010-00-16.png![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/5138529f-7706-41b9-b174-4a8679268094)





DAY -3:

inception of Layout and CMOS Fabrication Process:

SPICE Deck Creation for CMOS Inverter

    SPICE Deck is a netlist that has information on:
        component connectivity
        component values
        identifying the nodes
        giving a designation to the nodes

SPICE Simulation and Switching Threshold:

    The CMOS on the right side has a bigger size than the one on the left.
    These waveforms tell us that the CMOS is a very robust device. The characteristics of the CMOS are maintained across a variety of sizes.
    The arrow is pointing to the point where 'Vin = Vout'.

A Git Clone and some other Steps

    We need to perform a git clone here from a repository that we require, to do the future labs.
    We can type the following command

git clone https://github.com/nickson-jose/vsdstdcelldesign.git

    Now we need to copy the 'sky130A.tech' file into the directory we just cloned
    We can do this by using

cp sky130A.tech /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign

 Mask CMOS Process

    Selecting a Substrate - Selecting the appropriate substrate to synthsize the design on.
    Creating active reagion for transistors - Adding layers of SiO2(40nm), Si3N4(80nm) and photoresist(1um). On top of the photoresist we put a mask layer. Pass UV light and remove the mask. Resist is removed. LOCOS(Local Oxidation of Silicon) is performed. Si3N4 is etched.
    N-Well and P-Well formation - The next masks are used to create the source and drain regions of the MOSFETs. Boron is used to make P-Well using ion implantation. Phosphorus is used to create N-Well. Put the MOSFET in a Drive In furnace.
    Formation of Gate - Gate formation involves depositing a gate oxide, defining gate patterns using photolithography, depositing gate material, etching to create gates, doping the substrate and insulating the gates.
    Lightly Doped Drain Formation(LDD) - Lightly doped drain (LDD) formation involves implanting the drain and source regions of a MOSFET transistor with a lighter concentration of dopants to reduce hot electron effect and short channel effect and enhance device performance.
    Source and Drain Formation - Source and drain formation in a MOSFET transistor typically involves doping the silicon substrate with chemicals such as arsenic or phosphorous for n-type regions (source and drain) and boron for p-type regions (source and drain). High temperature annealing is performed.
    Steps to form Contacts and Interconnects(local) - Titanium is deposited with a process known as sputtering. Wafer is heated to about 650 - 700 C in an N2 ambient furnace for 60 seconds. TiSi2 contacts are formed. TiN is also formed used for local communication. TiN is etched using RCA cleaning.
    Higher Level Metal Formation - Forming contacts and interconnects locally involves depositing a dielectric material like silicon dioxide, patterning it using photolithography, etching contact holes, depositing a barrier metal (e.g., titanium or titanium nitride), filling with a conductor (e.g., aluminum or copper) using chemical vapor deposition (CVD), and then planarizing through chemical-mechanical polishing (CMP).


LAB-

file:///home/vsduser/Pictures/Screenshot%20from%202023-09-21%2011-42-32.png![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/1cbd24f3-5aa8-4fe2-912b-d6cc1a577689)

file:///home/vsduser/Pictures/Screenshot%20from%202023-09-21%2011-42-43.png![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/b3ab6d5f-5031-4e45-80f7-01144c20fb6a)

file:///home/vsduser/Pictures/Screenshot%20from%202023-09-21%2011-48-13.png![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/1bb0eb49-50b8-4bd3-af6e-54532ba38701)

file:///home/vsduser/Pictures/Screenshot%20from%202023-09-21%2011-48-49.png![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/eecdfa59-0c38-48bd-954a-738c8e766733)

file:///home/vsduser/Pictures/Screenshot%20from%202023-09-21%2011-48-49.png![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/d2a810c5-be94-439c-996f-474d3512dd65)
file:///home/vsduser/Pictures/Screenshot%20from%202023-09-21%2011-53-39.png![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/8a1cd47d-4e1b-4176-9e33-16d8c778313d)
file:///home/vsduser/Pictures/Screenshot%20from%202023-09-21%2012-10-37.png![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/a8c64bae-5fa7-4edb-b846-05444e273af0)


DAY -4:

Timing Modelling using Delay Tables:

LAB--:

file:///home/vsduser/Pictures/Screenshot%20from%202023-09-21%2012-11-36.png![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/38174407-f9ed-4cb2-afe0-3d88c97e3a9a)

file:///home/vsduser/Pictures/Screenshot%20from%202023-09-21%2012-11-49.png![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/a43831ab-2a37-4e55-9f3f-1dfa8c3781ab)

file:///home/vsduser/Pictures/Screenshot%20from%202023-09-21%2012-17-18.png![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/c7cc64b3-143b-491f-bf0e-4db247a645ac)
file:///home/vsduser/Pictures/Screenshot%20from%202023-09-21%2012-18-50.png![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/5e99af13-7788-4c76-b817-2d6367e9563d)
file:///home/vsduser/Pictures/Screenshot%20from%202023-09-21%2012-26-11.png![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/854eb03c-f91e-4b4a-b2b4-8ad5d12e5ebb)
file:///home/vsduser/Pictures/Screenshot%20from%202023-09-21%2012-26-13.png![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/1c694246-7fc5-4641-98c9-291811d380fe)
file:///home/vsduser/Pictures/Screenshot%20from%202023-09-21%2012-30-08.png![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/c502f584-364d-437d-a58a-d595f6980844)
file:///home/vsduser/Pictures/Screenshot%20from%202023-09-21%2012-30-08.png![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/d5c82d7c-fdfd-484f-9769-8212b2e6a079)
file:///home/vsduser/Pictures/Screenshot%20from%202023-09-21%2012-30-16.png![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/9a8b2ec2-28b2-4b3f-a3f8-e5f2a4b12c84)

file:///home/vsduser/Pictures/Screenshot%20from%202023-09-21%2012-30-48.png![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/8cd7f9a6-7873-486b-9e3b-760365e93781)
file:///home/vsduser/Pictures/Screenshot%20from%202023-09-21%2012-30-48.png![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/ff163830-bce6-44a0-98e6-03365de66435)
file:///home/vsduser/Pictures/Screenshot%20from%202023-09-21%2012-31-08.png![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/0cf7fee1-f312-43b1-863a-e0b3c5cdb8a4)


DAY -5:

Power Distribution Network :
After generating our clock tree network and verifying post routing STA checks we are ready to generate the power distribution network gen_pdn in OpenLANE:
The PDN feature within OpenLANE will create:

    Power ring global to the entire core
    Power halo local to any preplaced cells
    Power straps to bring power into the center of the chip
    Power rails for the standard cells
We see that there is a change in the DEF.


 Global and Detailed Routing

    OpenLANE uses TritonRoute as the routing engine for physical implementations of designs. Routing consists of two stages:
        Global Routing - Routing guides are generated for interconnects on our netlist defining what layers, and where on the chip each of the nets will be reputed.
        Detailed Routing - Metal traces are iteratively laid across the routing guides to physically implement the routing guides.
 DRC errors persist after routing the user has two options:

    Re-run routing with higher QoR settings.
    Manually fix DRC errors specific in tritonRoute.drc fil

    
    After routing has been completed interconnect parasitics can be extracted to perform sign-off post-route STA analysis. The parasitics are extracted into a SPEF file.
    The SPEF extractor is not included within OpenLANE as of now.



