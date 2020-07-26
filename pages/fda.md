# FDA

# Introduction

# Schematic of the FDA

## The Fully Differential Amplifier Core
![FDACore](img/FDACore.jpg)   

## The Vcm Feedback Circut
![VCMFB](img/VCMFB.jpg)   

## The Bias Circuit with Start Up
![FDABias](img/FDABias.jpg)   

# System Design

## Specifications
![FDA_Spec](img/FDA_Spec.jpg)  

## Calculation of Unity gain bandwidth
![FDA_ft_Equ](img/FDA_ft_Equ.jpg)  
To minimize the total area, the value of compensation capacitor should be as small as possible. In this design, a MIM capacitor is used. The smallest MIM capacitor is 606.875fF, which the area is 25umx25um. To achieve at least 10MHz unity gain bandwidth, the gm1 should be no less than 3.8 x 10^-5 S.   

## Calculation of slew rate
![FDA_sr_Equ](img/FDA_sr_Equ.jpg)  
The formula shown above determines the minimal quiescent current of M8, which is 1.5uA.   

## Calculation of open-loop gain
![FDA_gain_Equ](img/FDA_gain_Equ.jpg)  
The overall gain of this FDA is achieved by two stage, the first stage is a folded cascode stage and the second stage is a common source stage. To achieve at least 120dB gain, the first stage can be set to achieve 80dB gain and the second stage can be set to achieve 40dB gain. 

## The Devices Parameters
![FDA_Parameter_Mx](img/FDA_Parameter_Mx.jpg)  
![FDA_Parameter_CxRx](img/FDA_Parameter_CxRx.jpg)  

# Simualtion Results and Analysis

# Conclusion

# Return to Homepage
