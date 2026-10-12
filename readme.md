# ISAC System OFDM/FDM Waveform Performance Simulation: A Comprehensive Analysis of Theory and Code Implementation [with MATLAB Code]

Personal Blog: https://www.cnblogs.com/EWFrontier  
✿ISAC System OFDM/FDM Waveform Performance Simulation: A Comprehensive Analysis of Theory and Code Implementation ✿In the current research hotspot of integrated sensing and communication (ISAC, Integrated Sensing and Communication) technology, waveform design, as a core component of ISAC system performance, directly determines the comprehensive performance of communication and perception. This article will analyze the core principles of OFDM/FDM waveforms from a theoretical perspective, and combine MATLAB code that can be directly reproduced to fully dissect the BER (Bit Error Rate) performance simulation implementation logic of ISAC-OFDM and ISAC-FDM waveforms. It provides a practical reference for relevant research and engineering practice.  
I. Introduction: The Core Value of ISAC and Waveform Design Integration of sensing and communication into the same hardware platform significantly improves spectral utilization and device integration. OFDM, with its high spectral efficiency and resistance to multipath fading, has become the mainstream waveform in communication systems. On the other hand, FDM, with its flexible waveform flexibility in the sensing dimension, offers advantages. Through MATLAB simulation, this project quantitatively compares the waveform level BER performance of ISAC-OFDM and ISAC-FDM under different SNRs, providing a direct simulation tool chain for ISAC waveform selection.  
II. Core Theoretical Foundation: OFDM/FDM Waveform Principles 2.1 Basic Concepts and Mathematical Model of OFDM  
OFDM's core is to distribute high-speed serial data onto multiple low-speed subcarriers for transmission, eliminating inter-subcarrier interference (ICI) through orthogonality.
(1) OFDM modulation formula: If an OFDM symbol contains subcarriers, with a subcarrier spacing of (for the OFDM symbol period), the time-domain signal of the nth subcarrier is: where the modulation symbols on the nth subcarrier are (such as QPSK, 16QAM).
The time-domain signal of the entire OFDM symbol is the summation of all subcarriers:
(2) OFDM demodulation and BER calculation: The receiver side completes the time-frequency conversion through FFT, recovering subcarrier data. Here, the received signal (including channel fading and additive white Gaussian noise AWGN) is considered.
The calculation logic of BER is: the ratio of the number of error bits to the total number of bits, formula:
Mistake
Compare
Special
Number
Transmit
Output:
Total
Compare
Special
Number
2.2 FDM Waveform Compatibility with ISAC
✧  
For FDM modulation symbols;
✧  
For shaping filtering pulses;
✧  
For the bit period;
✧  
For the central frequency of the first sub-channel.
2.3 ISAC Waveform Performance Core Indicators: BER in the ISAC system, the core performance indicator for communication performance is BER, and its relationship with SNR is as follows: For a BPSK modulated AWGN channel, the theoretical BER formula is:
Logic
On
Among them, the complementary error function is:
III. Project Code Architecture and Functions in-depth explanation of the project code adopts modular design, all scripts can be directly run in MATLAB, core around "simulation execution - result analysis - visualization output" full process, folder and script functions are as follows:
3.1 Overall folder structure (core function division)
Core Features
Key documents
Main/
Independent waveform simulation script (OFDM/FDM)  
main_ISAC_OFDM_waveform.m, main_ISAC_FDM_waveform.m  
Run/
Simulation core function (called by upper-level scripts)  
run_ISAC_OFDM.m, run_ISAC_FDM.m  
Functions/
Lower-layer signal processing / Channel model  
Subcarrier mapping, channel fading, AWGN addition, BER calculation and other tool functions  
Analysis/
Result comparison and visualization  
compare_ISAC_OFDM_FDM.m, expected_ISAC_OFDM_FDM.m  
Outputs/
Simulation result graph storage  
BER-SNR curve (log scale), performance comparison chart  
3.2 Core script functionality and calling method (1) One-click comparison simulation: compare_ISAC_OFDM_FDM.m (key point) This is the most core control script in the project, no need to manually configure paths; it runs automatically after execution, completing the whole process:  
% Directly execute in MATLAB command line/script cd analysiscompare_ISAC_OFDM_FDM\nCore functions:  
✧  
Automatically add folders such as main/, run/, functions/ to MATLAB path;  
✧  
Set a fixed random seed (to ensure reproducibility of simulation);  
✧  
Call ISAC-OFDM and ISAC-FDM simulation functions separately;  
✧  
Draw log scale BER-SNR comparison curves;  
✧  
Automatically save the results to outputs/folder.
(2) Independent Waveform Simulation Functions: run_ISAC_OFDM.m/run_ISAC_FDM.m These two functions are the "computation core" for simulation, and cannot be directly clicked to run. They require input parameters for invocation, with the following input-output logic:
1. ISAC-OFDM Simulation
% Input parameters: gamma (ISAC resource allocation coefficient), SNR_dB (array of signal-to-noise ratios) gamma = 0.8; % 0~1, representing the proportion of communication resources in total resources SNR_dB = [-10 -5 0 5 10 15 20]; % Covering low/medium/high signal-to-noise ratio range BER_OFDM = run_ISAC_OFDM(gamma, SNR_dB);\nFunction internal functionality:  
✧  
Generate random modulation symbols (fixed seed);  
✧  
Complete OFDM modulation (subcarrier mapping, IFFT, cyclic prefix addition);  
✧  
Construct an AWGN channel model, adding noise corresponding to the SNR;  
✧  
OFDM demodulation (remove cyclic prefix, FFT);  
✧  
Bit decision, calculate the BER for each SNR;  
✧  
Return BER array (corresponding to SNR_dB).  
2. ISAC-FDM Simulation
% Input parameters: alpha (FDM subchannel resource allocation coefficient), SNR_dB (array of signal-to-noise ratios) alpha = 0.8; % 0~1, representing the proportion of communication in FDM subchannels SNR_dB = [-10 -5 0 5 10 15 20];BER_FDM = run_ISAC_FDM(alpha, SNR_dB);\nFunction internal functionality:  
✧  
Generate FDM subchannel modulation symbols;  
✧  
Complete FDM shaping filtering and carrier modulation;  
✧  
Channel transmission (AWGN);  
✧
FDM demodulation (matched filtering, symbol decision);  
✧  
Calculate the BER under different SNR and return.  
(3) The script for analyzing the impact of different resource allocation coefficients on BER is used to analyze the effect of different ISAC-OFDM parameters, corresponding to the core chart in the report:  
✧  
main_ISAC_OFDM_waveform.m: Analyze the BER-SNR curve of ISAC-OFDM under different (0.6/0.8/1.0) resources;  
✧  
main_ISAC_FDM_waveform.m: Analyze the BER-SNR curve of ISAC-FDM under different (0.6/0.8/1.0) resources;  
✧  
expected_ISAC_OFDM_FDM.m: Generate theoretical BER trend curves (corresponding to Fig.1).  
Example call (for FDM):  
cd mainmain_ISAC_FDM_waveform\n3.3 Core features of code✧  
Reproducibility: Consistent results are obtained with a fixed random seed;  
✧  
Modular design: Lower-level signal processing functions (such as BER calculation, channel modeling) are encapsulated independently, facilitating modification and extension (e.g., replacing modulation methods, channel models);  
✧  
Visual output: All simulation results automatically generate log scale BER-SNR curves (a standard presentation for communication performance analysis), eliminating the need for manual plotting.  
IV. Simulation Results and Engineering Value 4.1 Simulation output content After running the code, the outputs/folder will generate the following core results:  
✧  
BER-SNR comparison curves of ISAC-OFDM/ISAC-FDM (log scale, intuitively showcasing the anti-interference capability at low SNR);  
✧  
Differences in BER performance under different resource allocation coefficients (/);
Theory of BER and Simulation BER deviation analysis (Verification of the accuracy of the simulation model).
4.2 Key conclusions (based on simulation) ✧
Under the same SNR, ISAC-OFDM has a better BER than ISAC-FDM (the orthogonal subcarrier reduces subchannel interference);
✧
Resource allocation coefficient / is smaller (perceived occupying more resources), the communication BER is worse, reflecting the core characteristic of "communication resource trade-off";
✧
In the low SNR range (<-5dB), both waveforms have a sharp deterioration in BER, with OFDM's fading speed being slower, suitable for low SNR scenarios.
V. Summary and extension directions The project has realized the BER performance simulation of ISAC-OFDM/FDM waveforms through complete MATLAB code, which features "one-click operation, adjustable parameters, and reproducible results", suitable for university research teaching as well as an early verification tool for engineeringized ISAC waveform design.
Extension directions (based on the existing code framework):
✧
Replace modulation method: Change the default BPSK to 16QAM/64QAM, analyze the BER performance under high order modulation;
✧
Introduce channel model: Add multipath fading and Doppler shift (suitable for mobile scenarios);
✧
Perception performance integration: Based on the existing communication BER analysis, add a perception precision (such as distance / velocity estimation error) simulation module.
Appendix: Quick Start Guide 1
Open MATLAB, set the project folder as the current working directory;
2
Run the analysis script:
cd analysiscompare_ISAC_OFDM_FDM\n3
View the outputs/folder, get the BER-SNR comparison graph.
Author's Unit: National Yunlin University of Science and Technology, Department of Electronic Engineering. Core Value: This project code provides a "theoretical-simulation-visualization" full-process tool for waveform performance analysis, allowing core results to be reproduced without complex configurations, thereby facilitating the rapid verification and iteration of integrated tactile-sensing technology.
★

## Images

![ISAC System OFDM/FDM Waveform Performance Simulation: A Comprehensive Analysis of Theory and Code Implementation [with MATLAB Code]](01.jpg)
![ISAC System OFDM/FDM Waveform Performance Simulation: A Comprehensive Analysis of Theory and Code Implementation [with MATLAB Code]](02.jpg)
![ISAC System OFDM/FDM Waveform Performance Simulation: A Comprehensive Analysis of Theory and Code Implementation [with MATLAB Code]](03.jpg)
![ISAC System OFDM/FDM Waveform Performance Simulation: A Comprehensive Analysis of Theory and Code Implementation [with MATLAB Code]](04.jpg)

<!-- PAYMENT_BLOCK -->

## Get this dataset

- Payment link (Stripe): [Buy now](https://buy.stripe.com/3cs8yP7sY87d0vu9AB)
- Payment QR code: ![Payment QR code](pay.png)

<!-- /PAYMENT_BLOCK -->
