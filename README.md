# 3-智慧农业背景下对温湿度等生态环境因子的监测以及应用

项目名称：
智慧农业背景下对温湿度等生态环境因子的监测以及应用

| 姓名 | github ID |
| :--- | :--- |
| 刁政新 | mar7788 |
| 李宏钊 | HongZhao-Li |
| 郭沛兴 | ccgpx |
| 戴瑞 | QWERTY |
| 何津锋 | Discalrise |
| 李晨鸣 | salasd123 |

需求分析

目前智慧农业在世界各国建设发展的如火如荼。一些起步较早的国家，政策支持、科技研发、创新科技应用方面都早已大规模展开并快速发展。现在一些农业发达国家的智慧农业都已达到世界领先水平，因地适宜创新的现代化农业发展模式也已形成并在日益完善，精准生产管理、节约人力物力资本、提高产能和质量也都在逐渐实现。

智慧农业是在现代信息技术革命的红利中探索出来的农业现代化发展的新模式，是集集约化生产、智能化远程控制、精细化调节、科学化管理、数据化分析和扁平化经营于一体的农业发展高级阶段。智慧农业是智慧农业产业链，是现代信息技术与农业生产、经营、管理和服务全产业链的“生态融合”和“基因重组”，可以从生产、营销、销售等环节彻底升级传统的农业产业链，提高效率，改变产业结构。智慧农业以智慧生产为核心，智慧产业链为其提供信息化服务支撑。即使农业全产业链中的营销、物流、消费成为智慧农业生产的可靠的信息支撑网络，引导农业生产信息化决策、高效化生产、差异化服务。

从现实来讲，农民在新的时代往往无法跟上技术的变革，导致农业生产效率大打折扣。

一、问题定义
  
  当前智慧农业领域运用大数据的先进技术对农业主要生产领域在生产过程中采集的大量数据进行分析处理，同时对农业主要环境影响因子如:土壤、大气、水质、气象等进行实时全面检测，从而可以为农业生产提供精准的农资配方，在管理方面也朝着智慧化方向发展，对设施进行准确控制，增加农民的收入，农业也得到发展。
  
  我们组研究的问题经过讨论确定为在农业生产中温度、空气湿度、酸碱度等生态环境因子的监测。在农业生产领域运用农业大数据，可以在传感的各种节点（譬如图像、二氧化碳、土壤中的水分、环境的温度和湿度等）以及在无线通信网络方面，对农业大数据进行管理，使其完整地采集数据、传输数据、存储数据、处理数据，保障农业生产在种植方面的精确性，实施管理可视化、决策明智化。
  
  我们的团队基于实际考虑，计划利用温湿度测量有关的温湿度传感器和Arduino等相关软件结合工程实训所学习的内容进行检测方面的设计，以期最大化的实现对农作物生长状况的检测。



二、概念设计

| 评估标准 |  | 基于ESP32+SX278实现的温湿度监测与信息汇总模块 |  | 土壤湿度不足时自动浇水模块 |  | 自动报警功能 |  |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
|  |  | 权重 | 评分 | 权重×评分 | 评分 | 权重×评分 | 评分 | 权重×评分 |
| 成本 |  | 0.25 | 85 | 21.25 | 80 | 20 | 82 | 20.5 |
| 测量准确性 |  | 0.20 | 90 | 18 | 78 | 15.6 | 82 | 16.5 |
| 用户操作难度 |  | 0.20 | 80 | 16 | 80 | 16 | 80 | 16 |
| 产品使用周期 |  | 0.15 | 76 | 11.4 | 84 | 12.6 | 80 | 12 |
| 设计难度 |  | 0.20 | 72 | 14.4 | 85 | 17 | 85 | 17 |
| 总计 |  | 1 |  |  |  |  |  |  |

运作原理：

本产品秉持模块化设计原则，将上述功能分为两个独立模块分别运作。电源采用USB供电的方式，可以使用不同设备如充电宝进行供电。

三、详细设计

自动浇水部分：

该部分由5V水泵，继电器，以及土壤湿度模块和电阻式土壤湿度传感器构成。当传感器探头悬空时，三极管基极处于开路状态，三极管截止输出为0；当传感器插入土壤中时，由于土壤水分含量不同，土壤的电阻值也不同，三极管基极提供了大小变化的导通电流，三极管集电极到发射极的导通电流受到基极控制，经过发射极的下拉电阻后转换为电压。

土壤湿度模块原理图：

通过灵敏度调节电位器，我们就可以选择合适的湿度阀值，当土壤湿度低于阀值时，DO口输出高电平，反之输出低电平。该模块的AO口也可以与AD模块相连以获取精确的湿度数值。
该模块工作电压为DC3.5-5V，为了同时给水泵供电选择5V电压。

土壤湿度模块接口图：

土壤模块输出的开关信号再接入继电器，就可以实现继电器的开和闭。将水泵的供电线串联继电器之后，土壤湿度低于一定阀值就可以自动打开水泵进行浇水了。

信息汇总与报警部分

利用ESP32+SX278搭建的单通道网关和节点，我们可以将节点在诸如农田等地区收集到的温湿度信息汇总到网关处并显示在LCD屏幕上，方便进行监测与管理，同时当温度或湿度低于设定值时会使用蜂鸣器和LED灯报警。

ESP32接口图：该部分同样使用DC5V供电。

注：分析、实验和建模
本产品结构简单，模块化的设计降低了故障风险和制作难度，使得产品的质量有所保证。

由于水泵运作时间长短难以把控，浇水量每次不尽相同，若是加入单片机的控制会有更加稳定的表现。

在装配完成后我们小组对产品进行了实验。在将自动浇水模块的传感器插入土壤后，水泵能正常工作，适当调节电位器后水泵会停止工作。再将信息系统的传感器插入土壤后，可以读取到湿度和温度的值，并据此调节自动浇水电位器来确定合适的浇水阀值。

加工制造过程

四、性能指标

测试过程与测试结果：

1.节点组能够顺利测量数据并控制继电器开关

2.网关组能顺利接收到节点组所传递来的信息，同时在湿度低于阈值时实现报警功能

3.水泵在继电器接通的情况下能够顺利工作，将水抽出，实现自动浇水

性能评估：

目前能顺利实现预期的所有功能，信号传输、报警、自动浇水，且能在土壤中正常工作，满足目前的所有需要。

同时该系统具有很强的拓展性，例如可以实现光强、CO2浓度等影响植物生长的环境的测量并且实现自动化调节，甚至还可以在畜牧业领域发挥它的作用，是一款能够持续拓展功能的产品。

五、代码

六、代码如何运行

七、团建计划

首先，小组在前几周确立针对不同环境因子测量的相关模型，并选择最优模型确定产品的基本组成和制作流程，之后针对相关传感器的选择和Arduino软件编程等工作进行成员之间的分工协作，并在每周六下午四点商讨并反馈本周项目的进度。在最后几周，会针对产品相关功能进行测试，可以选择成都当地农作物产地作为测试地点，力求产品更加完善。
