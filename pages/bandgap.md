# Bandgap   

# Introduction   
**This project was to learn the basic architecture and design method of a bandgap reference.**   

# Design Method   
## Schematic of the design   
**The Schematic of the bandgap is shown below:**   
![BandgapSch](img/BandgapSch.jpg)   
**The design parameter of the bandgap is shown below:**   
![Parameter](img/bandgapparameter.jpg)   

# Simulation Results and Analysis   

# Layout   

# Conclusion   

# Designing Experience   
+ ***The temperature coefficient of Vbe is not always about -2mV/K***   
The Vbe can be expressed as follow:   
![VbeFormula](img/VbeFormula.jpg)  
From the formula, we can find that the temperature coefficient of Vbe depend on process and current. Using SMIC's 130um process, I simulated the Vbe vs Temperature, the results are shown below:   
![Vbe](img/Vbe.jpg)  
***The temperature coefficient of Vbe can be different when different current pass through the BE junction, as shown in the results.***   

+ ***The open-loop gain of operational amplifier can be affected by the dc operation point***

+ ***Start-up Circuitry***
The start-up circuit should be stable and reliable, and make sure the start-up circuit can help the whole circuit build stable operating point. The start-up circuit in the bandgap is shown below, using red line.   
![BandgapStartup](img/BandgapStartup.jpg)   
The previous version of the start-up circuit is shown below (without M27). This version of start-up circuit cannot start the bandgap successfully. The detailed reasons are as follow: at first, Vref=0, so M24 and M26 pull B to the VDD - |(VGS12 + Vov12)|, since M12 is saturated.   
![BandgapStartupPre](img/BandgapStartupPre.jpg)   

# Return to Homepage   
