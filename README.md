# CMOS-Circuit-Design-Spice-Simulation-using-Sky130nm-technology
Documentation and lab work for VSD CMOS Circuit Design using Sky130 technology.

# Table Of Contents

- [NgspiceSky130-Day1-Basics of NMOS Drain Current(Id) vs Drain-to-source Voltage(Vds)](#ngspicesky130-day1-basics-of-nmos-drain-currentid-vs-drain-to-source-voltagevds)

  - [Introduction to Circuit Design and Spice Simulations](#introduction-to-circuit-design-and-spice-simulations)

    - [L1 Why do we need SPICE simulations?](#L1-why-do-we-need-spice-simulations?)

    - [L2 Introduction to basic element in circuit design-NMOS](#L2-Introduction-to-basic-element-in-circuit-design-NMOS)

    - [L3 Strong inversion and threshold voltage](#[L3-Strong-inversion-and-threshold-voltage)

    - [L4 Threshold voltage with positive substrate potential](#)

  - [NMOS resistive region and Saturation region of operation](#)

    - [L1 Resistive region of operation with small drain-source voltage](#)

    - [L2 Drift current theory](#)

    - [L3 Drain current model for Linear region of operation](#)

    - [L4 SPICE conclusion to resistive operation](#)

    - [L5 Pinch-off region condition](#)

    - [L6 Drain current model for saturation region of operation](#)

  - [Introduction to SPICE](#)

    - [L1 Basic SPICE setup](#)

    - [L2 Circuit description in SPICE syntax](#)

    - [L3 Define Technology parameters](#)

    - [L4 First SPICE simulation](#)

    - [L5 SPICE lab with Sky130 models](#)

- [NgspiceSky130-Day2-Velocity saturation and basics of CMOS inverter VTC](#)

  - [SPICE simulation for lower nodes and velocity saturation effect](#)

    - [L1 SPICE simulation for lower nodes](#)

    - [L2 Drain current vs gate voltage for long and short channel device](#)

    - [L3 Velocity saturation at lower and higher electric fields](#)

    - [L4 Velocity saturation drain current model](#L4-Velocity-saturation-drain-current-model)

    - [L5 Labs Sky130 Id-Vgs](#)

    - [L6 Labs Sky130 Vt](#)

  - [CMOS voltage transfer characteristics (VTC)](#)

    - [L1 MOSFET as a switch](#)

    - [L2 Introduction to standard MOS voltage current parameters](#)

    - [L3 PMOS/NMOS drain current vs drain voltage](#)

    - [L4 Step1- Convert PMOS gate-source-voltage to Vin](#)

    - [L5 Step2 & Step3- Convert PMOS and NMOS drain-source-voltage to Vout](#)

    - [L6 Step4- Merge PMOS-NMOS load curves and plot VTC](#)

- [NgspiceSky130-Day3-CMOS switching threshold and dynamic simulations](#)

  - [Voltage transfer characteristics-SPICE simulations](#)

    - [L1 SPICE deck creation for CMOS inverter](#)

    - [L2 SPICE simulation for CMOS inverter](#)

    - [L3 Labs Sky130 SPICE simulation for CMOS](#)

  - [Static behaviour evaluation-CMOS inverter robustness-Switching Threshold](#)

    - [L1 Switching Threshold, Vm](#)

    - [L2 Analytical expression of Vm as a function of (W/L)n and (W/L)p](#)

    - [L3 Analytical expression of (W/L)n and (W/L)p as a function of Vm](#)

    - [L4 Static and Dynamic simulation of CMOS inverter](#)

    - [L5 Static and Dynamic simulation of CMOS inverter with increased PMOS width](#)

    - [L6 Applications of CMOS inverter in clock network and STA](#)

- [NgspiceSky130-Day4-CMOS Noise Margin robustness evaluation](#)

  - [Static behaviour evaluation-CMOS inverter robustness-Noise Margin](#)

    - [L1 Introduction to Noise Margin](#)

    - [L2 Noise Margin voltage parameters](#)

    - [L3 Noise margin equation and summary](#)

    - [L4 Noise margin variation with respect to PMOS width](#)

    - [L5 Sky130 Noise margin labs](#)

- [NgspiceSky130-Day5-CMOS power supply and device variation robustness evaluation](#)

  - [Static behaviour evaluation-CMOS inverter robustness-Power supply variation](#)

    - [L1 Smart SPICE simulations for power supply variations](#)

    - [L2 Advantages and disadvantages using low supply voltage](#)

    - [L3 Sky130 Supply variation Labs](#)

  - [Static behaviour evaluation-CMOS inverter robustness-Device variation](#)

    - [L1 Sources of variation - Etching process](#)

    - [L2 Sources of variation - Oxide thickness](#)

    - [L3 Smart SPICE simulation for device variations](#)

    - [L4 Conclusion](#)
   
    - [L5 Sky130 device variations labs](#)
   
  # NgspiceSky130-Day1-Basics of NMOS Drain Current(Id) vs Drain-to-source Voltage(Vds)

  ## Introduction to Circuit Design and Spice Simulations

  ### L1 Why do we need SPICE simulations?

  ---------
  # Introduction to SPICE
 
       
  ## L4 First SPICE simulation

  ### 1. Launch the Codespace
  
  ### From your GitHub repository page:
  <img width="1122" height="596" alt="image" src="https://github.com/user-attachments/assets/8bf86a34-8ca0-427f-9c83-f20e50895dc3" />

   1.Click on Code → Codespaces → Create codespace on main
    GitHub will automatically create a cloud-based Ubuntu environment.

  ### 2. Start ngspice and Verify Installation

  Once inside Codespace, open a terminal and type 
  `bash
  ngspice
   exit`
   You’ll see the ngspice version banner confirming installation.
   If ngspice exits successfully, your setup is ready.
  
  ### 3. Enable GUI / noVNC Desktop
    This Codespace comes with a full graphical desktop environment accessible through noVNC. Check the PORTS tab for a forwarded VNC link, typically on port 6080.
    <img width="1475" height="268" alt="image" src="https://github.com/user-attachments/assets/48dd1473-09fc-4a19-acff-afadd2ac13bb" />
     Click the forwarded address and click on "vnc_lite.html" as shown in below image — it opens a Linux desktop in your browser:
     <img width="1908" height="1020" alt="image" src="https://github.com/user-attachments/assets/999a3b84-baae-4dfc-954f-6e163abcf1c7" />
        Use this environment to visualize ngspice plots and waveforms interactively.

   ### 

- Open GitHub Codespaces

-  Open Terminal

- Clone the workshop repository:

`
git clone https://github.com/kunalg123/sky130CircuitDesignWorkshop.git`

 - Navigate to the design directory:

`cd sky130CircuitDesignWorkshop/design`
<img width="1642" height="295" alt="image" src="https://github.com/user-attachments/assets/df8a9881-1edd-4f5e-9af4-d702839381bf" />

 the `sky130_fd_pr` directory contains cells, models and tech files
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/c896178a-f614-4131-91da-cf25cf2b1f71" />

In the cells files ,it contains nfet and pfet cells, these only two cells we will be using in this entire workshop.

the nfet has spice libraries at different corners, we will be considering one such typical corner.
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/ec5129e2-329e-4157-a5f5-60c3193892ae" />
We get all the model parameters required for the process
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/dae233fd-4399-406c-9e9c-af8ff0448fb3" />
If we go to `less sky130_fd_pr__nfet_01v8__tt.corner.spice` , it contains different W and L values , which is pre defined . For this simulation, one of the available values is chosen.
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/e3cf04ea-854b-4d18-bd4a-da9800ff7e7c" />

Next, navigate to the `models` directory and open the `lib.spice` file. This file contains different library definitions for NMOS and PMOS devices.
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/2da59857-4efa-49dd-bc59-566548071575" />

The library includes various process corner files such as Typical-Typical (TT), Slow-Fast (SF), Fast-Slow (FS), and Fast-Fast (FF). These corner models are used to study the behaviour of transistors under different manufacturing conditions.
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/61f52847-b4f2-4968-9d90-68e75d718c24" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/71ec4beb-42c8-41e0-b0de-f023a7c3453a" />

Go to `design` directory and choose `day1_nfet_idvds_L2_W5.spice`
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/0b8e8321-e29b-4eda-a49e-d774874a63b2" />


Here ,ew can see we are including the library file , here we are doing the typical corner (tt) --> if wanted to do Slow-Slow corner replace 'tt' with 'ss' 
if we see spice syntax , we we see it in this order - transistor -> drain vge -> gate-> source-> substrate-> transistor technology file-> width of gate -> length

 here , Vgs is sweeping from 0 to 1.8V, with the step of 0.2V 
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/5743ef98-7008-4cd9-953d-fc1223e07c1b" />

For spice simulation, type ` ngspice day1_nfet_idvds_L2_W5.spice`
<img width="1920" height="1080" alt="Screenshot 2026-06-12 200909" src="https://github.com/user-attachments/assets/9852fe6e-c393-49c3-a53d-2d6c3be54646" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/9080c9ab-b970-4514-a648-f1c0687b5a9d" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/72df8cdd-d5d0-48e3-9a24-1eca06582538" />

The graph is Id v/s Vds at different Vgs values
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/69201afe-247a-46e6-a7a5-dd7c80162d4b" />

For seeing different Id values at particular Vd and Vgs then left click on it
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/941d0af8-ce33-48f2-941c-b8d8b4f72d1a" />


## L2 Drain current vs gate voltage for long and short channel device

compare the two different simulation for Long (length= 1.2 u) channel device and short (length= 0.25u) channel device
<img width="951" height="387" alt="image" src="https://github.com/user-attachments/assets/e040da19-5ab1-49fc-9542-338575414141" />

For long channel device
<img width="745" height="722" alt="image" src="https://github.com/user-attachments/assets/9c8ad24f-da2f-4d67-94ce-0a208a3205ee" />
First observation- For different value of Vgs at one value of Vds (lets take 2.5V) , you will see drain current quadratically increases with increase in gate voltage(Vgs)

For short channel 
<img width="691" height="557" alt="image" src="https://github.com/user-attachments/assets/1160a762-29c2-4b77-8b48-f665ed35486b" />
Drain current varies quadratically for small Vgs values and then as the gate valotage increases it varies linearly due to velocity saturation.

now lets do Ids v/s Vgs by keeping Vds constant =2.5V

  First lets see syntax -
          <img width="532" height="302" alt="image" src="https://github.com/user-attachments/assets/b430c913-a625-4909-a61f-3da1bcb53bb5" />
         whatever you see in the left hand side is sweeped or tuned at every value of right hand side so Vin will sweeped at every value of Vdd

<img width="838" height="675" alt="image" src="https://github.com/user-attachments/assets/913ad58a-dd12-41ff-8c23-642f8c793439" />
this plot looks fairly quadratic

Lets compare this plot with short channel one
<img width="1361" height="682" alt="image" src="https://github.com/user-attachments/assets/c255299a-318d-4b86-92c8-3ca83987d127" />

## L3 Velocity saturation at lower and higher electric fields
 We see as the Vgs increases in short cahnnel device , drain current increases linearly  due to velocity saturation .
 One of the effect of short channel is velocity saturation .
 <img width="1361" height="682" alt="image" src="https://github.com/user-attachments/assets/9f425fe8-1e60-4989-b236-0cbd1553f0e7" />

For lower nodes - 4 regions of operation:  Cut Off, Linear, Saturation and Velocity Saturation 
   Velocity saturation means velocity is linear function when electric field is lower than critical electric field and velocity becomes constant after elctric field crosses critical electric field.
<img width="983" height="536" alt="image" src="https://github.com/user-attachments/assets/1644e0aa-9cf1-4a32-b09d-d687f57d7307" />
    Drain current model 
    <img width="947" height="463" alt="image" src="https://github.com/user-attachments/assets/530471dd-7e6b-433e-8111-a2b1b7c8f822" />

## L4 Velocity saturation drain current model
 
 <img width="947" height="463" alt="image" src="https://github.com/user-attachments/assets/6e0be203-8d09-414a-ab42-a53c20a270e7" />
 Current eq as shown above in pic , for lower value of Vds that 'lambda Vds ' term will get vanished.
 for Vmin we will take the lowest value of among vgt, vds, vgsat. 

 lets do an example
     here we take Vgs- Vt = Vgt, if Vgt <0 then Id =0 , transistor operates at cuttoff region
     Vdsat is technology parameter , it tells at what value of Vdsat the device enters the velocity saturation region
     <img width="956" height="576" alt="image" src="https://github.com/user-attachments/assets/dacd3e3a-27cd-48aa-84da-e8e587ddb3f9" />
 
 <img width="926" height="562" alt="image" src="https://github.com/user-attachments/assets/0dc44d17-0f11-4975-af5e-4de7f5d6d568" />
 <img width="907" height="557" alt="image" src="https://github.com/user-attachments/assets/a2f5c853-08a7-4c7d-99e3-c9cbd983d3f6" />
 <img width="902" height="558" alt="image" src="https://github.com/user-attachments/assets/ef2b437f-5d6e-4a93-b5e6-3bdcb0770ef0" />
  lets expand the eq
 <img width="1142" height="607" alt="image" src="https://github.com/user-attachments/assets/b7ac0eac-b0b1-4391-a106-6fb9f4a6d0c6" />
    if we ignore other terms in eq , and keeps w constant and for lower value of L, id increases but its not true practically.

  ### - 2nd obseravtion - for lower value of nodes of device the peak curent reduces and reason is velocity saturation causes devices to saturates early.
  
  so peak current value for same W/L ratio is different for long channel device and lower channel device .peak cureent in lower nodes device saturates early.
  <img width="1357" height="712" alt="image" src="https://github.com/user-attachments/assets/64c0c1ef-d540-42b9-8b31-fdc7ae05a324" />

   open source websites to getting more hands on 
   <img width="1097" height="192" alt="image" src="https://github.com/user-attachments/assets/63763106-090c-45c2-9561-d754f37dae8b" />


