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

    - [L4 Velocity saturation drain current model](#)

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

