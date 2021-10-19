# PLL-design-OSU-180nm
This repository presents design of on-chip clock multiplier(8X PLL) using open source EDA tool OSU 180nm 

**Table of Contents:

1.[INTRODUCTION TO ON-CHIP CLOCK MULTIPLIER](#-INTRODUCTION-TO-ON--CHIP-CLOCK-MULTIPLIER)<br />
2.[THEORY](#-THEORY)

1.**INTRODUCTION TO ON-CHIP CLOCK MULTIPLIER:**

The repository contains simulation files and other relevant files for on-chip clock multiplier using PLL(Fclock-in:5MHZ-12MHz ;Fclock-out:40MHz-100MHz at 1.8V)IP.
The goal is to design on-chip clock multiplier using OSU-180nm technology node.The on-chip clock multiplier is present in almost all synchronous processors.

2.**THEORY:**

A phase-locked loop (PLL) uses a reference frequency(Fclock-in) to generate a multiple of that frequency. A voltage controlled oscillator (VCO) is initially tuned roughly to the range of the desired frequency multiple. The signal from the VCO is divided down using frequency dividers by the multiplication factor. The divided signal and the reference frequency are fed into a phase comparator. The output of the phase comparator is a voltage that is proportional to the phase difference. After passing through a low pass filter and being converted to the proper voltage range, this voltage is fed to the VCO to adjust the frequency. This adjustment increases the frequency as the phase of the VCO's signal lags that of the reference signal and decreases the frequency as the lag decreases (or lead increases). The VCO will stabilize at the desired frequency multiple. This type of PLL is a type of frequency synthesizer.

Moderm microprocessors have 2GHz-5GHz clock frequencies whereas quartz oscillator can produce only few MHz ,so to achieve high frequency clock signal from low-frequency clock source we are designing PLL IP block and simulating it in this repository.


