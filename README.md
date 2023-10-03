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

 Placer

    In order to change the distance between the IO pins:

     % set ::env(FP_IO_MODE) 2 % run_floorplan
 
We can see that they are no more equidistant.


SPICE Deck Creation for CMOS Inverter
SPICE Simulation Lab for CMOS Inverter

    Simulation steps

    cd <folder where the .cir file is present>
    source CMOS_INVERTER.cir
    run
    setplot
    dc1
    display
    plot out vs in

    ![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/30714342-dfc2-411f-88f6-7efe48060a5e)

    
    The output should be symmetric ie., the threshold voltage should be at vdd/2.
    If it isnt, try to increase the PMOS width and run the simulation again.


Switching Threshold Vm

    CMOS as a circuit itself is a very Robust device.
    Switching threshold defines the robustness of CMOS.
    Vm is the point where Vin=Vout.

 Lab Steps to Gitclone vsdstdcelldesign

    git clone https://github.com/nickson-jose/vsdstdcelldesign.git
     cp sky130A.tech /home/vsduser/Desktop/work/tools/openlane_working_dir/openlane/vsdstdcelldesign


     
Create Active Regions

    Fabrication of CMOS is a 16 Mask process.

Selecting the Substrate

    We go for a p-type substrate with
        resistivity around : 5-50 ohm
        doping level : 10^15 cm^-3
        orientation : 100

Creating Active region for transistors

    Grow a layer of SiO2(~40nm) on Psub.
    Deposit a layer of ~80nm Si3N4 on SiO2.
    Deposit 1um layer of photoresist(used to define regions).
    Photolithography.
    Etch out Si3N4 and SiO2 using a suitable solvent.
    Place the obtained structure in oxidation furnace due to which field oxide is grown.This process is called LOCOS ( Local oxidation of silicon).
    Etch out Si3N4 using hot phosphoric acid.


Formation of n-well and p-well

    Deposit a layer of photoresist.
    Apply mask to cover NMOS.
    Expose to UV light, wash away the area which is exposed and remove mask.
    Deposit Boron using ion implementation at an energy of 200keV.
    Repeat the same steps for other half using phosphorous at an energy of 400keV.
    Wells have been created but the depth is low, hence subject it to high temperature furnace which increases the well depth.

 
Formation of Gate Terminal

    Deposit a layer of photoresist.
    Apply mask to cover NMOS.
    Expose to UV light, wash away the area which is exposed and remove mask.
    Deposit Boron using ion implementation at an energy of 200keV cause we need boron at the surface.
    Repeat the same steps for other half using arsenic.
    Original oxide etched/stripped using hydroflouric solution.
    Then re-grown again to give high quality oxide (~10nm thin).
    Deposit ~0.4um polysilicon layer.
    Dope N-type (phosphorous/ arsenic) ion implants for low gate resistance.
    Deposit a layer of photoresist and repeat the same steps till removing the mask.

 Lightly Doped Drain Formation

    The doping profile near n-well is P+, P-, N.
    Near p-well is N+, N-, P.
    2 reasons to do this:
        hot electron effect
        short cahnnel effect
    On the surface of SiO2, near N-well, deposit a layer of photoresist, and mask it.
    Expose to UV light, wash away the area which is exposed and remove mask.
    Apply phosphorous to form N- implant on p-well.
    Similarly do it on the other half, but apply boron to form P- implant on n-well.
    LDD needs to be protected, hence deposit 0.1um thick SiO2 on full structure and etch out using plasma anisotropic etching.
    This results in the formation of side-wall spacers.


    
Local Interconnect Formation

    Etch thin SiO2 oxide in HF solution.
    Deposit Titanium of wafer surface using sputtering.
    Wafer heated at 650-700 degree celsius in N2 ambient for 60 sec.
    Results in low resistant TiSi2.
    At the other places, TiN is formed which is used only for local communication.
    TiN is etched off using RCA cleaning.



    
Source and Drain Formation

    On the surface of SiO2, near N-well, deposit a layer of photoresist, and mask it.
    Expose to UV light, wash away the area which is exposed and remove mask.
    Deposit arsenic at 75KeV that forms an N+ implant on Pwell.
    Similarly do it on the other half, but apply boron to form P+ implant on n-well.
    Subject it to high temperature furnace that results in required thickness of N+,P+,N-,P- implants.

Local Interconnect Formation
Higher Level Metal Formation
Lab Introduction to Sky130 Basic Layers Layout and LEF using Inverter
Lab Steps to Create std cell Layout and Extract SPICE Netlist 


  

 Higher Level Metal Formation

    Deposit 1um of SiO2 with phosphorous or boron (known as phosphoborosilicate glass) on wafer surface.
    Use CMP (chemical mechanical polishing) technique for planarizing wafer surface.
    TiN and blanket Tungsten layers are deposited and subjected to CMP.
    An aluminum (Al) layer is added and subjected to photolithography and CMP.
    Deposit a layer of Si3N4 that acts as dielectric to protect the chip.





