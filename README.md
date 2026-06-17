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
 We see as the Vgs increases in short channel device , drain current increases linearly  due to velocity saturation .
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

## L5 Labs Sky130 Id-Vgs

Simulation for Id vs Vgs for short length device
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/9b97cbd0-d4eb-4b1c-94c8-a75abc89ecf9" />


<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/aeb07f65-71a8-48ef-a5eb-e76c191c31d1" />

  here you can see we are doing for typical corner and w=0.39 l=0.15 and here doing dc simulation and sweeping Vds from 0 to 1.8V with the step of .1 V and sweeping Vgs also with the step of .2 V

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/863eb8de-68e7-4546-80a9-4a71d079f5a7" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/490768cf-cd10-4dbe-b3cf-bedf3470ea8d" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/a55346b9-686d-4ce7-bc25-7716264b3d34" />
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/86d06f3b-7a7e-40b4-ae0e-fae36def6991" />

The plot is Id vs Vds for different values of Vgs. We can see for lower values of Vgs it is quadratic behaviour and for higher values of Vgs it is Linear . To see the peak current for Vgs=1.8V, left click on at Vgs=1.8V

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/c6c59ef9-9219-478b-b63e-3d5b80e083eb" />
 peak current is around 197 uA

 If we want to see Id vs Vds 
 <img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/8f127cf2-fc60-48bf-863d-160e69d18f95" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/c864db92-81dc-44d8-ab8f-dd46a9a8b7d6" />

  We are again keeping same values  w=0.39 l=0.15 , and keeping Vds constant 1.8 v and sweeping only Vgs values from 0 to 1.8V with the step of .1v

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/b625715f-c278-439b-874e-f1875595ce07" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/cc48312f-712f-4b85-b756-8a506a371842" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/838ac860-51c5-4ef8-a254-87735d55837f" />
The above is Id vs Vgs curve keeping Vds constant and due to short channel it is showing linear behaviour for higher values of Vgs

## L6 Labs Sky130 Vt

Calculating threshold voltage Vt for Ig vs Vgs curve 

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/e836ef16-772b-44f7-987f-8bbd443ddabc" />

<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/13521d65-5187-4c28-9804-6e39dcf5c12a" />

For Id vs Vgs curve threshold voltage is somewhere where current starts increasing drastically with small change in Vgs values.
To plot 'Vt' , we have to take tangent of the slope and extends it on the x-axis( we can do this by moving cursor )
<img width="1920" height="1080" alt="image" src="https://github.com/user-attachments/assets/5460e800-5e85-4b2d-a552-1c8c65e15cb3" />
we gets somewhere around  0.78 V

# CMOS voltage transfer characteristics (VTC)

## L1 MOSFET as a switch
 We will see mosfet device property from switch point of view 

<img width="1145" height="561" alt="image" src="https://github.com/user-attachments/assets/245b3efa-1fdf-4946-a53d-40dec06e6092" />

MOS device characteristics :
 This MOS transistor works when |Vgs| > |Vt| 
 |Vgs| -> PMOS  +ve Vgs and NMOS -ve Vgs

 |Vgs| > |Vt| , switch closed and device is ON

Now we will bias the MOS :where we will connect NMOS and PMOS and make it behave as CMOS device.

<img width="1242" height="722" alt="image" src="https://github.com/user-attachments/assets/a2a5d02c-7c96-47cc-b0a5-891c8fd12451" />

CMOS means complementary mosfet ; it has complementary logic when one is ON other one is OFF and vice versa
here , CL is either a long wire or with a short wire with the another CMOS over here
In NMOS ,Vgs = Vin (gate)- Vss(source)
In PMOS, Vgs = Vin(gate) -Vdd(source)

