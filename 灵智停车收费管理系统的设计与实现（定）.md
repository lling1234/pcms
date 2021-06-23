***\*灵智停车收费管理系统\*******\*的设计与实现\****

摘 要：根据我国停车收费现状发现，管理员了解用户停车订单详情和当日停车收入和设备状态等不够直观，停车用户想知道停车时长和停车费用等信息不够快速，易造成停车场出口拥堵。

为解决城市停车收费问题，做到车位资源的充分利用与信息共享，选用Java编程语言Spring Boot框架设计开发，Shiro权限控制，MD5算法信息加密，采用MySQL关系型数据库进行管理，大数据统计分析面板运用EChars可视化图表库，车牌识别运用HyperLPR高性能框架。已实现管理员与工作人员对订单和系统管理，已完成停车用户根据车牌查询订单和支付宝在线支付等功能。

目前，大数据统计分析数据是伪数据，基于高德AR导航正反向寻车处于蓝图阶段，功能待后续补充完善。

 

关键词：停车收费；SpringBoot；HyperLPR；AR正反向寻车



***\*Design and Implementation of Smart Parking Charge Management System\**** 

***\*Abstract\*******\*:\**** According to the current status of parking fees in my country, it is found that the administrators are not intuitive enough to understand the parking order details of parking users and the parking revenue of the day. Parking users want to know the parking duration and parking fees and other information is not fast enough, which may easily cause the parking lot exit congestion. 

In order to solve the problem of urban parking fees, make full use of parking resources and information sharing, the Java programming language Spring Boot framework is selected for design and development, Shiro authority control, MD5 algorithm information encryption, MySQL relational database management, big data statistical analysis The panel uses the EChars visualization chart library and the HyperLPR high-performance license plate recognition framework. The administrator and staff have realized the order and system management, and the parking users have completed the functions of querying orders according to the license plate and Alipay online payment. 

At present, the big data statistical analysis data is pseudo data, and the forward and reverse car search based on AutoNavi AR navigation is in the blueprint stage, and the functions need to be supplemented and improved in the future.

 

***\*Keywords\****: Parking charge; HyperLPR; AR forward and reverse car sear

**
**

***\*目\****  ***\*录\****

