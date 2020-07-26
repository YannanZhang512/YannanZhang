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

## Calculation of power dissipation
The whole circuit consists of three parts, FDA circuit, CMFB circuit and bias circuit. We expect the total power dissipation is no more than 200uW. Since we have known that the drain current of M8 should not be less than 1.5uA, thus we can determine the dc operating point of the whole circuit, which is shown below:   
![FDA_Current](img/FDA_Current.jpg)  

The total current is 35uA, under 3.6V supply voltage, the total power dissipation is 126uW, which is less than 200uW. Although we can increase the current of each branches, since there is a lot of room to do this. But the bias circuit cannot generate any value of current easily, because the current of bias circuit is determined by the resistor, and the resistor cannot set to any value easily. So, in order not to exceed the maximal 200uW power dissipation, we don't need to change the settings.   

## Calculation of common-mode input and output range
The calculation formulae are shown below. VTHN is about 700mV, so the overdrive vlotage of M1, M3 and M4 is about 100mV, so that the minimal input voltage is 1V. Since VTHN is usually larger than overdrive voltage, the maximal input voltage can slightly exceed VCC. The output voltage range is between VSS+Vov15 and VCC+Vov13, so the overdrive voltage cannot exceed 0.2V to meet the requirements.   
![FDA_cmV](img/FDA_cmV.jpg)  

## The Devices Parameters
According to the prior analysis with the help of gm/ID method, the devices parameters can be calculated, which are shown as follow:   
![FDA_Parameter_Mx](img/FDA_Parameter_Mx.jpg)  
![FDA_Parameter_CxRx](img/FDA_Parameter_CxRx.jpg)  

# Simualtion Results and Analysis

## DC opreating point
![FDA_DCop](img/FDA_DCop.jpg)  
The DC operating points of the circuit are shown above. The real operating point of the circuit has increased about 8%, this is due to the inaccuracy of the resistor as well as channel length modulation effect. The real power dissipation is 138.6uW, which still meet the requirements.    

## Open-loop gain
![FDA_openLoopFig](img/FDA_openLoopFig.png)  

## Input common mode voltage

## Output common mode voltage

# Conclusion

# Return to Homepage