# L2 Introduction to standard MOS voltage current parameters
We trying to get the equivalent circuit of CMOS by varying the boundary conditions when Vin is 'high' and 'low', so that we can get the Voltage Transfer Characteristics (VTC) and therefore calculate the delay of the cell.
When we take Vin as 'high' and equal to Vdd, PMOS will be OFF and NMOS will be ON
<img width="1243" height="722" alt="Screenshot 2026-06-13 174913" src="https://github.com/user-attachments/assets/b76722d0-b463-43ac-940f-c82738a010d9" />
When we take Vin as 'low' or equal to '0', PMOS will be ON and NMOS will be OFF.
 <img width="1238" height="738" alt="Screenshot 2026-06-15 151413" src="https://github.com/user-attachments/assets/968e9e47-8785-489e-8b87-9acdb56f8b25" />
So we can see that when Vin=Vdd there is a direct path that exists between Vss and Vout, the capacitor CL discharges through the resistor.
Similarly when Vin=0 there is a direct path between Vdd and Vout, CL charges
<img width="1200" height="642" alt="Screenshot 2026-06-15 152414" src="https://github.com/user-attachments/assets/8a83da49-3539-47d5-a7fc-2cf1e542d8ce" />
Lets give the naming convention of the CMOS
<img width="1244" height="654" alt="Screenshot 2026-06-15 152824" src="https://github.com/user-attachments/assets/4023d6b5-e74e-4835-b722-a4d1ad668a12" />
current in both the condition is Idsn(drain to source for NMOS) and Idsp(Drain to source for PMOS) And Idsp = -Idsn, both are opposite in direction to each other.

## L3 PMOS/NMOS drain current vs drain voltage
<img width="1281" height="733" alt="Screenshot 2026-06-15 154755" src="https://github.com/user-attachments/assets/9402f8fc-82b6-4255-8b40-1ea233d2d258" />
the curve between Idsn Vs Vdsn and Idsp Vs Vdsp, it is as shown above.

## L4 Step1- Convert PMOS gate-source-voltage to Vin
There are many voltages but from logic block POV , we will consider only two vpltages Vout , Vin. From these we calculate the VTC and eventually we get to know the delay.
#### Assumption- 
Now we will see the steps to obtain Voltage Transfer Characteristics(VTC) for static CMOS inverter: Assumption: Let us assume that it is a long channel device with Vdd=2V
We will fix the Vgs values as shown below
We know that Vgsp= Vin-Vdd, So we get the above values.So we get Vin = Vgsp+Vdd, we are trying to convert all the voltages as function of Vin and Vout.
We will try to plot the graph of PMOS in terms of Idsn, the plot will be as shown below. We can see that the corresponding Vin value of Vgsp is being plotted as shown in the above table.<img width="1301" height="732" alt="Screenshot 2026-06-15 181444" src="https://github.com/user-attachments/assets/340bf594-9f01-45d5-8b5c-811a9da526b1" />

## L5 Step2 & Step3- Convert PMOS and NMOS drain-source-voltage to Vout
we will be converting the Vdsp as function of output voltage . We know Vdsp = Vout-Vdd.
 converting Vdsp into Vout. So to get Vout there is a shift of Vdd towards left hand side.
<img width="1362" height="467" alt="image" src="https://github.com/user-attachments/assets/7d555d2e-28de-4e74-9f75-4c23ab2ce1f5" />
We can see that whenever Vout=2V that means Vdsp=0V and Vdd=2V (given), then The current is zero and capacitor at the output is discharged. This is true only when PMOS is in combination with NMOS and forms a CMOS inverter.
Let us take another example, when Vout=0V, that means -Vdsp=2V and Vdd=2V, so at every gate voltage of Vin we will see a finite current whenever Vout=0V. As Vout=0V, the capacitor is completely discharged and we need to charge that, so that is the charging current required. So, here we get the load curve for PMOS
<img width="492" height="427" alt="image" src="https://github.com/user-attachments/assets/aea34145-6fb7-4820-b44e-cccbb0219b0d" />
Now we will try to get the "load curve" for NMOS transistor from this equations.
<img width="296" height="227" alt="image" src="https://github.com/user-attachments/assets/938b0358-fcf5-4272-8a52-d1bfae701e2f" />
It is actually simple as Vgsn = Vin and Vdsn = Vout, directly we can get the graphs.
<img width="447" height="317" alt="image" src="https://github.com/user-attachments/assets/e435c6b1-2c92-4151-86db-a9c74370e10b" />
<img width="937" height="403" alt="image" src="https://github.com/user-attachments/assets/7adce866-0b66-4455-87da-8105a6247933" />