[摘要	I](#_Toc16239 )

[Abstract	II](#_Toc24002 )

[1 引言	1](#_Toc28949 )

[1.1 研究背景	1](#_Toc22630 )

[1.1.1 针对企业管理者的痛点分析	1](#_Toc14857 )

[1.1.2 针对用户的痛点分析	2](#_Toc7179 )

[1.2 研究意义	3](#_Toc14394 )

[1.3 结构安排	3](#_Toc22590 )

[2 可行性分析	4](#_Toc10478 )

[2.1 市场可行性	4](#_Toc14677 )

[2.2 经济可行性	4](#_Toc682 )

[2.3 技术可行性	4](#_Toc28992 )

[2.4 社会可行性	4](#_Toc22316 )

[3 需求分析	5](#_Toc1655 )

[3.1 系统顶层需求结构	5](#_Toc1352 )

[3.2 系统角色需求分析	5](#_Toc21250 )

[4 系统的总体设计	8](#_Toc15869 )

[4.1 开发技术简介	8](#_Toc10369 )

[4.2 系统架构图	8](#_Toc11977 )

[4.2.1 系统的逻辑架构	8](#_Toc12776 )

[4.2.2 系统物理架构	9](#_Toc28759 )

[4.3 系统主要功能	10](#_Toc151 )

[4.4 停车接口调用流程	10](#_Toc17505 )

[4.5 数据库设计	12](#_Toc21967 )

[5 系统详细设计与实现	15](#_Toc7119 )

[5.1 登录模块的实现	15](#_Toc26847 )

[5.2 车主订单查询和支付的实现	16](#_Toc15025 )

[5.3 订单管理的实现	17](#_Toc6058 )

[5.4 车位余量查询的实现	18](#_Toc20771 )

[5.5 车位管理的实现	19](#_Toc7288 )

[5.6 收费标准的实现	19](#_Toc22635 )

[5.7 设备管理的实现	20](#_Toc31533 )

[5.8 用户管理的实现	20](#_Toc15811 )

[5.9 通知公告的实现	21](#_Toc10589 )

[5.10 在线用户管理的实现	21](#_Toc28844 )

[6 系统测试	22](#_Toc20437 )

[6.1 项目部署	22](#_Toc22730 )

[6.1.1 部署工具简介	22](#_Toc14733 )

[6.1.2 部署发布	22](#_Toc6029 )

[6.2 接口测试	25](#_Toc25384 )

[6.2.1 接口测试工具简介	25](#_Toc23603 )

[6.2.2 接口测试结果	26](#_Toc30569 )

[6.3 性能测试	27](#_Toc1269 )

[6.3.1 性能测试工具简介	27](#_Toc10302 )

[6.3.2 性能测试报告分析	27](#_Toc24138 )

[7 总结与展望	29](#_Toc4445 )

[参考文献	30](#_Toc6577 )

[附录	32](#_Toc30848 )

[致谢	37](#_Toc8032 )



**
**

# ***\*1 引言\****

## ***\*1.1 研究背景\****

伴随着科技和社会的快速发展，城市中的汽车持有量在不断的增加[1]，信息科技化技术正在悄无声息的改变着我们的生活方式，而传统的停车收费方式，流程复杂、人工操作、统计繁琐等问题，已经无法满足我们当前的日常需求。为了提高停车收费管理水平，分析了部分现有停车收费系统的优点和缺点，通过信息化手段和物联网等技术，为解决城市停车收费问题提供一整套可靠的解决方案，做到车位资源的充分利用与共享[2]。

通过熟悉停车场收费流程业务逻辑，了解到管理员和用户停车收费的难题与痛处，管理员很难了解到停车订单、停车收入、设备状况、充电桩充电状态等信息，停车用户遇到停车安全、停车纠纷、停车收费等问题，致力于开发出一个信息一体化展示、订单可溯源的灵智停车收费管理系统，为用户提供更加优质的服务，解决停车收费不标准、不规范等一系列问题[3]。

### 1.1.1 针对企业管理者的痛点分析

人工成本：传统路侧停车管理的人工成本越来越高，且人工效率低下，一般两个人只能有效的管理十几个车位，管理难度较大。

人事纠纷：由于传统路边停车带来的纠纷层次不穷，车主与车主之间的矛盾、车主与停车管理企业的矛盾以及车主或企业与政府监管部门之间的矛盾等等，用户体验较差。

逃费：有相关资料表明，路侧停车的逃费率高达50%以上。传统路侧停车管理不同于路外停车，有封闭出入口，同时缺乏有效的证据。

收费不标准：收费员利用漏洞私下支付停车费。由于无法有效监督人工费，收费员可能会浪费停车费并填补他们的口袋。

运营模式：传统路侧停车管理采取层层转包方式，不仅降低了管理效率，增加了执法者取证难度，从某种程度上增加了车主们的停车费用。

信息化水平低：区域停车资源没有联网管理，缺乏有效的信息发布渠道，驾驶人与停车场之间无法达成信息交互[4]，驾驶人不能及时掌握空车位信息，空闲车位和收入统计不够一体化，历史停车数据无法追溯,应收、实收费用无法核对。企业管理痛点分析如图1-1所示。

![img](https://gitee.com/ling66611/picgo-image/raw/master/wps3.jpg) 

图1-1 企业管理者痛点分析图

### 1.1.2 针对用户的痛点分析

人工收费：工作人员业务不熟练，自助扫码不熟悉，沟通成本增加，找零慢没零钱，导致车主等待时间较长，造成出入口拥堵。

停车不规范：一部小分车主随意停车，车辆之间间隙过小。

车辆安全：进入地下车库时，上坡下坡是必经之地，上坡速度会减缓，下坡则会加速度。而且有些车库的坡度较大，光线不佳，视角倾斜，少有不慎会发生追尾的状况，安全意识薄弱不锁车，车内物品被盗等。

停车纠纷：车辆逆行，车辆刮蹭，事故认定等，停车用户痛点分析如图1-2所示。

![img](https://gitee.com/ling66611/picgo-image/raw/master/wps4.jpg) 

图1-2 停车用户痛点分析图

## ***\*1.2 研究意义\****

设计开发灵智停车收费管理系统和完成停车用户根据车牌号码查询订单支付功能，停车用户可以快速直观的了解停车场车位余量，根据车牌号码查询入场时间、停车时间、停车费用和支付待付款订单；为超级管理员提供大数据可视化面板，超级管理员拥有用户登录、车位余量、车位管理、订单管理、收费支付、设备管理、系统管理、系统监控等八个模块管理权限；工作人员仅拥有用户登录、车位余量、车位管理、订单管理、设备管理等五个模块管理权限。停车场提供给停车用户更加美观、科学、人性化的停车场设计，改善传统停车场“脏、乱、差”形象。

致力于提供智能停车收费管理系统，打造出结合视频流车牌识别系统自主缴费机设备等AI技术的一流停车场，提供专业运营服务，解放财务提升收益，真正实现“集中管理”，提供管理咨询和云服务，依托云端大数据分析，自动检测设备情况,定期巡检、第一时间维护，实现管理人员“无感管控” [5]。

## ***\*1.3 结构安排\****

(1) 引言首先介绍灵智停车收费管理系统的研究背景和意义，针对企业管理者和用户的痛点分析，然后对系统进行市场、经济、技术和社会可行性分析。

(2) 系统需求分析与总体设计，先对整个系统的需求分析进行顶层需求详细介绍，然后对系统角色进行分析；总体设计先介绍开发技术，系统的架构纷飞逻辑架构和物理架构，明确系统的主要功能，停车接口调用的流程，对整个系统的数据库的设计进行详细介绍，最后对数据库如何实现做一个说明。

(3) 系统详细设计与实现，十大模块的实现介绍和功能界面展示，核心功能为车主订单查询支付和管理员对订单的管理。

(4) 系统测试，最先需要项目打包部署到云服务器，数据移植到云数据库，使用Nginx反向代理到域名，进行功能测试、接口测试和性能测试。

(5) 总结与展望，总结整个系统学到的知识和进步，遇到的问题和解决问题的思路，需要改进的地方，展望未来的方向。

***\*
\****

# ***\*2 可行性分析\****

## ***\*2.1 市场可行性\****

能否取得最佳社会效益。传统的停车收费管理系统相对老旧，技术和框架老旧，无法支持大数据处理和分布式动态服务，核心偏向销售，技术投入乏力和不足；兼容硬件少，捆绑销售，垄断；需要经过对方账号或者非正规小第三方支付平台，到账延时，没有保障，迫切需要一个提供智能一体化、易拓展的停车收费管理系统来解决市场问题。

## ***\*2.2 经济可行性\****

经济可行性是指系统投入市场使用后，获得的经济利润大于其本身的成本开发[6]。本项目的主要成本和预期收益主要包括:开发测试期间成本投入较少，主要是道闸、摄像头、显示屏、服务器费用和管理维护人员等成本，所以经济方面满足。

## ***\*2.3 技术可行性\****

本系统在技术可行性方面主要利用：道闸、摄像头、显示屏、服务器等硬件设备随手可得，运用车牌识别技术识别率高达96%~98%，非常成熟的springboot框架[7]，软件项目组开发成员具备良好的编程能力和自学能力，测试人员掌握主流的测试方法以及相应测试工具的使用。

## ***\*2.4 社会可行性\****

本项目的社会可行性主要体现在: 无软件权利归属问题，无侵权问题，与国家的政策法规不存在任何冲突和抵触之处心。

***\*
\****

# ***\*3 需求分析\****

## ***\*3.1 系统顶层需求结构\****

本系统分为八个模块：用户登录，车位余量，车位管理，订单管理，收费支付，设备管理，系统管理，系统监控，系统顶层需求结构图如图3-1所示。

![img](https://gitee.com/ling66611/picgo-image/raw/master/wps5.jpg) 

图3-1 系统顶层需求结构图

根据使用者的角色类型不同，此系统将使用者的角色分作两种类型，第一类是管理角色分为超级管理员和工作人员，另一类是用户角色分为普通用户、店铺商户和公务人员。

超级管理员用户拥有八个模块的所有权限，工作人员仅有用户登录、车位余量、车位管理、订单管理、设备管理五个模块权限。

普通用户拥有停车入库，根据车牌号查询订单，支付停车订单，车辆出库，查看车位余量；店铺商户由于频繁外出，向超级管理员申请一个月两百元停车次数不限；公务车辆包括公检法和领导车辆，提供相应的证件和资料可以免费停车。

## ***\*3.2 系统角色需求分析\****

灵智停车收费管理系统的主要角色分为停车用户、工作人员和超级管理员三个系统角色。

 

 

 

停车用户分为普通用户、小票用户、店铺商户、公务人员，停车用户用例图如图3-2所示。

![img](https://gitee.com/ling66611/picgo-image/raw/master/wps6.jpg) 

图3-2 停车用户用例图

工作人员拥有车位余量、车位管理、订单管理和设备管理权限，工作人员用例图如图3-3所示。

![img](https://gitee.com/ling66611/picgo-image/raw/master/wps7.jpg) 

图3-3 工作人员用例图

 

超级管理员拥有车位余量、车位管理、订单管理和设备管理、收费支付、系统管理和系统监控等权限，超级管理员用例图如图3-4所示。

![image-20210623110911951](https://gitee.com/ling66611/picgo-image/raw/master/image-20210623110911951.png) 

图3-4 超级管理员用例图

# ***\*4 系统的总体设计\****

## ***\*4.1 开发技术简介\****

灵智停车收费管理系统需要使用的开发技术主要包括： 

(1) Bootstrap前端框架；

(2) SpringBoot后端框架；

(3) Apache Shiro安全框架；

(4) Thymeleaf模板引擎；

(5) MyBatis持久层框架；

(6) Druid数据库连接池等；

(7) Swagger 接口服务框架；

(8) RouYi-fast开源项目。

系统开发环境主要是：开发工具 IntelliJ IDEA 2019.2、Win10操作系统、CPU i7-8=1206U、内存8.0G。

## ***\*4.2 系统架构图\****

### 4.2.1 系统的逻辑架构

灵智停车收费管理系统的整体逻辑架构分为数据Model层、业务逻辑Service 层、控制Controller层、表示View层和持久Dao层五层架构。其中表示View层主要是Web前端的展示，代码主要是HTML、CSS、JavaScript 等。控制层主要用于接口的编写，数据全部以json格式传输[8]。业务逻辑层包括了用户登录，车位余量，车位管理，订单管理，收费支付，设备管理，系统管理，系统监控这八个模块的业务逻辑。数据访问层主要是用于domain实体类的编写。持久层以MyBatis进行数据库的读写操作[9]。

### 4.2.2 系统物理架构

系统物理架构为云服务器和云数据库，移动端支持手机和平板电脑，pc端支持台式电脑和笔记本电脑等硬件设备；为车主、工作人员和管理员提供服务，系统物理架构如图4-1所示。

![img](https://gitee.com/ling66611/picgo-image/raw/master/wps9.jpg) 

图4-1 系统物理架构图

 

## ***\*4.3 系统主要功能\****

系统主要功能包括用户登录、车位余量、车位管理、订单管理、收费支付、设备管理、系统管理、系统监控等八个模块，系统主要功能如图4-2所示。

 ![image-20210623111107930](https://gitee.com/ling66611/picgo-image/raw/master/image-20210623111107930.png)

图4-2 系统主要功能图

## ***\*4.4 停车接口调用流程\****

车主车辆进入道闸前拍照记录停车信息，离开时候支付宝App扫一扫停车服务二维码，查询停车费用并缴纳，道闸自动抬杆离场，停车支付流程如图4-3所示。

![image-20210623111329232](https://gitee.com/ling66611/picgo-image/raw/master/image-20210623111329232.png) 

图4-3 停车支付流程图

停车用户驾驶车辆驶入停车场，识别车牌抬杆，停车平台记录车辆驶入信息，用户查询支付停车费后驶出停车场，识别车牌抬杆离场记录车辆驶出信息，用户对订单有疑虑可以申请退款，支付宝接口调用流程如图4-4所示。

![image-20210623111354327](https://gitee.com/ling66611/picgo-image/raw/master/image-20210623111354327.png) 

图4-4 支付宝接口调用流程图

## ***\*4.5 数据库设计\****

MySQL数据库设计共8张表，InnoDB引擎，utf8字符集，utf8_general_ci排列规则[10]，车位余量表、收费标准表、设备表、订单管理表、支付方式表、车位管理表、小票订单表、特殊订单表。

车位余量表储存车库名、车位余量、是否有充电桩枚举类型是或否，其主键为id字段，如表4-1所示。

表4-1 车位余量表

| ***\*序列\**** | ***\*列名\****    | ***\*数据类型\**** | ***\*可空\****     | ***\*默认值\**** | ***\*注释\**** |
| -------------- | ----------------- | ------------------ | ------------------ | ---------------- | -------------- |
| 1              | ***\*id\****      | ***\*int\****      | ***\*NOT NULL\**** |                  | id，主键       |
| 2              | ***\*name\****    | ***\*varchar\****  | ***\*NULL\****     |                  | 车库名         |
| 3              | ***\*balance\**** | ***\*int\****      | ***\*NULL\****     |                  | 车位余量       |
| 4              | ***\*charge\****  | ***\*enum\****     | ***\*NULL\****     | '否','是'        | 是否有充电桩   |

收费标准表储存收费名称、收费标准、收费状态枚举类型启用中或未启用，其主键为收费支付id字段，如表4-2所示。

表4-2 收费标准表

| ***\*序列\**** | ***\*列名\**** | ***\*数据类型\**** | ***\*可空\**** | ***\*默认值\****  | ***\*注释\****   |
| -------------- | -------------- | ------------------ | -------------- | ----------------- | ---------------- |
| 1              | id             | int                | NOT NULL       |                   | 收费支付id，主键 |
| 2              | name           | varchar            | NULL           |                   | 收费名称         |
| 3              | standard       | text               | NULL           |                   | 收费标准         |
| 4              | state          | enum               | NULL           | '启用中','未启用' | 收费状态         |

设备表储存设备名、设备型号、设备价格、使用时长、备注，设备状态枚举类型故障或正常，其主键为设备管理id字段，如表4-3所示。

表4-3 设备表

| ***\*序列\**** | ***\*列名\****      | ***\*数据类型\**** | ***\*可空\****     | ***\*默认值\**** | ***\*注释\**** |
| -------------- | ------------------- | ------------------ | ------------------ | ---------------- | -------------- |
| 1              | ***\*id\****        | ***\*int\****      | ***\*NOT NULL\**** |                  | 设备管理id     |
| 2              | ***\*equipName\**** | ***\*varchar\****  | ***\*NULL\****     |                  | 设备名         |
| 3              | ***\*models\****    | ***\*varchar\****  | ***\*NULL\****     |                  | 设备型号       |
| 4              | ***\*price\****     | ***\*double\****   | ***\*NULL\****     |                  | 设备价格       |
| 5              | ***\*useTime\****   | ***\*varchar\****  | ***\*NULL\****     |                  | 使用时长       |
| 6              | ***\*state\****     | ***\*enum\****     | ***\*NULL\****     | '正常','故障'    | 设备状态       |
| 7              | ***\*remark\****    | ***\*varchar\****  | ***\*NULL\****     |                  | 备注           |

订单管理表储存车牌号码、车辆类型、入场时间、入场拍照、离场时间、离场拍照、停车费用、支付方式、支付状态，其主键为订单id字段，如表4-4所示。

表4-4 订单管理表

| ***\*序列\**** | ***\*列名\****      | ***\*数据类型\**** | ***\*可空\****     | ***\*默认值\****                              | ***\*注释\**** |
| -------------- | ------------------- | ------------------ | ------------------ | --------------------------------------------- | -------------- |
| 1              | ***\*id\****        | ***\*int\****      | ***\*NOT NULL\**** |                                               | 订单id         |
| 2              | ***\*carNumber\**** | ***\*varchar\****  | ***\*NULL\****     |                                               | 车牌号码       |
| 3              | ***\*carType\****   | ***\*enum\****     | ***\*NULL\****     | '单行蓝牌','单行黄牌','新能源车牌'            | 车辆类型       |
| 4              | ***\*enterTime\**** | ***\*datetime\**** | ***\*NULL\****     | CURRENT_TIMESTAMP                             | 入场时间       |
| 5              | ***\*enterImg\****  | ***\*varchar\****  | ***\*NULL\****     |                                               | 入场拍照       |
| 6              | ***\*leaveTime\**** | ***\*datetime\**** | ***\*NULL\****     |                                               | 离场时间       |
| 7              | ***\*leaveImg\****  | ***\*varchar\****  | ***\*NULL\****     |                                               | 离场拍照       |
| 8              | ***\*price\****     | ***\*double\****   | ***\*NULL\****     |                                               | 停车费用       |
| 9              | ***\*payMethod\**** | ***\*enum\****     | ***\*NULL\****     | '支付宝','微信','银联','二维码','现金','免费' | 支付方式       |
| 10             | ***\*payState\****  | ***\*enum\****     | ***\*NULL\****     | '未支付','已支付'                             | 支付状态       |

支付方式表储存支付名称、支付商户、支付标准、支付状态，其主键为支付id字段，如表4-5所示。

表4-5 支付方式表

| ***\*序列\**** | ***\*列名\****         | ***\*数据类型\**** | ***\*可空\****     | ***\*默认值\**** | ***\*注释\**** |
| -------------- | ---------------------- | ------------------ | ------------------ | ---------------- | -------------- |
| 1              | ***\*id\****           | ***\*int\****      | ***\*NOT NULL\**** |                  | 支付支付id     |
| 2              | ***\*name\****         | ***\*varchar\****  | ***\*NULL\****     |                  | 支付名称       |
| 3              | ***\*bussinesName\**** | ***\*varchar\****  | ***\*NULL\****     |                  | 商户名称       |
| 4              | ***\*appid\****        | ***\*text\****     | ***\*NULL\****     |                  | 支付标准       |
| 5              | ***\*state\****        | ***\*enum\****     | ***\*NULL\****     | '启用','关闭'    | 支付状态       |

车位管理表储存车位编号、使用状态、车牌号为枚举类型使用中或未使用，其主键为车位id字段，如表4-6所示。

表4-6 车位管理表

| ***\*序列\**** | ***\*列名\****      | ***\*数据类型\**** | ***\*可空\****     | ***\*默认值\****  | ***\*注释\**** |
| -------------- | ------------------- | ------------------ | ------------------ | ----------------- | -------------- |
| 1              | ***\*id\****        | ***\*int\****      | ***\*NOT NULL\**** |                   | 车位Id         |
| 2              | ***\*name\****      | ***\*varchar\****  | ***\*NULL\****     |                   | 车位编号       |
| 3              | ***\*occupy\****    | ***\*enum\****     | ***\*NULL\****     | '未使用','使用中' | 使用状态       |
| 4              | ***\*carNumber\**** | ***\*varchar\****  | ***\*NULL\****     |                   | 车牌号         |

小票订单表储存车牌号码、车辆类型、入场时间、入场拍照、离场时间、离场拍照、停车费用、支付方式、支付状态、充电桩状态、备注，如表4-7所示。

表4-7 小票订单表

| ***\*序列\**** | ***\*列名\****        | ***\*数据类型\**** | ***\*可空\****     | ***\*默认值\****                              | ***\*注释\**** |
| -------------- | --------------------- | ------------------ | ------------------ | --------------------------------------------- | -------------- |
| 1              | ***\*id\****          | ***\*int\****      | ***\*NOT NULL\**** |                                               | 订单id         |
| 2              | ***\*carNumber\****   | ***\*varchar\****  | ***\*NULL\****     |                                               | 车牌号码       |
| 3              | ***\*carType\****     | ***\*enum\****     | ***\*NULL\****     | '单行蓝牌','单行黄牌','新能源车牌'            | 车辆类型       |
| 4              | ***\*enterTime\****   | ***\*datetime\**** | ***\*NULL\****     | CURRENT_TIMESTAMP                             | 入场时间       |
| 5              | ***\*price\****       | ***\*double\****   | ***\*NULL\****     |                                               | 停车费用       |
| 6              | ***\*payMethod\****   | ***\*enum\****     | ***\*NULL\****     | '支付宝','微信','银联','二维码','现金','免费' | 支付方式       |
| 7              | ***\*payState\****    | ***\*enum\****     | ***\*NULL\****     | '未支付','已支付'                             | 支付状态       |
| 8              | ***\*chargeState\**** | ***\*enum\****     | ***\*NULL\****     | '未使用','使用中'                             | 充电桩状态     |
| 9              | ***\*remark\****      | ***\*varchar\****  | ***\*NULL\****     |                                               | 备注           |

特殊订单表储存车牌号码、车辆类型、入场时间、入场拍照、离场时间、离场拍照、停车费用、支付方式、支付状态、充电桩状态、备注，其主键为订单id字段如表4-8所示。

表4-8 特殊订单表

| ***\*序列\**** | ***\*列名\****        | ***\*数据类型\**** | ***\*可空\****     | ***\*默认值\****                              | ***\*注释\**** |
| -------------- | --------------------- | ------------------ | ------------------ | --------------------------------------------- | -------------- |
| 1              | ***\*id\****          | ***\*int\****      | ***\*NOT NULL\**** |                                               | 订单id         |
| 2              | ***\*carNumber\****   | ***\*varchar\****  | ***\*NULL\****     |                                               | 车牌号码       |
| 3              | ***\*carType\****     | ***\*enum\****     | ***\*NULL\****     | '公务车辆','商户车辆'                         | 车辆类型       |
| 4              | ***\*enterTime\****   | ***\*datetime\**** | ***\*NULL\****     | CURRENT_TIMESTAMP                             | 入场时间       |
| 5              | ***\*enterImg\****    | ***\*varchar\****  | ***\*NULL\****     |                                               | 入场拍照       |
| 6              | ***\*leaveTime\****   | ***\*datetime\**** | ***\*NULL\****     |                                               | 离场时间       |
| 7              | ***\*leaveImg\****    | ***\*varchar\****  | ***\*NULL\****     |                                               | 离场拍照       |
| 8              | ***\*price\****       | ***\*double\****   | ***\*NULL\****     |                                               | 停车费用       |
| 9              | ***\*payMethod\****   | ***\*enum\****     | ***\*NULL\****     | '支付宝','微信','银联','二维码','现金','免费' | 支付方式       |
| 10             | ***\*payState\****    | ***\*enum\****     | ***\*NULL\****     | '未支付','已支付'                             | 支付状态       |
| 11             | ***\*chargeState\**** | ***\*enum\****     | ***\*NULL\****     | '未使用','使用中'                             | 充电桩         |
| 12             | ***\*remark\****      | ***\*varchar\****  | ***\*NULL\****     |                                               | 备注           |

***\*
\****

# ***\*5 系统详细设计与实现\****

## ***\*5.1 登录模块的实现\****

登录分为超级管理员登录和工作人员登录，超级管理员和工作人员输入正确的账号密码和验证码将会进入管理界面首页，否则将无法登陆，提示用户不存在密码错误，右上角有个人中心可以修改用户信息、修改密码、切换主题横向菜单，退出登录返回用户登录界面，登录界面和管理员主界面如图5-1、图5-2所示。

![img](https://gitee.com/ling66611/picgo-image/raw/master/wps13.jpg) 

图5-1 登录界面图

 

![image-20210623111505056](https://gitee.com/ling66611/picgo-image/raw/master/image-20210623111505056.png) 

图5-2 管理员主界面图

## ***\*5.2 车主订单查询和支付的实现\****

车主可以一目了然获取车位余量，可以根据车牌号码查询订单，返回给车主入场时间、停车时长和停车费用，车主验证无误后可以支付订单，跳转到付款页面打开支付宝App完成订单支付，订单交易付款成功跳转至商户页面，提示用户“支付成功后，请在十五分钟内离场，否则将会重新计费，谢谢配合”，否则未查到数据将返回车辆未入场，车主订单查询支付和支付宝沙箱环境支付如图5-3、图5-4所示。

![image-20210623111526872](https://gitee.com/ling66611/picgo-image/raw/master/image-20210623111526872.png) 

图5-3 车主订单查询支付图

 

![image-20210623111541773](https://gitee.com/ling66611/picgo-image/raw/master/image-20210623111541773.png) 

图5-4 支付宝沙箱环境支付图

## ***\*5.3 订单管理的实现\****

订单管理分为停车订单、小票订单、特殊订单，车辆入库拍照HyperLPR自动识别车牌号抬杆[11]，车主提前支付停车订单或者到道闸现金支付，离场拍照道闸抬杆离库；小票订单是出现道闸出故障、无法识别车牌号码等情况，人工生成小票订单给车主，车主可以通过扫码支付；特殊订单在商业广场、医疗机构、教育机构、政府机构等场景，有办月卡的店铺商户频繁进出停车场，工作人员、领导干部、公检法人员等办公需出示相关证件拍照即可免费停车，订单管理和修改停车订单如图5-5、图5-6所示。

![image-20210623111620506](https://gitee.com/ling66611/picgo-image/raw/master/image-20210623111620506.png) 

图5-5 订单管理图

 

![image-20210623111633473](https://gitee.com/ling66611/picgo-image/raw/master/image-20210623111633473.png) 

图5-6 修改停车订单图

## ***\*5.4 车位余量查询的实现\****

灵智停车收费管理系统有五个车库，一二三号车库没有充电桩，四五号车库有充电桩，新能源电动汽车可以一边停车一边充电，方便快捷，安全省心，车位余量如图5-7所示。

![image-20210623111654733](https://gitee.com/ling66611/picgo-image/raw/master/image-20210623111654733.png) 

图5-7 车位余量图

## ***\*5.5 车位管理的实现\****

车位管理可以清楚知道车主进入几号停车库，能了解车位使用状态，合理的分配资源，提供更优质的服务，车位管理如图5-8所示。

![image-20210623111709748](https://gitee.com/ling66611/picgo-image/raw/master/image-20210623111709748.png) 

图5-8 车位管理图

## ***\*5.6 收费标准的实现\****

收费标准有四种方式，24小时统一收费、指定收费标准、充电桩收费、店铺商户月卡，可以灵活的制定选用收费标准，支付方式有六种，支付宝、微信、银联、二维码、现金、免费，收费标准如图5-9所示。

![img](https://gitee.com/ling66611/picgo-image/raw/master/wps21.jpg) 

图5-9 收费标准图

## ***\*5.7 设备管理的实现\****

道闸设备选用徽腾道闸型号D0001，每个道闸口设置前后两个华夏摄像头，200万像素高清摄像机，Led高清显示屏等，设备管理如图5-10所示。

![img](https://gitee.com/ling66611/picgo-image/raw/master/wps22.jpg) 

图5-10 设备管理图

## ***\*5.8 用户管理的实现\****

用户管理可以对用户进行增加、删除、修改和查询等一系列操作，导出导入用户数据，为用户分配权限、组织部门、角色，重置密码等，用户管理如图5-11所示。

![img](https://gitee.com/ling66611/picgo-image/raw/master/wps23.jpg) 

图5-11 用户管理图

## ***\*5.9 通知公告的实现\****

超级管理员发布通知和公告，修改通知和公告的状态为正常或关闭，工作人员可以查看到通知和公告，通知公告如图5-12所示。

![img](https://gitee.com/ling66611/picgo-image/raw/master/wps24.jpg) 

图5-12 通知公告图

## ***\*5.10 在线用户管理的实现\****

系统用户里面可以看到所有在线的用户，显示会话编号、部门名称、主机IP、登录地点、登录时间、浏览器、操作系统等信息，超级管理员可以强退在线用户，在线用户管理如图5-13所示。

![image-20210623111805196](https://gitee.com/ling66611/picgo-image/raw/master/image-20210623111805196.png) 

图5-13 在线用户管理图

 

***\*
\****

# ***\*6 系统测试\****

## ***\*6.1 项目部署\****

首先用maven把项目打包成jar文件，本机通过XFTP文件上传客户端将jar包上传到阿里云Linux服务器，服务器已经安装宝塔Linux面板。

### 6.1.1 部署工具简介

宝塔面板是一款服务器管理软件[12]，支持windows和linux系统，可以通过Web端轻松管理服务器，提升运维效率。例如：快速部署SpringBoot项目，创建管理网站、FTP、数据库，拥有可视化文件管理器，可视化软件管理器，可视化CPU、内存、流量监控图表，计划任务等功能。

Nginx是俄罗斯的程序设计师开发高性能的web和反向代理服务器，也是一个IMAP/POP2/STMP代理服务器。nginx之所以性能良好，完全是由它的架构决定的。每个worker进程是业务处理进程，负责监听套接字、处理请求、响应请求、代理请求至后端服务器等。在高连接并发的情况下，Nginx是Apache服务器不错的替代品[13]。

### 6.1.2 部署发布

阿里云ECS安全组规则入方向手动添加8082端口，协议类型自定义tcp，授权对象源:0.0.0.0/0，阿里云ESC安全组规则配置如图6-1所示。

![img](https://gitee.com/ling66611/picgo-image/raw/master/wps26.jpg) 

图6-1 阿里云ESC安全组规则配置图

宝塔软件商城安装并且运行java项目部署1.0,选择SpringBoot，添加项目项目路径为/www/SpringBoot，项目端口为8082，初始状态为停止，点击开启运行项目，项目可正常访问，宝塔项目发布如图6-2所示。

![img](https://gitee.com/ling66611/picgo-image/raw/master/wps27.jpg) 

图6-2 宝塔项目发布图

为了防止网站项目非正常关闭，计划任务里面添加计划任务，执行周期每十分钟执行一次，宝塔计划任务如图6-3所示。

![image-20210623111849453](https://gitee.com/ling66611/picgo-image/raw/master/image-20210623111849453.png) 

图6-3 宝塔计划任务图

宝塔计划任务脚本内容如下：

cd /usr/local/nginx/sbin

./nginx

nohup java -jar /www/SpringBoot/pcms.jar --server.port=8082

Nginx反向代理配置，我们监听80端口，访问域名为www.ling111.top，不加端口号时默认为80端口，故访问该域名时会跳转到www.ling111.top:8082路径上。在 nginx.conf 配置文件中增加如下配置：

server {

?    listen    80;

?    server_name  www.ling111.top;

?    location / {

?      proxy_pass http://www.ling111.top:8082;

?      index  index.html index.htm index.jsp; }

 }

## ***\*6.2 接口测试\****

### 6.2.1 接口测试工具简介

Swagger是一个简单但功能强大的API表达工具。它具有地球上最大的API工具生态系统，数以千计的开发人员，使用几乎所有的现代编程语言，都在支持和使用Swagger[14]。使用Swagger生成API，我们可以得到交互式文档，自动生成代码的SDK以及API的发现特性等，Swagger接口文档如图6-4所示。

![image-20210623111914959](https://gitee.com/ling66611/picgo-image/raw/master/image-20210623111914959.png) 

图6-4 Swagger接口文档图

### 6.2.2 接口测试结果

获取用户详情接口，输入用户id，状态码为200，接口测试结果如图6-5所示。

![img](https://gitee.com/ling66611/picgo-image/raw/master/wps30.jpg) 

图6-5 接口测试结果图

## ***\*6.3 性能测试\****

### 6.3.1 性能测试工具简介

压力测试使用的是k6，k6是高性能的负载测试工具，也是一种高性能工具，旨在在预生产和QA环境中以高负载运行测试，可使用JavaScript编写脚本。它是一个以开发人员为中心（当然，测试人员亦可以使用，因为真的很方便），免费和开源的负载测试工具，旨在使性能测试具有生产力和令人愉悦的体验，可最大程度地减少系统资源的消耗[15]，性能测试配置准备如图6-6所示。

![image-20210623111941217](https://gitee.com/ling66611/picgo-image/raw/master/image-20210623111941217.png) 

图6-6 性能测试配置准备图

### 6.3.2 性能测试报告分析

经过漫长的等待，[自动化算法](https://k6.io/docs/cloud/analyzing-results/performance-insights)已经分析了测试结果，没有发现任何性能问题，性能测试相应时间如图6-7所示。

![image-20210623111957522](https://gitee.com/ling66611/picgo-image/raw/master/image-20210623111957522.png) 

图6-7 性能测试响应时间图

被测系统的平均响应时间为3047ms，发出930个请求，其中31个失败，平均请求率为3个请求/秒，性能测试请求分析如图6-8所示。

![image-20210623112018607](https://gitee.com/ling66611/picgo-image/raw/master/image-20210623112018607.png) 

图6-8 性能测试请求分析图

***\*
\****

# ***\*7 总结与展望\****

灵智停车收费管理系统使用Java开发，运用SpringBoot框架作为核心，整合Thymeleaf模板、MySQL驱动包、MyBatis框架、Pagehelper分页插件、阿里巴巴Druid连接池、Fileupload文件上传工具类、Shiro核心框架、EhCache缓存框架、Fastjson解析器、Quartz定时任务、Kaptcha验证码、Swagger2框架、Excel工具类、Echars表图可视化库等技术。系统实现了用户登录，车位余量，车位管理，订单管理，收费支付，设备管理，系统管理，系统监控等功能。基本满足小中型停车场的需求，适用于多种复杂的场景，提供大数据实时分析，快速兼容主流车牌识别品牌，实现将传统停车管理互联网化改造，无人值守，月卡线上缴费、访客车辆授权、临停扫码和代客缴费等。

系统也存在很多不足之处，主要体现在：其一数据库表结构的设计与索引具有较大的优化空间，SQL语句的优化等问题，由于请求并发量不高，此类问题并没有暴露出来。其二使用阿里云学生服务器性能需要进一步改善，本系统面向中小型停车场开发，高并发服务器可能无法支撑。其三车牌号码识别使用开源的HyperLPR项目，原计划也集成到项目里面，环境安装有版本不兼容问题，使用安卓端的HyperLPRDemo进行测试。其四由于时间问题支付功能目前只实现支付宝支付，微信、银联等支付还没有接入。

在完成毕业设计的这段时间里，通过自学平台学习了大量的较为前沿的开发知识，本系统基于Spring Boot + BootStrap完成，在后续的项目部署上可以通过Maven直接导出 jar包的方式运行中 Linux云服务器中，同时使用Nginx作为反向代理服务器很轻松的部署，大大简化了后期维护的力度和时间成本。 

**
**

# ***\*参考文献\****

[1]张欢欢,王冰玲.智能停车收费管理系统设计[J].现代商贸工业,2019,40(03):189.

[2]张群. 改善城市停车问题的对策研究——以宁夏银川市为例[J]. 智能城市, 2020(19).

[3]Yinghua Gu. Parking Charge Problem Based on Traffic Demand Management[A]. 中国科学技术协会、交通运输部、中国工程院.2018世界交通运输大会论文集[C].中国科学技术协会、交通运输部、中国工程院:中国公路学会,2018:5.

[4]左臣华. 基于物联网的区域停车场管理系统[J]. 城市建筑, 2017,000(008):345-345.

[5]伍鹏, 林力辉, 吴晓杰,等. 基于"互联网+"大数据的输电巡检智能管控平台研发及应用[J]. 电网与清洁能源, 2020, v.36;No.248(03):59-63.

[6]邓智明, 孙红岩, 杨蓉,等. 一种基于经济评价模型的投资决策方法及系统:, CN111027831A[P]. 2020.

[7]Jian Chen,Chen Jian,Pan Hailan. Design of Man Hour Management Information System on SpringBoot Framework[J]. Journal of Physics: Conference Series,2020,1646(1).

[8]周建韡. 电商系统数据库设计及数据访问优化技术研究[D]. 东华大学.

[9]叶刚;王立河;王英明;谷国栋.基于Mybatis Plus的动态生成代码设计与实现[J].电脑编程技巧与维护,2019,No.409,9-10.

[10]叶方超，张思扬，李传锴.基于SpringBoot的旧物回收商城的设计与实现[J].智能计算机与应用.2019.9(5):84-87.

[11]王美琴,易敏,关财忠,王茗祎.车牌自动识别系统设计[J].仪器仪表用户,2020,27(10):5-9+40.

[12]段尊敬. Java项目从Windows开发平台到Linux服务器的移植[J]. 电脑知识与技术, 2020, v.16(07):91-93.

[13]岳晋, 温宇, 黄旻亮. Windows环境下的Nginx高并发实现[J]. 电子技术与软件工程, 2019, No.163(17):63-65.

[14]吴江. 开发实践:使用Swagger快速打造REST API文档. 

[15]张艳华. 基于LoadRunner的网络考试系统性能测试实践[J]. 电脑知识与技术, 2019(7X):106-108.

 

 

 

 

 

**
**

# ***\*附   录\****

***\*附录1 停车订单controller类\****

/**  * 停车订单Controller  *   * @author ling  * @date 2021-03-05  */ @Controller @RequestMapping("/ParkingOrder/ParkingOrder") public class ParkingOrderController extends BaseController {   private String prefix = "ParkingOrder/ParkingOrder";   @Autowired   private IParkingOrderService parkingOrderService;    @RequiresPermissions("ParkingOrder:ParkingOrder:view")   @GetMapping()   public String ParkingOrder()   {     return prefix + "/ParkingOrder";   }    /**    * 查询停车订单列表    */   @RequiresPermissions("ParkingOrder:ParkingOrder:list")   @PostMapping("/list")   @ResponseBody   public TableDataInfo list(ParkingOrder parkingOrder)   {     startPage();     List<ParkingOrder> list = parkingOrderService.selectParkingOrderList(parkingOrder);     return getDataTable(list);   }    /**    * 导出停车订单列表    */   @RequiresPermissions("ParkingOrder:ParkingOrder:export")   @Log(title = "停车订单", businessType = BusinessType.EXPORT)   @PostMapping("/export")   @ResponseBody   public AjaxResult export(ParkingOrder parkingOrder)   {     List<ParkingOrder> list = parkingOrderService.selectParkingOrderList(parkingOrder);     ExcelUtil<ParkingOrder> util = new ExcelUtil<ParkingOrder>(ParkingOrder.class);     return util.exportExcel(list, "ParkingOrder");   }    /**    * 新增停车订单    */   @GetMapping("/add")   public String add()   {     return prefix + "/add";   }    /**    * 新增保存停车订单    */   @RequiresPermissions("ParkingOrder:ParkingOrder:add")   @Log(title = "停车订单", businessType = BusinessType.INSERT)   @PostMapping("/add")   @ResponseBody   public AjaxResult addSave(ParkingOrder parkingOrder)   {     return toAjax(parkingOrderService.insertParkingOrder(parkingOrder));   }    /**    * 修改停车订单    */   @GetMapping("/edit/{id}")   public String edit(@PathVariable("id") Long id, ModelMap mmap)   {     ParkingOrder parkingOrder = parkingOrderService.selectParkingOrderById(id);     mmap.put("parkingOrder", parkingOrder);     return prefix + "/edit";   }    /**    * 修改保存停车订单    */   @RequiresPermissions("ParkingOrder:ParkingOrder:edit")   @Log(title = "停车订单", businessType = BusinessType.UPDATE)   @PostMapping("/edit")   @ResponseBody   public AjaxResult editSave(ParkingOrder parkingOrder)   {     return toAjax(parkingOrderService.updateParkingOrder(parkingOrder));   }    /**    * 删除停车订单    */   @RequiresPermissions("ParkingOrder:ParkingOrder:remove")   @Log(title = "停车订单", businessType = BusinessType.DELETE)   @PostMapping( "/remove")   @ResponseBody   public AjaxResult remove(String ids)   {     return toAjax(parkingOrderService.deleteParkingOrderByIds(ids));   } }

***\*附录2 MyBatis ParkingOrderMapper配置文件\****

<?xml version="1.0" encoding="UTF-8" ?> <!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "http://mybatis.org/dtd/mybatis-3-mapper.dtd"> <mapper namespace="com.ruoyi.project.parking.ParkingOrder.mapper.ParkingOrderMapper">      <resultMap type="ParkingOrder" id="ParkingOrderResult">     <result property="id"   column="id"   />     <result property="carNumber"   column="carNumber"   />     <result property="carType"   column="carType"   />     <result property="enterTime"   column="enterTime"   />     <result property="enterImg"   column="enterImg"   />     <result property="leaveTime"   column="leaveTime"   />     <result property="leaveImg"   column="leaveImg"   />     <result property="price"   column="price"   />     <result property="payMethod"   column="payMethod"   />     <result property="payState"   column="payState"   />   </resultMap>    <sql id="selectParkingOrderVo">     select id, carNumber, carType, enterTime, enterImg, leaveTime, leaveImg, price, payMethod, payState from parking_order   </sql>    <select id="selectParkingOrderList" parameterType="ParkingOrder" resultMap="ParkingOrderResult">     <include refid="selectParkingOrderVo"/>     <where>         <if test="carNumber != null  and carNumber != ''"> and carNumber = #{carNumber}</if>       <if test="carType != null  and carType != ''"> and carType like concat('%', #{carType}, '%')</if>       <if test="enterTime != null "> and enterTime like concat('%', #{enterTime}, '%')</if>       <if test="leaveTime != null "> and leaveTime like concat('%', #{leaveTime}, '%')</if>       <if test="payMethod != null  and payMethod != ''"> and payMethod = #{payMethod}</if>       <if test="payState != null  and payState != ''"> and payState = #{payState}</if>     </where>   </select>      <select id="selectParkingOrderById" parameterType="Long" resultMap="ParkingOrderResult">     <include refid="selectParkingOrderVo"/>     where id = #{id}   </select>        <insert id="insertParkingOrder" parameterType="ParkingOrder" useGeneratedKeys="true" keyProperty="id">     insert into parking_order     <trim prefix="(" suffix=")" suffixOverrides=",">       <if test="carNumber != null">carNumber,</if>       <if test="carType != null">carType,</if>       <if test="enterTime != null">enterTime,</if>       <if test="enterImg != null">enterImg,</if>       <if test="leaveTime != null">leaveTime,</if>       <if test="leaveImg != null">leaveImg,</if>       <if test="price != null">price,</if>       <if test="payMethod != null">payMethod,</if>       <if test="payState != null">payState,</if>      </trim>     <trim prefix="values (" suffix=")" suffixOverrides=",">       <if test="carNumber != null">#{carNumber},</if>       <if test="carType != null">#{carType},</if>       <if test="enterTime != null">#{enterTime},</if>       <if test="enterImg != null">#{enterImg},</if>       <if test="leaveTime != null">#{leaveTime},</if>       <if test="leaveImg != null">#{leaveImg},</if>       <if test="price != null">#{price},</if>       <if test="payMethod != null">#{payMethod},</if>       <if test="payState != null">#{payState},</if>      </trim>   </insert>    <update id="updateParkingOrder" parameterType="ParkingOrder">     update parking_order     <trim prefix="SET" suffixOverrides=",">       <if test="carNumber != null">carNumber = #{carNumber},</if>       <if test="carType != null">carType = #{carType},</if>       <if test="enterTime != null">enterTime = #{enterTime},</if>       <if test="enterImg != null">enterImg = #{enterImg},</if>       <if test="leaveTime != null">leaveTime = #{leaveTime},</if>       <if test="leaveImg != null">leaveImg = #{leaveImg},</if>       <if test="price != null">price = #{price},</if>       <if test="payMethod != null">payMethod = #{payMethod},</if>       <if test="payState != null">payState = #{payState},</if>     </trim>     where id = #{id}   </update>    <delete id="deleteParkingOrderById" parameterType="Long">     delete from parking_order where id = #{id}   </delete>    <delete id="deleteParkingOrderByIds" parameterType="String">     delete from parking_order where id in      <foreach item="id" collection="array" open="(" separator="," close=")">       #{id}     </foreach>   </delete>  </mapper> 

**
**

# ***\*致\****  ***\*谢\****

大学四年恍然间就接近尾声，这是人生中最美好、独立支配时间称得上是自由的四年。在这四年里，认识了很多优秀负责的老师和学生，也收获了很多感动与知识。在此，我要感谢郑州财经学院的悉心培养。由衷致谢大学四年来，在我通往进步的道路上帮助过指点过我的长者、老师、同学、朋友、同事。

首先，在系统设计和说明书撰写即将完成之际，回顾繁忙却又充实的学习和开发过程，非常感谢指导老师王水萍，她对工作负责，对待学生亲切、有耐心，感谢她在毕业设计过程中带给我的指导和帮助，遇到这样的老师是我的幸运。

其次，我想感谢我的家人。这四年里带给我对人生不同的理解与体会，家人永远是我最大的动力与支撑，他们深爱我、关心我、支持我，我永远牢记，我也很珍惜每次相聚和交流。希望我能用更大的努力换来更好的自己，不辜负他们对我的关爱。

最后衷心的感谢各位老师参加系统设计说明书审稿和答辩，您们辛苦了。

 