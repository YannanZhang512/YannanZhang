# 低功耗高精度电压基准   

# 简介   
**本项目实现了一个简单的低功耗高精度电压基准**   

# 设计方法   
## 整体电路   
**带隙电压基准电路图如下图所示：**   
![BandgapSch](img/BandgapSch.png)   
**本项目中的元器件参数:**   
![Parameter](img/bandgapparameter.jpg)  

## 静态电流与工作点设置
为了满足不超过200uW的功耗, 各支路静态电流设置如下:   
![BandgapQuiescentCurrent](img/BandgapQuiescentCurrent.png)  

## 电路参数计算
### 电阻阻值的计算
输出电压Vref和温度系数的表达式如下图所示, 由于 R5=R3, R5'=R3', R4=R2, 为了简化公式, 令R1=R1, R2=R2, R3=R3//R3'.   
![BandgapVoutEuqation](img/BandgapVoutEuqation.jpg)  

在上述公式中的第二个公式中，最后一项表征电阻温度系数的影响。在本设计中, 我使用了HRP poly电阻, 根据数据手册所示，其温度系数如下所示:   
![BandgapResistorTco](img/BandgapResistorTco.jpg)   

为了实现尽量低的温漂，参考数据手册中的值，电阻取值必须满足如下条件:   
![Bandgap_Resistor](img/Bandgap_Resistor.jpg)   

由于T1，T2的静态电流均设置为10uA, 同时有如下关系:   
![Bandgap_CurrentEqu](img/Bandgap_CurrentEqu.jpg)   

能够计算出R1的值大概为5.4065k. 2segments，W=2u, L=5u的HRP poly 电阻是5.3525k, 根据此值可以决定其余所有电阻值。   

# 仿真结果与分析   
## 输出电压与温度的关系
![VoutVSTemperature](img/VoutVSTemperature.jpg)   
从仿真结果上看, 输出的基准电压随温度的变化很符合带隙基准的特性，同时也比较稳定，但是当VDD=5V时是例外。 当电源电压变化时，输出电压也变化。这是由于电源电压变化时，放大器的开环增益同样变化（我把详细的分析放在设计经验里了）。当电源电压从3V开始增加，放大器的开环电压增益同样增加，输出电压同样向着理论计算值增加（开环增益增加，等效失调电压减小）。开环电压增益在电源电压为3.5~4.0V时达到最大值，然后当电压继续升高时，开环电压增益反而下降，因而输出电压下降。   

# 设计经验  
+ ***Vbe的温度系数并不一定是-2mV/K***   
Vbe可以由以下公式计算:   
![VbeFormula](img/VbeFormula.jpg)  
从公式中看出，Vbe的温度系数与工艺和偏置电流相关，在本项目中使用的工艺库为 SMIC's 130um工艺, 我仿真了Vbe的温度系数，结果如下:   
![Vbe](img/Vbe.jpg)  
***Vbe的温度系数会随着偏置电流的改变而改变，同时也与工艺相关。***   

+ ***运算放大器的开环电压增益受直流工作点影响***   
1. 运算放大器的输出电压可以由以下公式表示:   
![BandgapVampoutEqu](img/BandgapVampoutEqu.jpg)   
**最后两项基本是常数, 所以运放的输出将随着VDD的增加而增加**   
2. 运放的开环电压增益表达式如下:   
![Bandgap_OpenLoopGainEqu](img/Bandgap_OpenLoopGainEqu.jpg)   
**当VDD从3V增加时, 运放的输出同时增加，M6的漏源电压VDS也增加。由于M6的漏源电压VDS也增加, M11的漏源电压 |VDS|则减小。漏源电压的增大会导致更大的输出电阻ro, 所以由M7和M6构成的共源共栅结构的输出电阻将增加, 但由M11和M9构成的共源共栅结构的输出电阻将减小（减小程度不大）, 总的输出电阻则是增加的, 因此开环电压增益增加。当VDD继续增加，超过4V之后，M6的漏极电压将更大（在2V以上）, M6的衬底漏电将产生显著影响并大幅降低输出电阻，总增益就减小。**   
3. 为了证明以上分析, 利用仿真提取了一下参数进行实际分析.   
![Bandgap_GainVSOp](img/Bandgap_GainVSOp.jpg)   
在上表中，橙色的单元格代表M3, M7 and M6构成的cascode的输出电阻; 绿色的单元格代表M9 and M11构成的cascode的输出电阻。 黄色的单元格代表由M6衬底漏电形成的等效输出电阻。当VDD增加时，VD6增加，ro6显著增加所以开环电压增益增加。但是当VDD超过4V后，M6的衬底漏电影响显著，导致输出电阻下降，因此开环电压增益降低。      


+ ***启动电路***   
在整个电路的设计中，开始我对启动电路的理解还较浅，觉得参考书上的启动电路应该就可以，但后来发现启动电路有很多值得深思的地方。启动电路必须要能够可靠稳定地启动整个电路，并帮助带隙基准建立合适的静态工作点。下图所示是本项目中使用的启动电路（使用红色线标注）。   
![BandgapStartup](img/BandgapStartup.png)   
之前版本的启动电路如下图所示（即去掉M27）。这个版本的启动电路不能成功启动带隙基准，下面进行详细分析：   
**电路上电后，输出电压Vref=0，M24和M25构成的反相器的输出为高电平，所以M26开启，并将B点拉低。流过M12和M26的电流用Istartup标注。B点电压为 VDD - |VTHP + Vov12|, 由于VTHP大越是-0.7V, Istartup电流较大, 所以B点电压应不大于VDD - 1V。 第二点，无论A点电压为多少, M14的漏极电流 (Id14) 要小于M15的漏极电流 (Id15), 原因在于 Vgs14 < Vgs15。因此，VIP电压大于VIN。由于运算放大器的同相输入端比反相输入端的电位高，运算放大器将会饱和，输出为最大电压，因此A点电压为VDD - |VDS9|, 此电压比B点高，M14关断。由于M14一直关断，因此带隙基准不能工作。为了解决这个问题，需要利用启动电路把A点同时拉低，可以通过增加M27实现。**   
![BandgapStartupPreAna](img/BandgapStartupPreAna.png)   

# 返回主页
[返回主页](https://yannanzhang512.github.io/YannanZhang/pages/index_cn.html)