## L6 Step4- Merge PMOS-NMOS load curves and plot VTC

we will generate the VTC of CMOS by superimposing load curve of NMOS on load curve of PMOS 
<img width="1315" height="397" alt="image" src="https://github.com/user-attachments/assets/d33f72cc-7b96-40cf-9235-16a37a0df8a0" />

To superimpose both the Load Curves to get the VTC we are doing this to find out the common point between Vin and Vout of both NMOS and PMOS
<img width="500" height="367" alt="image" src="https://github.com/user-attachments/assets/3110630c-dc3f-4595-9abe-ea69dcba37e7" />

Range of voltage we are looking now is 0 - 2V

- When Vin = 0V, Vout = 2V; PMOS is in Linear region and NMOS is Cut Off .

- When Vin = 0.5V, 1.5V < Vout < 2V; NMOS is in Saturation region and PMOS is in Linear region, this is the area of the CMOS where it lies in very high gain state and 'gain'=cahnge in output per change in input .

- When Vin = 1V, 0.5V < Vout < 1.5V; NMOS and PMOS are in Saturation region.

- When Vin = 1.5V, 0<Vout<0.5V; NMOS is Linear region and PMOS is in Saturation region.

- When Vin = 2V, Vout = 0V; NMOS is in linear region and PMOS is Cut Off 
<img width="1288" height="717" alt="image" src="https://github.com/user-attachments/assets/a225eb8a-ca8e-4000-9c7d-f8324d0cf57c" />

# NgspiceSky130-Day3-CMOS switching threshold and dynamic simulations

## Voltage transfer characteristics-SPICE simulations

## L1 SPICE deck creation for CMOS inverter

Before simulating spice simulation of CMOS we first create spice deck. Spice deck is connectivity information(Netlist). As there is information about substrate, the circuit is as shown below.Here M1 is PMOS and M2 is NMOS
In this case we are looking at the static characteristics of CMOS
<img width="475" height="426" alt="image" src="https://github.com/user-attachments/assets/a9dc6f74-5b8b-4669-8ae9-ffd212853e49" />

Next define component values , keeping W/L ratio of both same
<img width="397" height="426" alt="image" src="https://github.com/user-attachments/assets/72e55491-8a5a-4394-917b-57b60414494a" />

Now assume the Vin and Vout values
<img width="522" height="438" alt="image" src="https://github.com/user-attachments/assets/562033fc-89b7-44af-adae-fded8dfe3f20" />

Now identify the nodes(*two points betwwen which there is a component*) 
<img width="715" height="548" alt="image" src="https://github.com/user-attachments/assets/42fb9419-6588-49e6-97da-95db893ff37c" />

Name these nodes . In model file we will mention like, 2.5V input lies between Vin and 0, similarly Vdd lies between vdd and 0.
<img width="563" height="446" alt="image" src="https://github.com/user-attachments/assets/50190c84-85cd-4b1e-b209-54f6a4eab27b" />

now write *Spice Deck*  
<img width="1242" height="577" alt="image" src="https://github.com/user-attachments/assets/8d6f4a51-43d6-417f-a0d3-7c04e9fd8c4c" />
Syntax for MOSFET is drain, gate, substrate, source.

## L2 SPICE simulation for CMOS inverter

<img width="1247" height="562" alt="image" src="https://github.com/user-attachments/assets/1911792b-f31f-474c-aca1-23c7b950a929" />
<img width="1232" height="567" alt="image" src="https://github.com/user-attachments/assets/ed0e783b-624e-4a69-a421-d6dad9a87f12" />

