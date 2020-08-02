# A 500MHz bandwidth AM receiver with 54dB input dynamic range

# Introduction 
![AM_Picture](img/AM_Picture.jpg)   
**This AM receiver was designed by me during the National Undergraduate Electronic Design Contest, it won the first prize. The input power range is from -101dBm to -47dBm, input frequency range is from 30MHz to 510MHz. Output bandwidth is from 300Hz to 5KHz.**   

# System Block diagram
The system block diagram is shown below:      
![am_blockdiagram](img/am_blockdiagram.jpg)  

# Design of the system
## Low noise amplifier
The performance of low noise amplifier is of great importance, since it determines the overall SNR of the system. To achieve the lowest possible NF, the low noise amplifier should have high gain and low noise figure. Qorvo's SPF5189Z was used there, its noise figure can be as low as 0.5dB, with 20dB power gain.   
![spf5189z_data](img/spf5189z_data.jpg)  
It is noticeable that the Output P1dB is 22.3dBm at 0.8GHz, and the AM receiver is required to accept -47dBm input power. That means, if we want to cascade multiple SPF5189Z stages, the overall gain should not exceed 22.3+47 = 69.3dB, which are three stages. To achieve best linearity, two stages are reasonable, because the maximal output of LNA is 0dBm, we can expect the circuit do not product much distortion.   

## Mixer
![AD831_data](img/AD831_data.jpg)  
The mixer AD831 was the only device that I had during the contest, since the maximal working frequency of AD831 is 500MHz, so upper frequency limit of the AM receiver cannot exceed this value too much, which is 510MHz. It is expected to have a larger input frequency range if the mixer can be replaced with a better one.   
The 1dB compression point of AD831 is 10dBm, the maximal input power of AM receiver is -47dBm, so the overall gain before mixer cannot exceed 57dB. Two stages of LNA contributes 40dB gain, a bandpass filter contributes -1.5dB, so the overall gain before mixer is 38.5dB, which is suitable. 
The next consideration of mixer is its minimal LO driving power. The official data shows the minimal input power of LO port is -10dBm, as shown below, and the maximal output power of PLL is 5dBm, so the mixer can work happily.   
![AD831_Lo](img/AD831_Lo.jpg)  
![ADF4351_Output](img/ADF4351_Output.jpg)  

## Phase Locked Loop   
The phase locked loop is implmented using ADI's ADF4351. ADF4351 is a wideband synthesizer with integrated VCO. Its output frequency range is from 35MHz to 4400MHz. Since the IF in this particular system is 10.7MHz, in order to have a 30MHz to 510MHz input frequency range, the PLL should have a output frequency ranging from 40.7MHz to 520.7MHz and ADF4351 is suitable for this application.   
The schematic of ADF4351 is shown below:   
![ADF4351sch](img/ADF4351sch.jpg)   
The layout of ADF4351's pcb is shown below, to reduce the noise, enough decoupling capacitor should be used and the digital ground and analog ground should be split. Besides, two ultra-low noise LDO TPS79633 are used to power the digital and analog part.   
![ADF4351PCB_ToP](img/ADF4351PCB_ToP.jpg)  
![ADF4351PCB_Bottom](img/ADF4351PCB_Bottom.jpg)  

## IF Filter
The IF in this system is set to 10.7MHz, since many high performance commercial products are available. In this AM receiver, muRata's SFECV10M7KA00 is used. The electrical characteristics are shown below:   
![IFFilterParameter](img/IFFilterParameter.jpg)  
**Since the input/output impedance of SFECV10M7KA00 is 330ohm, to connect with 50ohm system, a matching network should be added to reduce input loss**, the matching network is shown below:   
![matchingnetwork](img/matchingnetwork.jpg)  

## Auto Gain Control Circuit
The schematic of AGC is shown below. A voltage-controlled gain amplifier VCA810 is used to amplify the input signal. The peak detector formed by high-speed comparator AD8561 is used to detect the peak value of output signal, then the output of peak detector is used to control the VCA810, so that the output is stable.   
![AGCSch](img/AGCSch.jpg)  
A single stage of AGC has over 30dB dynamic range, although higher range is achieveable, it could increase the distortion and noise. Since it's required the AM receiver should have 54dB input dynamic range, so two cascade AGC stage are required. The first AGC(X8) stage is used to stablize the IF signal, the second AGC stage is used to stabllize the LF signal.   

# Designing Experience
## Matching Consideration of the IF Filter
The input/output impedance of SFECV10M7KA00 is 330ohm, to connect with 50ohm system, it's required to have a matching network. Although 10.7M is not too high and in most applications, there is no need to matching it into 50ohm, but to reduce the input loss of the filter, it's better to add a matching network. Following figure shows the purpose of the matching network.   
![IFFilter_Matching](img/IFFilter_Matching.jpg)  
If there is no matching network, the input loss of the filter is 12dB, while it is only 6dB if the matching network is added. So to reduce the input loss as well as increase the dynamic range, the matching network should be added.   

## Considerations about the power supply
In this project, multiple power supply is needed. The LNA needs 5V single power supply, the mixer needs 9V single power supply. The 5V VCC is provided by a switching power supply that converts 12V to 5V.  Since switching power supply is noisier than LDO, so some measures should be taken to reduce the output noise. Following figure shows the output of LNA when there are no noise reducing circuit.   
![PowerNoise](img/PowerNoise.jpg)  
The waveform is "thick" because the switching noise of the power supply has coupled into the signal path. To reduce the power supply noise, a pi filter can be applied, as shown below, and the power supply will be clear enough.   
![PiFilter](img/PiFilter.png)  

## Be careful of the oscilloscope probe
In order to measure the bandwidth of the LNA, I used the RF signal generator and oscilloscope to get a rough estimation. But I soon found the bandwidth was so small, about 150MHz. But the datasheet says it should have more than 500MHz bandwidth. After some analysis, I found that's because the probe has input capacitance of tens of pF, it forms a lowpass filter with LNA’s output resistance. The probe has 13pF capacitance, the wire as well as other parts has about few pF, so the total capacitance is about 20pF. The output resistance of LNA is 50ohm, so the bandwidth is limited to 159MHz, which comply with the measurement. One solution is to trun on the oscilloscope's input matching function so that the input resistance of oscilloscope is 50ohm, then the input capacitance of the oscilloscope can be reduced to less than 1pF. The another solution is to use a network analyzer to measure the bandwidth. ***Always remember the input capacitance thing of the oscilloscope.***   

# Returen to Homepage
