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