*simulation commands*
Here we are sweeping the gate input voltage from 0 to 2.5V and of step size 0.05V , reason we are doing this is to calculate the Vout or waveform at output while we sweep the input voltage because that's the Voltage Transfer Characteristics.
*Final Step* - is to describe the *Model files*, all the information about the technological parameteres is given inside the model files.
<img width="1223" height="566" alt="image" src="https://github.com/user-attachments/assets/bb5e8fda-da9f-4783-8623-f81b5d3d609f" />

Now we will do the SPICE simulation for Wn=Wp=0.375u, Ln=Lp=0.25u, Wn/ln=Wp/Lp=1.5. Below is the VTC we get for the above netlist.
<img width="788" height="638" alt="image" src="https://github.com/user-attachments/assets/c7c0baf3-3cc7-4955-a2be-a0e74b57cf76" />

Next we will get the VTC for Wn= 0.375u, Wp= 0.9375u, Ln,p=0.25u; Wn/Ln=1.5, Wp/Lp=2.5 (PMOS width is 2.5 times more than NMOS)
<img width="786" height="635" alt="image" src="https://github.com/user-attachments/assets/981c3e8c-3a6b-4b9f-9e7e-97b264099cf7" />
If we observe this graph is toward middle and the previous graph is left shifted slightly. This happens because NMOS is more stronger than PMOS in previous graph.

## L3 Labs Sky130 SPICE simulation for CMOS
Plot the VTC characteristics of CMOS inverter.
<img width="1902" height="975" alt="image" src="https://github.com/user-attachments/assets/6ae7e35c-2fc3-40b9-9ff0-46a07ee0af25" />

We are using both pfet and nfet for CMOS inverter. We can see that W/L ratio of pmos is 2.33 times greater than that of nmos. And we will be sweeping Vin from 0 to 1.8V with step isze of 0.01V and plotting the Vout.
<img width="1912" height="978" alt="image" src="https://github.com/user-attachments/assets/be907c06-ca47-4d40-b183-cb9dc5e01335" />
<img width="1907" height="978" alt="image" src="https://github.com/user-attachments/assets/416e7b3d-4dc1-4344-b378-c02f2711cb9e" />
VTC of CMOS inverter
Now we need to know the Switching Threshold from this graph, it is the point when Vin=Vout.
To zoom in the curve; press righ mouse button + hold it.
<img width="1913" height="1001" alt="image" src="https://github.com/user-attachments/assets/69067425-a62f-402b-9528-345b29a66815" />

So switching threshold for W/L=2.3 is around 0.876V
<img width="290" height="57" alt="image" src="https://github.com/user-attachments/assets/9c158b8b-22b5-4d71-9a58-3696d4db1d3b" />
We will now to the transient analysis:
For that we will go inside the tansient SPICE file for day3
<img width="1918" height="977" alt="image" src="https://github.com/user-attachments/assets/f54e63fb-f237-4d7c-a0c1-e64e93aa9c81" />
<img width="1918" height="982" alt="image" src="https://github.com/user-attachments/assets/1576ae73-8116-4ab7-bc2e-d77c23e51c52" />
We can see that it is for typical corner as before and the W/L is also same. But now we taking transient pulse from 0v to 1V with shift of 0 with rise time and fall time being 0.1ns and 0.1ns respectively, pulse width of 2ns and total time period of 4ns. Let us run this.
<img width="1906" height="982" alt="image" src="https://github.com/user-attachments/assets/652fb796-e2e0-4d85-9b1d-3c334d155c09" />
To calculate rise delay and fall delay, we need to consider 50% of Vdd output curve i.e. at 0.9V; out-in area
<img width="1887" height="973" alt="image" src="https://github.com/user-attachments/assets/5ef422bf-0f1d-40ca-b0cc-c46e7857e674" />
<img width="286" height="68" alt="image" src="https://github.com/user-attachments/assets/91762faa-0449-4a1c-a0c0-35e32e4c27cf" />
herefore Rise delay = 2.47742ns-2.14839ns = 0.32903ns

