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
+ ***Data***
*The Unit is dBm.*
| Layout | HD1  |  HD2  |  HD3  |  HD4  |  HD5  |  HD6  |  HD7  |  HD8  |  HD9  | HD10  |
| :----: | :--: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: | :---: |
| first  | 16.5 | -33.8 | -36.0 | -35.0 | -33.8 | -37.0 | -38.0 | -39.5 | -40.0 | -41.5 |
| second | 16.5 | -33.6 | -36.0 | -37.0 | -35.0 | -38.0 | -44.0 | -39.0 | -40.5 | -40.0 |
| third  | 16.5 | -37.0 | -38.5 | -41.0 | -41.5 |   0   |   0   |   0   | -45.0 |   0   |
| fourth | 16.5 | -40.0 | -38.5 | -45.0 | -45.2 |   0   |   0   |   0   |   0   |   0   |

## Input frequency = 50M, input power = 3dBm
+ ***Waveform***   
![50M_waveform](img/50m_waveform_combined.png)   
+ ***Spectrum***   
![50M_spectrum](img/50m_spectrum_combined.png)  
+ ***Data***
*The Unit is dBm.*
| Layout | HD1  |  HD2  |  HD3  |
| :----: | :--: | :---: | :---: |
| first  | 16.4 | -18.3 | -21.4 |
| second | 16.4 | -20.0 | -22.6 |
| third  | 16.4 | -25.6 | -21.8 |
| fourth | 16.4 | -29.6 | -21.0 |


# Conclusion      

**The 4th layout is the best layout, that means, the feedback signal path and the input signal path should end at the same point.**    

# The final version of layout   

![Final_Layout_2D](img/finallayout2d.jpg)   
![Final_Layout_3D](img/finallayout3d.jpg)  
