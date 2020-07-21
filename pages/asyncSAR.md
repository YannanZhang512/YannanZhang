# AsyncSAR ADC

# Introduction

# Circuit Implementation
## D Flip-Flop
### Elimination of the output glitches
In SAR ADC, D Flip-Flop is often used to generate proper logic. Traditional D Flip-Flop is slow and power-hungry. To achieve low propagation delay and high speed, TSPC D Flip-Flop is used in this project. However, traditional TSPC DFF has the problem of output glitches, as shown below.   
![OutputGlitches](img/OutputGlitches.png)  
The output glitch may cause wrong logic states. By coupling through any possible paths, the output glitch of traditional TSPC can add extra noise into the circuit. To eliminate the output glitches, I proposed a glitch-free TSPC DFF as shown below. (Few months later, I found this schematic has already been proposed in a patent by Piguet in 1974).   
![Fig_1](img/SARFig_1.jpg)  
Fig.1 (a) shows the schematic of traditional TSPC DFF, it have output glitches when D=0 and CLK is going through a low to high transition. To eliminate the output glitches of traditional TSPC DFF, transistor M10 has been added into the circuit so that the improved version of TSPC DFF is glitch-free. The schematic of glitch-free TSPC DFF is shown in Fig.1 (b).   
![Fig_2](img/SARFig_2.jpg)  
Fig.2 shows the waveform of two DFF, including input stimuli and output response. Fig. 2 (a) is obtained when VDD=3.6V, the output of glitch-free TSPC DFF is same as that of traditional TSPC DFF. But the output of traditional TSPC DFF has many glitches when output is low, while the output of glitch-free TSPC DFF is clear. Fig.2 (b) is obtained when VDD=1.2V, the output of glitch-free TSPC DFF is not same as that of traditional TSPC DFF. The detailed waveforms of two DFF with a time span from 75ns to 100ns when VDD=1.2V is shown in Fig. 3. When t=80ns, the clock and D is changing from low to high, so the output of DFF should be low. But according to the result, the output of traditional TSPC DFF is changing from low to high at this time, which is wrong. At low power supply, traditional TSPC DFF cannot behave correctly while glitch-free TSPC DFF is still functional.   
![Fig_3](img/SARFig_3.jpg)  
### The reset logic of TSPC DFF
The traditional TSPC DFF with reset logic is shown in Fig.4.   
![Fig_4](img/SARFig_4.jpg)  
However, the reset logic is not reliable, because the floating point (the drain of M4 and M5 is not being properly reset when D=1 and CLK=1. Fig.5 shows the simulation result. At t= 95ns, RSTn is changing from low to high, the Q is expected to remain low, but the result shows a quite different result.   
![Fig_5](img/SARFig_5.jpg)  
To improve the reliability of the reset logic, a glitch-free TSPC DFF with modified version of reset logic is shown in Fig.6.   
![Fig_6](img/SARFig_6.jpg)  
Here, M14, M15 and M16 are added to properly reset another floating point, the simulation result shows the glitch-free TSPC DFF with modified version of reset logic can be properly reset, as shown in Fig. 7.   
![Fig_7](img/SARFig_7.jpg)  


## Dynamic Comparator

# Return to Homepage