For fall delay, consider while falling.
<img width="876" height="675" alt="image" src="https://github.com/user-attachments/assets/781d6c53-2406-4858-aa3a-4692a5e28405" />
<img width="343" height="68" alt="image" src="https://github.com/user-attachments/assets/9f21bf13-edc8-4947-9b2b-cbc8f5c0ba15" />
Therefore **Fall Delay** = 4.334ns-4.050ns = 0.285n

# Static behaviour evaluation-CMOS inverter robustness-Switching Threshold

## L1 Switching Threshold, Vm
Lets compare CMOS of same and different W/L ratio ,shape of VTC in both the cases are same , this shows robustness of CMOS inverter.
Robustness- when Vin is zero output is high & when Vin is high, output is zero.
One of the Parameters defining the robustness of CMOS is Switching frequency
*Switching Thresholds* is a point where Vin=Vout
<img width="1182" height="560" alt="image" src="https://github.com/user-attachments/assets/5111686a-389b-429d-948a-9b512dc93cce" />
Let us find out the Switching threshold, in *both* cases switching threshold is different Vm in both the cases by drawing a 45 degree line.
So, in first case Vm comes out to be somewhere around 0.9V and in second case Vm=1.2V.
<img width="1168" height="625" alt="image" src="https://github.com/user-attachments/assets/480412fe-0b1d-406c-8756-1fd3220b5f7c" />
<img width="1150" height="625" alt="image" src="https://github.com/user-attachments/assets/1a042dfe-9cbf-4bc0-9d1e-f419973e6f5b" />
This is the area where PMOS and NMOS both are in saturation region. Current flows from both the transistor, it is actually a dangerous situation.

## L2 Analytical expression of Vm as a function of (W/L)n and (W/L)p
Lets continue we were analysing the situation when gate voltage is equal to drain voltage i.e Vin=Vout and that the point where we call switching threshold so we call the threshold point where output switches.
we will be calculating Vm for both cases same W/L ratio and different one where pmos is greater and also we will defining Vm values and then see what will be the W/L .
Now lets evaluate the value of Vm as the function of W/L ratio of PMOS
<img width="520" height="331" alt="image" src="https://github.com/user-attachments/assets/95f57651-11d1-4147-ad22-efcad6ae00b7" />
<img width="861" height="227" alt="image" src="https://github.com/user-attachments/assets/b67943ba-1189-44a1-9793-50ab6ce67c45" />

## L3 Analytical expression of (W/L)n and (W/L)p as a function of Vm

we will calculate the value of W/L for PMOS and NMOS when Vm is given
This is a reverse fashion
calculate W/L ratio of PMOS and NMOS such that Switching threshold is exatly half of the power supply Vdd = 2.5V, therefore required Vm = 1.25V.
We will start from the current equation itself i.e. Idsn = -Idsp
<img width="938" height="226" alt="image" src="https://github.com/user-attachments/assets/402ffa21-07d9-44c1-afe4-41e00f7da4c8" />
Expandind kp and kn as gain factor
<img width="1023" height="238" alt="image" src="https://github.com/user-attachments/assets/1797f011-7cf9-4def-ab54-0703f5146dc0" />
<img width="1012" height="247" alt="image" src="https://github.com/user-attachments/assets/3f285183-057b-4838-b8d7-ccfa16bddeda" />
<img width="936" height="242" alt="image" src="https://github.com/user-attachments/assets/505d5323-cb99-4146-8fbb-cc32637b90d9" />
<img width="572" height="306" alt="image" src="https://github.com/user-attachments/assets/c8d200db-d945-45f6-8793-db9918bf9ef3" />
The values of all parameters are available from the model files except Vm. Once Vm is known, the required W/L ratios can be calculated.

