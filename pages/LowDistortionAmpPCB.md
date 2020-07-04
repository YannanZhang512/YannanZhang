# About this project   

*This project was started in June. 2017, so some of the original figures are missing.* This project was intended to **find out a better way to layout a high speed operational amplifier**, this is of paramount importance because high speed opamp can be used in many applications and they serve to build the signal chain. If the signal after being amplified by the opamp are distorted, then the whole system cannot have a good performance.    
A careless and perfunctory layout can lead to high distortion. I realized this problem when I was using a TI's high speed opamp **THS3201** to amplify a 20MHz small signal. The input signal was provided by a signal generator, the output signal after being amplified was being examined by a oscilloscope.   
![10M_worstCase](img/10m_worst_case.png)   

The waveform was really ugly, so I decided to find out the reason and solution.   

# Possible reason   

At first, I have no idea about the cause of the problem, I asked many people, including some professors and experts but no one could give me an answer. So I had to think of it by myself.   

## Impedance matching problem?   

## Layout problem?   

The original layout was shown below. All the important signal paths are shown.   

![Original_Layout](img/original_layout.png)   

In order to find out if the feedback signal path is the culprit, I arranged the feedback resistors in four different ways to form four different feedback paths.   

+ ***The first layout.***   

   The first layout is same as the original design, the feedback signal path is also the same.   

   ![First_layout](img/first_layout.jpg)   

+ ***The second layout.***   

   The second layout changed the direction of R1, as shown in figure.   

   ![Second_layout](img/second_layout.jpg)   

+ ***The third layout.***   

   The third layout moved the R1 to the top layer. Actually, the third layout is same as the second layout, but its feedback signal path ends on the top layer of PCB.   

   ![Third_layout](img/third_layout.jpg)   

+ ***The fourth layout.***   

   The fourth layout also moved the R1 to the top layer. Besides, the R1 was arranged in a way so that the feedback signal path and input signal path ends at the same point.   

   ![Fourth_layout](img/fourth_layout.jpg)   

# Measurement Results   

## Input frequency = 10M, input power = 3dBm   

+ ***Waveform***   
![10M_waveform](img/10m_waveform_combined.png)   
+ ***Spectrum***   
![10M_spectrum](img/10m_spectrum_combined.png)  

## Input frequency = 50M, input power = 3dBm
+ ***Waveform***   
![50M_waveform](img/50m_waveform_combined.png)   
+ ***Spectrum***   
![50M_spectrum](img/50m_spectrum_combined.png)  


# Conclusion      

**The 4th layout is the best layout, that means, the feedback signal path and the input signal path should end at the same point.**    

# The final version of layout   

![Final_Layout_2D](img/finallayout2d.jpg)   
![Final_Layout_3D](img/finallayout3d.jpg)  