ab Introduction to Sky130 Basic Layers Layout and LEF using Inverter

    magic -T sky130A.tech sky130_inv.mag &


![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/f0e67171-96db-41cd-813c-611d062391aa)


![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/f6154bd5-10dd-4144-9330-b0eb978489ec)


ab Steps to Create std cell Layout and Extract SPICE Netlist

    DRC errors in magic will be highlighted with white dotted lines.

![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/bd7fe057-45e1-41a8-8d7f-1b273860a3ed)



    To identify DRC errors select DRC find next error.
    It will be displayed on the tkcon window.

![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/cc358aea-5889-42cb-885f-d880dd4a0bcd)




![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/489f2579-5ec9-49a9-9300-6661b29aec48)


Extracting to SPICE Command

    extract all
    ext2spice cthresh 0 rthresh 0
    ext2spice

cthresh and rthresh are used to extract all parasatic capacitances.


We can see that the spice file is created in the folder.


![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/b45470f3-c4a7-497e-b278-f4fd846e36ad)

Spice File


![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/fb136d1c-bf58-47a8-9a23-dd87a97de41a)










 Lab Steps to Create Final SPICE Deck using Sky130 Tech

    Grid size.
![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/c42e8e99-eec6-4139-ba22-c95b09a0b71f)


We modified the spice file.

![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/203a54d0-4866-4129-a7e7-adeac810ad14)

ngspice sky130_inv.spice
plot y vs time a


![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/b845b52e-965a-4feb-88fb-b759a48b2b5a)


ntroduction to Magic Options and DRC rules
+ For reference : http://opencircuitdesign.com/magic/

Magic

    Magic is a venerable VLSI layout tool, written in the 1980's at Berkeley by John Ousterhout, now famous primarily for writing the scripting interpreter language Tcl.
    Due largely in part to its liberal Berkeley open-source license, magic has remained popular with universities and small companies.
    The open-source license has allowed VLSI engineers with a bent toward programming to implement clever ideas and help magic stay abreast of fabrication technology.
    However, it is the well thought-out core algorithms which lend to magic the greatest part of its popularity.
    Magic is widely cited as being the easiest tool to use for circuit layout, even for people who ultimately rely on commercial tools for their product design flow.

DRC rules

    DRC (Design Rule Check) rules are a set of guidelines and constraints used in the field of semiconductor and integrated circuit (IC) design to ensure that the physical layout of a chip or circuit adheres to the manufacturing process's design rules.
    These rules are essential for maintaining manufacturability and ensuring that the final ICs can be fabricated without defects.
    The design rules used by Magic's design rule checker come entirely from the technology file.




Introdcution to Sky130 PDKs and Steps to Download Labs

Sky130 PDK

    SKY130 is a mature 180nm-130nm hybrid technology developed by Cypress Semiconductor that has been used for many production parts.

    SKY130 is now available as a foundry technology through SkyWater Technology Foundry.

    wget http://opencircuitdesign.com/open_pdks/archive/drc_tests.tgz

 Lab Introduction to Magic and Steps to Load Sky130 Tech-Rules

    To open Magic
        magic -d XR

    Go to files then open met3.mag file.
![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/3a78bb3a-8643-446b-b8e5-a648e5a85a35)


    To check which DRC rule is being violated select area.
    Type drc why in tkcon.

![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/c13a2904-86a4-4c77-bdc9-2bfca2dbac94)



    To add contact cuts add met3 contact by selecting area and clicking on m3contact using middle mouse button.
    Type cif see VIA2 in tkcon prompt.


![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/be1b3500-fa52-43b0-ad0d-8f3f8c3f1efe)


 Lab Exercise to fix poly.9 error in Sky130 Tech File

    Type load poly in the tkon prompt.

![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/c1384648-d676-486c-820f-9810928d86bd)

The error is:


![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/4faacb8c-dce5-44ad-9fb4-5cd1968ca4f7)



To fix the error open the sky130A.tech file using a editor and search for poly.9 and make the changes.


![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/ed61bc68-d5f9-48bd-8afb-57f7c974e333)


![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/854ab648-4ced-44fa-a84f-0beba3b3f1ea)


    Now load the sky130A.tech file tech load sky130A.tech.
    Type the command drc check.
    We can see that the error is fixed.



