# PLL-design-OSU-180nm
This repository presents design of on-chip clock multiplier(8X PLL) using open source EDA tool OSU 180nm 

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Table of Contents:**

1.[INTRODUCTION TO ON-CHIP CLOCK MULTIPLIER](#-INTRODUCTION-TO-ON--CHIP-CLOCK-MULTIPLIER)<br />
2.[THEORY](#-THEORY)<br />
3.[SPECIFICATION](#-SPECIFICATION)<br />
4.[TOOLS](#-TOOLS)<br />
5.[PRE-LAYOUT DESIGN AND SIMULATION](#-PRE--LAYOUT-DESIGN-AND-SIMULATION)


1.**INTRODUCTION TO ON-CHIP CLOCK MULTIPLIER:**

The repository contains simulation files and other relevant files for on-chip clock multiplier using PLL(Fclock-in:5MHZ-12MHz ;Fclock-out:40MHz-100MHz at 1.8V)IP.
The goal is to design on-chip clock multiplier using OSU-180nm technology node.The on-chip clock multiplier is present in almost all synchronous processors.

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------

2.**THEORY:**

A phase-locked loop (PLL) uses a reference frequency(Fclock-in) to generate a multiple of that frequency. A voltage controlled oscillator (VCO) is initially tuned roughly to the range of the desired frequency multiple. The signal from the VCO is divided down using frequency dividers by the multiplication factor. The divided signal and the reference frequency are fed into a phase comparator. The output of the phase comparator is a voltage that is proportional to the phase difference. After passing through a low pass filter and being converted to the proper voltage range, this voltage is fed to the VCO to adjust the frequency. This adjustment increases the frequency as the phase of the VCO's signal lags that of the reference signal and decreases the frequency as the lag decreases (or lead increases). The VCO will stabilize at the desired frequency multiple. This type of PLL is a type of frequency synthesizer.

Modern microprocessors have 2GHz-5GHz clock frequencies whereas quartz oscillator can produce only few MHz ,so to achieve high frequency clock signal from low-frequency clock source we are designing PLL IP block and simulating it in this repository.

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------

3.**SPECIFICATION:**

| Parameter | Description                       | Min  | Type        | Max   | Unit | Condition                                                                            |
|-----------|-----------------------------------|------|-------------|-------|------|--------------------------------------------------------------------------------------|
| VDD       | Digital supply voltage            |      | 1.8         |       | V    | T=-40 to 150C                                                                        |
| FCLKREF   | Reference clock frequency         | 5    | 10          | 12.5  | MHz  |                                                                                      |
| FCLKOUT   | Output clock frequency            | 39.7 | 80.91       | 99.81 | MHz  | PLL mode, T=27C, VDD=1.8                                                             |
| FCLKOUT   | Output clock frequency            |      |             |       | MHz  | VCO mode, T=27C, VDD=1.8                                                             |
| DC        | Duty Cycle                        | 48   |             | 52    | %    | T=-40 to 150C                                                                        |
| IBCP      | Bias current for VCO              |      |             |       | uA   |                                                                                      |
| VVCO      | Oscillatror control input voltage | .557 |             | 0.62  | V    | Vin_vco = 0V at t = 0 (.uic)                                                         |
| JRMS      | Jitter (rms)                      |      | future work |       | ps   | PLL mode, FCLKREF = 10MHz                                                            |
| TSET      | Settling Time                     | 5.2  | 5           | 4.6   | us   | start from EN_CP and report 2 values; one at FCLKOUT=40MHz and one at FCLKOUT=100MHz |
| CL        | Load Capacitance                  |      |             |       | pF   |                                                                                      |
| IDDA      | Analog Supply current             |      |             |       | ua   | VVCO=0.8V, VCO mode                                                                  |
| IDDA      | Analog Supply current             |      |             |       | ua   | FCLKREF=10MHz, PLL mode                                                              |
| IDDA      | Analog Supply current             |      |             |       | pa   | EN_VCO=0, EN_CP=0, FCLKREF=0                                                         |
| IDDD      | Digital Supply Current            |      |             |       | uA   | VVCO=0.8V, VCO mode                                                                  |
| IDDD      | Digital Supply Current            |      |             |       | uA   | FCLKREF=10MHz, PLL mode                                                              |
| IDDD      | Digital Supply Current            |      |             |       | uA   | EN_VCO=0, EN_CP=0, FCLKREF=0                                                         |

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

4.**TOOLS:**


The design has been developed using open souce CAD tools .They are:
  
  1.[NGSPICE](http://ngspice.sourceforge.net/download.html)<br />
  2.[MAGIC](http://opencircuitdesign.com/magic/)
  
  ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------
  
5.**PRE-LAYOUT DESIGN AND SIMULATION:**

1.Installl tools<br />
2.Circuit design<br />
3.Netlist extraction<br />
4.Netlist modification for NGSPICE<br />
5.Run

![image](https://user-images.githubusercontent.com/39303205/137882881-f77aac7b-b080-4409-bc72-ea3dcc1610ad.png)

Simulation results:
![image](https://user-images.githubusercontent.com/39303205/137902672-c56d83a1-5bde-47fc-82d1-e5ca8c72458f.png)<br />

![image](https://user-images.githubusercontent.com/39303205/137902737-f8990401-98f3-4973-aed6-a3ef235c9827.png)

