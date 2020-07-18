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

# Return to Homepage   