![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/a4b39e79-2509-45c1-a0cb-a1c2d768e7c5)




 Lab Challenge Exercise to Describe DRC Error as Geometrical Construct

    Open the nwell.mag file in magic.
    Select the nwell.6
    Type the following commands in tkon prompt:
        cif ostyle drc
        cif see dnwell_shrink
        cif see dnwell_missing
![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/3123c9b1-d434-4385-893e-adfe8891fe89)


To find missing or incorrect rules and fix them.


![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/5018ee9d-4bd8-47aa-a432-dfa95d54bb83)




    Error is :

![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/16136445-9642-4741-9c7c-eeba967f5776)


To fix the error open the sky130A.tech file using a editor.

![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/26bbb654-dbe8-4751-8d87-5fd1576fb925)



![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/1d0428cf-8f26-42d1-8337-f7445cb514a2)




    Now load the sky130A.tech file tech load sky130A.tech.
    Type the command drc check for both normal and drc fast.


![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/71626c3a-ef9a-4e23-8d7e-15b20fcec5c0)






![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/41916c00-64df-47e0-9419-0d8d2828aa23)













DAY -4:

 Lab steps to convert Grid info into Track info

     ~/Desktop/work/tools/openlane_working_dir/pdks/sky130A/libs.tech/openlane/sky130fd_sc_hd/tracks.info
    less tracks.info


![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/56466d3e-b179-4bb8-90c2-67300ba5d3cc)








    The 'tracks.info' file is used during the routing stage.

    Routes are the metal traces.

    Since the PNR is an automated flow, we need to specify where all we want the routes to go.

    Now we converge the grid definition in the layout to track definition.

    
    The next requirement is that the width of the cell should be the odd multiple of xpitch which is '0.46' as seen in the 'tracks.info' file.
    As we can see it encloses two full boxes and two halves of one box, totally making three boxes as indicated by the white line.

 Lab steps to convert Magic Layout to Std Cell LEF

    In the tkcon window, type save sky130_vsdinv.mag.
    This is to make our own .mag file.
    lef write to make .lef file
![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/2b738ab0-e88d-4bab-b7ab-f6dc7a55b401)


less sky130_vsdinv.lef


![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/038a5aad-9987-4282-8101-52b3f60afdb5)

 Introduction to Timing Libs and Steps to include New cell in Synthesis

    We copy the lef file and the libraries.