Different PMOS and NMOS sizing combinations are then tested to observe their effect on CMOS inverter behavior and switching threshold.

## L4 Static and Dynamic simulation of CMOS inverter
For (W/L)n = (W/L)p = 1.5
<img width="790" height="636" alt="image" src="https://github.com/user-attachments/assets/01fb7d8f-953a-44fb-bdcb-e7de877caa54" />
Transient analysis is used to calculate the rise delay and fall delay of the CMOS inverter.
<img width="1236" height="566" alt="image" src="https://github.com/user-attachments/assets/b0640f3b-226e-4395-ad75-0763961c6e1a" />

## L5 Static and Dynamic simulation of CMOS inverter with increased PMOS width
doing the SPICE simulations for increased width of PMOS transistors and compare the results.
<img width="1240" height="512" alt="image" src="https://github.com/user-attachments/assets/8553e299-364e-420a-8704-1a01f38aacd6" />
<img width="1237" height="501" alt="image" src="https://github.com/user-attachments/assets/11afdb7c-61cd-4d5a-bb79-1d7b1b82e9ab" />
<img width="1242" height="507" alt="image" src="https://github.com/user-attachments/assets/1b81a44f-6bfb-482d-bf34-4f08ff50874a" />
<img width="1213" height="492" alt="image" src="https://github.com/user-attachments/assets/1e28f858-5758-49a4-9273-e5b1babbee8b" />

## L6 Applications of CMOS inverter in clock network and STA

Data set:
<img width="770" height="279" alt="Screenshot 2026-06-16 234835" src="https://github.com/user-attachments/assets/edc7e5b3-9af5-428b-a5cf-057a93eb7d44" />

From this experiment, a few important observations can be made.

Small variations in PMOS and NMOS dimensions may occur during the fabrication process. However, the CMOS inverter remains fairly robust, and the switching threshold voltage (Vm) does not change significantly for minor size variations.

It is also observed that when the PMOS transistor is sized approximately twice the NMOS transistor, i.e., (W/L)p ≈ 2(W/L)n, the rise delay and fall delay become nearly equal. This balanced behavior provides symmetry in the inverter's switching characteristics.

Such symmetrical operation is desirable in clock buffers and clock inverters, where equal rise and fall delays help maintain accurate timing performance.
<img width="1157" height="687" alt="image" src="https://github.com/user-attachments/assets/7b46b6f8-9098-47f6-99a4-859a26c4f771" />

<img width="770" height="278" alt="image" src="https://github.com/user-attachments/assets/254cd8bc-1a78-4058-b691-cdb92cf23bb5" />

<img width="1315" height="706" alt="image" src="https://github.com/user-attachments/assets/395d838c-9349-4e2c-8e1c-b05e20570c56" />
Different types of cells can be selected in the data path depending on the timing requirement. Stronger cells can be used to reduce rise time, fall time, and propagation delay, thereby improving timing performance.

# NgspiceSky130-Day4-CMOS Noise Margin robustness evaluation

## Static behaviour evaluation-CMOS inverter robustness-Noise Margin

## L1 Introduction to Noise Margin

Next step in determining the CMOS inverter robustness is to identify the noise margin.Any device and logic gates has certain noise maegin
*Noise Margin* represents the ability of a digital circuit to tolerate unwanted noise without causing an incorrect logic transition.
<img width="453" height="436" alt="image" src="https://github.com/user-attachments/assets/cab9cbf5-e288-4819-9657-9a57306cfb20" />
In an ideal Inverter, for inputs 0/1 it gives output as 1/0. The slope of switch is infinite.
But practically , it has some resistance and capacitance so it will have some finite slope and there will be a delay
<img width="372" height="343" alt="image" src="https://github.com/user-attachments/assets/c595eacf-a5ac-4c30-a663-ea612988be61" />
We see that whenever the input is between 0 to VIL(input low voltage); the output will be high 'VOH'
Any input voltage which lie between VIH (input high voltage) and Vdd ,output will be VOL.
<img width="361" height="343" alt="image" src="https://github.com/user-attachments/assets/7a354af3-7b94-44af-88b6-d251c8083c76" />

