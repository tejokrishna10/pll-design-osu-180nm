# PLL-design-OSU-180nm
This repository presents design of on-chip clock multiplier(8X PLL) using open source EDA tool OSU 180nm 

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------

**Table of Contents:**

1.[INTRODUCTION TO ON-CHIP CLOCK MULTIPLIER](#-INTRODUCTION-TO-ON--CHIP-CLOCK-MULTIPLIER)<br />
2.[THEORY](#-THEORY)<br />
3.[SPECIFICATION](#-SPECIFICATION)<br />
4.[TOOLS](#-TOOLS)<br />
5.[PRE-LAYOUT DESIGN AND SIMULATION](#-PRE--LAYOUT-DESIGN-AND-SIMULATION)<br />
6.[POST-LAYOUT DESIGN AND SIMULATION](#-POST--LAYOUT-DESIGN-AND-SIMULATION)<br />
7.[SCOPE](#-SCOPE)<br />
8.[CONCLUSION](#-CONCLUSION)<br />
9.[REFERENCES](#-REFERENCES)


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


Phase-detector : Based on the feedback from the frequency divider it creates two signals ,up and down which are given to the charge-pump<br />
Charge pump : Charge-pump consists of power MOSFETS it helps in better charging of the capacitors present in the next stage which is a LPF<br />
LPF : LPF is used for smoothning the waveform and get a dc value<br />
MUX : Here MUX is used to select between VCO only mode or PLL<br />
VCO : VCO is used to get the output frequency based on the input DC value<br />
Frequency divider :Here a basic D-Filp-flop based counter is used to get frequency division

**Operation of feedback-loop
control**




![image](https://user-images.githubusercontent.com/39303205/137938353-6c471bab-a2b0-465d-89a5-f5a2d62cca57.png)



![image](https://user-images.githubusercontent.com/39303205/137938240-ee6d070c-6f8b-4922-b057-28f600afe425.png)




As shown above we consider a second-order feed back systesm , the response can be as shown below based on location of poles



For PLL we should obtain a critically damped response as it has less oscillations and its fast.

NETLIST FROM ESIM



![image](https://user-images.githubusercontent.com/39303205/137939973-b7fae254-1698-4ee8-8e67-29734f617146.png)


NETLIST FOR NGSPICE




![image](https://user-images.githubusercontent.com/39303205/137940041-fa6ebfd8-5a70-4f80-85b4-39bf7c002e69.png)



RUNNING NGSPICE IN TERMINAL



![image](https://user-images.githubusercontent.com/39303205/137940479-1f873fc9-ad04-4187-ab59-8d026d22a14f.png)




![image](https://user-images.githubusercontent.com/39303205/137940603-e1c83013-cb83-483a-9695-b705b64c250c.png)


PHASE DETECTOR



RUNNING IN NGSPICE


![image](https://user-images.githubusercontent.com/39303205/137941185-9d13b04b-d0b6-476d-90ee-d03433125ee6.png)




![image](https://user-images.githubusercontent.com/39303205/137941310-6efdd7e6-87eb-4495-804a-f26a57918628.png)




Simulation results:













![image](https://user-images.githubusercontent.com/39303205/137902672-c56d83a1-5bde-47fc-82d1-e5ca8c72458f.png)<br />






![image](https://user-images.githubusercontent.com/39303205/137902737-f8990401-98f3-4973-aed6-a3ef235c9827.png)

------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

6.**POST-LAYOUT DESIGN AND SIMULATION:**



1.**Phase Frequency Detector**


![image](https://user-images.githubusercontent.com/39303205/137926589-c6f8a0a1-94dc-4306-933b-1cabae392fa2.png)<br />





![image](https://user-images.githubusercontent.com/39303205/137926643-173615aa-d783-446c-a4f9-9e9e0f628fae.png)<br />




2.**2-1 MUX**




![image](https://user-images.githubusercontent.com/39303205/137942010-629608c2-27b7-420d-90b1-19fa746e319c.png)






![image](https://user-images.githubusercontent.com/39303205/137926841-909b7e0d-fdc7-4da1-8942-a67687d84eaf.png)<br />











![image](https://user-images.githubusercontent.com/39303205/137926958-3bec1952-f86c-4f6f-a117-64e082872032.png)<br />








3.**FREQUENCY DIVIDE BY 8**







![image](https://user-images.githubusercontent.com/39303205/137927233-0c15d577-404b-4bf6-9389-0b0c544c247c.png)<br />









![image](https://user-images.githubusercontent.com/39303205/137927331-0a6542c2-51c0-478a-9ddc-cdef8bf2b3a6.png)<br />








4.**PLL**



![image](https://user-images.githubusercontent.com/39303205/137942353-c508a128-86fd-4536-b4db-d5ab886ad867.png)




![image](https://user-images.githubusercontent.com/39303205/137942567-a63a5051-b8e3-4443-a21d-893d4ee12f0c.png)






![image](https://user-images.githubusercontent.com/39303205/137927575-7ddd9719-f171-48fe-bdad-870013230a29.png)<br />







------------------------------------------------------------------------------------------------------------------------------------------------------------------------------



7.**SCOPE:**

1.Porting this IP on lower technology nodes using advance PDK's where capacitor fabrication is realizable<br />
2.Area Efficient Design Improvements.<br />
3.Improvements for Power Reduction.<br />
4.Improvements of accuracy, jitter & dead zone.<br />


----------------------------------------------------------------------------------------------------------------------------------------------------------------------------


8.**CONCLUSION:**

I have learnt the flow of designing a PLL and how to design a system from lower block to higher blocks.



-------------------------------------------------------------------------------------------------------------------------------------------------------------------

9.**REFERENCES:**

1.https://github.com/parasgidd/avsdpll_3v3<br />
2.VLSI system design pvt ltd tutorial sessions