![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/fc9bbffa-608a-45ec-acbb-d63d9919bc2e)




    Next we modify the 'config.tcl' file in the picorv32a folder.

    Open the OpenLANE interactive window and retrieve the 0.9 package.

    prep -design picorv32a -tag 14-09_10-42 -overwrite
    set lefs [glob $::env(DESIGN_DIR)/src/*.lef]
    add_lefs -src $lefs 
    run_synthesis


![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/d4d6d967-da4f-4b23-a51b-f9a646890920)


![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/c6e8f889-780f-41f7-b899-936e0e64229a)





 Configure OpenSTA for Post-Synth Timing Analysis

    We must create two files.
    The first one must be in the openlane directory
    This file is known as the 'pre_sta.conf' file.




    The second is the my_base.sdc file.
    This should be in the 'src/sky130' directory under the picorv32a directory.







    To run the timing analysis we type
    sta pre_sta.conf




There is a slack violation.


 Optimise synthesis

    Setting MAX_FANOUT value to 4 reduces the slack violation.
    set ::env(SYNTH_MAX_FANOUT) 4
    Then run_synthesis

Since we have synthesised the core using our vsdinv cell too and as it got successfully synthesized, it should be visible in layout after run_placement stage which is followed after run_floorplan stage.




 CTS

    To run CTS we need to type the command.
    run_cts
    New .v is created.




     Lab steps to analyse Timing with Real CLocks

    openroad
    read_lef /openLANE_flow/designs/picorv32a/runs/14-09_10-42/tmp/merged.lef
    read_def /openLANE_flow/designs/picorv32a/runs/14-09_10-42/results/cts/picorv32a.cts.def
    write_db pico_cts.db
    read_db pico_cts.db
    read_verilog /openLANE_flow/designs/picorv32a/runs/14-09_10-42/results/synthesis/picorv32a.synthesis_cts.v
    read_liberty -max $::env(LIB_SLOWEST)
    read_liberty -max $::env(LIB_FASTEST)
    read_sdc /openLANE_flow/designs/picorv32a/src/my_base.sdc









    set_propagated_clock [all_clocks]
    report_checks -path_delay min_max -format full_clock_expanded -digits 4



We perform it again for a more accurate result










 Lab steps to Observe Setup and Hold Timing

    report_clock_skew -hold



report_clock_skew -setup






DAY -5:



Maze routing

    Maze routing is a method used in electronic design automation (EDA) and integrated circuit (IC) design to determine efficient paths for interconnecting various components, such as logic gates, on a chip's layout. The goal is to find a path through a maze-like grid of obstacles while optimizing for factors like wire length, signal delay, and area utilization.

    Lee's algorithm, also known as Lee's breadth-first search (BFS) algorithm, is a graph traversal and pathfinding algorithm that is commonly used in maze routing, maze solving, and other grid-based problems. Named after its creator, C. Y. Lee, the algorithm is particularly useful for finding the shortest path between two points in a grid while exploring the grid layer by layer.


DRC

Lambda rules are process-specific design rules used in semiconductor manufacturing to ensure that integrated circuit (IC) layouts adhere to the capabilities and constraints of a particular semiconductor process. These rules are expressed in terms of lambda (λ), a normalized unit of measurement relative to the process technology. Lambda rules can vary between semiconductor foundries and process nodes, but they typically cover various aspects of IC design. Here's a list of common lambda rules and design considerations:

    Minimum Feature Size: Specifies the minimum allowed width and spacing for features such as transistors, metal tracks, and vias, often expressed as multiples of λ.
    Aspect Ratio: Defines the acceptable aspect ratio (width-to-height ratio) for rectangular structures, ensuring manufacturability.
    Metal Layer Constraints: Specifies minimum metal track widths, metal-to-metal spacings, and via sizes on metal layers.
    Poly Pitch: Defines the minimum pitch (spacing between features) for the poly-silicon (poly) layer, which affects the size of transistors and gates.
    Active Area Constraints: Specifies minimum active area dimensions, ensuring that transistors meet process requirements.
    Well and Substrate Taps: Covers the placement and size of well and substrate taps for connecting to power and ground planes.
    Gate Length: Specifies the minimum gate length for transistors, affecting their performance characteristics.
    Contact and Via Rules: Defines the minimum size and spacing of contacts and vias used to connect different layers in the IC.
    Local Interconnects: Provides rules for local interconnects, which are used for routing within a cell or macro.
    Minimum Metal to Active Spacing: Sets the minimum separation between metal tracks and active areas.
    Minimum Metal to Contact Spacing: Specifies the minimum distance between metal tracks and contacts.
    Edge Exclusion Zones: Defines exclusion zones near the chip's edge, where certain design elements are not allowed.
    Density Rules: Enforces limits on the density of features in different regions of the chip to ensure proper manufacturing and avoid over-congestion.
    Well Proximity Rules: Governs the proximity of different well types (e.g., n-well and p-well) to prevent undesirable interactions.
    Metal Layer Ordering: Specifies the order in which metal layers should be used in the design hierarchy.
    Metal Filling: Addresses requirements for metal fill patterns to ensure planarity and manufacturability.
    Antenna Rules: Addresses the issue of charge buildup (antenna effect) during manufacturing, providing guidelines for mitigating this effect.
    Variation-Aware Rules: Accounts for process variations, statistical timing, and other variations in critical design rules.
    Electromigration Constraints: Specifies limits on current densities to prevent electromigration issues in metal tracks.
    Supply Voltage Constraints: Sets design guidelines for supply voltage levels and power distribution.

 Power Distribution Network

    After generating our clock tree network and verifying post routing STA checks we are ready to generate the power distribution network gen_pdn in OpenLANE:


![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/d5914af3-3654-4eab-8004-569653664428)

![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/55f8a7f1-710b-4980-b48d-4fe4e6d740db)


    The PDN feature within OpenLANE will create:
        Power ring global to the entire core
        Power halo local to any preplaced cells
        Power straps to bring power into the center of the chip
        Power rails for the standard cells
    We see that there is a change in the DEF.
![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/8852db9c-ab28-42b4-9d3c-0f9b3b26c463)



 Global and Detailed Routing

    OpenLANE uses TritonRoute as the routing engine for physical implementations of designs. Routing consists of two stages:
        Global Routing - Routing guides are generated for interconnects on our netlist defining what layers, and where on the chip each of the nets will be reputed.
        Detailed Routing - Metal traces are iteratively laid across the routing guides to physically implement the routing guides.

    To run routing in OpenLANE: run_routing

![image](https://github.com/ughdeiek/Nirupamaec101-pes_pd/assets/142580251/9c08a4b8-c339-4811-a01d-86d5f7aa9d09)
if DRC errors persist after routing the user has two options:

    Re-run routing with higher QoR settings.
    Manually fix DRC errors specific in tritonRoute.drc




    
    After routing has been completed interconnect parasitics can be extracted to perform sign-off post-route STA analysis. The parasitics are extracted into a SPEF file.
    The SPEF extractor is not included within OpenLANE as of now.