## L2 Noise Margin voltage paramters
In an ideal inverter, the transition between logic HIGH and logic LOW is very sharp. However, in a practical CMOS inverter, the VTC curve has a finite slope due to device non-idealities.

When the input voltage is below VIL, the output remains close to VOH (logic HIGH). Similarly, when the input voltage is above VIH, the output remains close to VOL (logic LOW).

The points VIL and VIH are obtained from the locations where the slope of the VTC curve is approximately −1. These points are used to determine the noise margins of the inverter.

A larger noise margin indicates better immunity to noise and more reliable circuit operation.
<img width="732" height="497" alt="image" src="https://github.com/user-attachments/assets/ab4bdef7-450b-4d92-9bb4-245a2aaec6a7" />

## L3 Noise margin equation and summary

we will calculate the noise margin equation, for that we will plot the voltages on the same scale.
In below image-
- **Noise Mrgin High** - Any voltage level which lie at the range of VIH and VOH will be detected as logic 1 whether it is input or output of the circuit.
- **Noise Margin Low** - Any voltage level which lie betwwen the range VIL and VOL will be detected as logic 0
In the range between VOH and VIL thats called undefined region , can't be either 1 or 0
<img width="710" height="422" alt="image" src="https://github.com/user-attachments/assets/ede2ad34-1735-4272-af25-8b5e9de1c285" />
<img width="1312" height="840" alt="image" src="https://github.com/user-attachments/assets/cfe98a3c-be56-4290-b39f-de6fe0189cb0" />

## L4 Noise margin variation with respect to PMOS width

Here we will see by increasing the size of PMOS w.r.t NMOS by some integer of NMOS how does the value of *Noise Margin* high and low will raise and depending on these noise margin will decide the robustness CMOS to the noise margin.
So first we will findout the point on this particular curve when the slope is negative 1 and extend them.
<img width="1292" height="685" alt="image" src="https://github.com/user-attachments/assets/f06723a0-89d1-4b0b-a112-93487ff85077" />

<img width="1215" height="681" alt="image" src="https://github.com/user-attachments/assets/823d99c8-4db1-461d-8253-28301c32f7bc" />
As the noise margin increases, the CMOS inverter becomes more reliable and less sensitive to external noise disturbances
<img width="1222" height="528" alt="image" src="https://github.com/user-attachments/assets/126e23ed-6315-4495-b3f9-c69da5333cef" />
<img width="1228" height="526" alt="image" src="https://github.com/user-attachments/assets/69a6357c-af99-4826-81d7-3ed6ab3165d2" />
<img width="1222" height="522" alt="image" src="https://github.com/user-attachments/assets/236c925d-cdc8-4553-b4db-0ec993d5db97" />
From the simulation results, it is observed that increasing the PMOS width beyond a certain value does not significantly improve the noise margin. For the higher W/L ratios considered, the noise margin remains nearly constant, indicating that the inverter has reached a stable operating region.
<img width="732" height="253" alt="image" src="https://github.com/user-attachments/assets/bc34d0a3-4bf6-4f6b-ac36-8b9b8ad0bb1a" />
This behavior demonstrates the robustness of the CMOS inverter against device size variations.

The VTC and noise margin analysis also help in identifying the transition region between analog and digital operation of the inverter. Outside the transition region, the inverter behaves as a digital circuit, while within the transition region it exhibits analog characteristics.
<img width="707" height="597" alt="image" src="https://github.com/user-attachments/assets/0347e829-5ee8-4692-aff5-550cae4982de" />
<img width="736" height="566" alt="image" src="https://github.com/user-attachments/assets/2d67e691-8692-4a3b-9704-65c0f18d77ba" />

## L5 Sky130 Noise margin labs






