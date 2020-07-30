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
The above figure shows the results of the FDA's open loop characteristics. The DC open-loop gain is about 127dB, the unity gain bandwidth is 15.0284MHz. Phase margin is 76deg and gain margin is 22.4dB.    

## Step response
![StepResponseTesting](img/StepResponseTesting.png)  
The step response is tested using the above circuit. FDA is configured to have unity gain, and a large swing input pulse is used as stimuli. The following figure shows the step response of the FDA. The output has a 8.2V/us slew rate. Since ID8 is 2.7uA and the compensattion capacitor C1 is 606.875fF, the calculated slew rate is 8.89V/us, which is consistent with the simulation results.   
![FDA_StepRespnoseFig](img/FDA_StepRespnoseFig.png)  

## Input common mode voltage
![TestingSchInputVCM](img/InputVCMTesting.png)  
The input common mode voltage range is tested using the above circuit. V1, E1 and E2 form a differential voltage source, it outputs a 1V differential voltage. R1~R4 are used to set the gain of FDA to 1, thus, the differential output voltage of FDA should be 1V if it works properly. The VIN and VIP pins have same voltage, their voltage are 0.5(V3 + V3). Since V3 is fixed to 1.8V, which is the output common-mode voltage, by scanning V2 and observing the differential output, we can find the input common mode voltage range. The following figure shows the simulation results, the FDA can be functional when the input common mode voltage is as low as 0.7V, but this is not the valid input common mode voltage because under this condition, M3 and M4 have already entered in to triode region. The lowest possible voltage that both M1, M2, M3 and M4 are all working in saturated region is 0.9V, so the input common mode voltage range is 0.9+VSS ~ VCC.   
![FDA_VinCMFig](img/FDA_VinCMFig.png)  

## Output common mode voltage
![OutputVCMTesting](img/OutputVCMTesting.png)  
The output common mode voltage range is tested using the above circuit. V1 changes from -3.6V to +3.6V, the differential output is the output common-mode voltage range. The maximal output voltage range is determined by the overdrive voltage of M13, M14, M15 and M16. The overdrive of M13 and M14 are about 119mV, while M15 and M16's overdrive voltage are 90mV. That means the maximal output voltage range is VCC-0.12 ~ VSS+0.09. The simulation result is shown below, and it comply with analysis.   
![FDA_VoCMFig](img/FDA_VoCMFig.png)   

# Conclusion

# Return to Homepage
