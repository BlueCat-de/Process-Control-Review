# 过程控制复习手册

cqm20@mails.tsinghua.edu.cn

## 零、绪论

### 1. 什么是过程控制

* **过程：**
  * 从原料到产品的加工过程
  * 经历一段时间
  * 伴随**物质**、**能量**和**信息**的变化
  * 分类：流程工业和离散制造业
    * 连续过程：上道工序生产出一单位的中间品即向下转移的生产方式称为连续生产。
    * 批量（间歇）过程：生产过程有间断，不连续。
    * 离散过程：产品是由许多零部件构成的， 各零件的加工装配过程彼此是独立的 ，整个产品的生产工艺是离散的 ，制成的零件通过部件装配和总装配，最后成为成品 。例如，机械造、电子设备制造、汽车生产。
* **过程控制 考过**
  * 连续过程：针对连续或半连续（间歇）过程中的**温度**、**压力**、**流量**、**液（物）位**、**化学成份**（如产品成份、含氧量）、**物性参数**（如粘度、融熔指数）等工艺参数作为被控变量的自动控制。
  * 离散过程：针对离散过程中**位置、速度、加速度、尺寸**等工艺参数作为被控变量的自动控制。
  * 五大被控参数：温度（实验室反应釜温控系统）、压力（蒸汽发生器压力控制系统）、流量（化工生产中液体流量控制系统）、液位（液体储罐的液位控制系统）、成分（乙醇生产中的乙烯浓度控制系统）
  * 涉及领域：流程工业

### 2. 过程控制的基础知识

* **过程控制系统及其基本构成**

  * **过程控制系统定义**：对生产过程中的重要参数（温度、压力、流量、物位、成分、湿度等）进行控制 ，使其 保持恒定或按一定规律变化，克服干扰 ，满足性能指标要求。
  * **被控参数CV（考过）**
    * 直接参数：适用于可以直接测量和监测的被控量。如热油出口温度、燃料油压力、炉膛负压、烟气含氧量。
    * 间接参数：适用于无法直接测量被控量，但可以通过其他相关参数来推导和间接估计被控量的情况。如，对于流量控制系统，如果无法直接测量流量，但可以测量液位和管道压力，可以利用管道截面积和压力差来间接推导和估计流量。
    * 若无法找到合适的间接参数，可以使用**故障诊断法**，通过监测和分析控制系统中的故障或异常状态，识别和判断被控量的变化。
  * **控制量/操作量MV**：受控制器操纵的，使被控参数保持设定值的物料量或能量。
  * **扰动量DV**：作用于被控过程并引起被控参数变化的因素。
  * **设定值SP**：被控参数的预定值。
  * **当前值PV**：被控参数的当前实际值。
  * **控制器输出值COV**：是指控制器经过计算后得到的数值，通过执行机构驱动操作变量。
  * **偏差E**：被控参数的设定值与当前实际值之差，**SP-PV**

* **控制结构图**

  <img src="C:\Users\28113\AppData\Roaming\Typora\typora-user-images\image-20230612155428475.png" alt="image-20230612155428475" style="zoom:67%;" />

  ![image-20230612155443563](C:\Users\28113\AppData\Roaming\Typora\typora-user-images\image-20230612155443563.png)

  <img src="C:\Users\28113\AppData\Roaming\Typora\typora-user-images\image-20230612155732758.png" alt="image-20230612155732758" style="zoom:80%;" />

  <img src="C:\Users\28113\AppData\Roaming\Typora\typora-user-images\image-20230612155901056.png" alt="image-20230612155901056" style="zoom:80%;" />

  * **过程控制系统目标**：对于任意的外部干扰（DV），通过控制算法调节操作变量（MV）以使被控变量（CV）维持在其设定值（SP）。

* **控制系统性能指标（阶跃响应）**

  各品质指标之间既有联系、又有矛盾。例如，过分减小最大偏差，会使过渡时间变长。

  * **稳定性**

    ![image-20230612161701984](C:\Users\28113\AppData\Roaming\Typora\typora-user-images\image-20230612161701984.png)

    * 衰减比：$n=\frac{B_1}{B_2}$，B1为第一个波振幅，B2为第二个波振幅，n大于1系统稳定。一般n=4:1~10:1之间合适，对应$\phi=75\%-90\%$
    * 衰减率：$\phi=\frac{B_1-B_2}{B_1}=1-\frac{1}{n}$

  * **准确性**

    ![image-20230612161948666](C:\Users\28113\AppData\Roaming\Typora\typora-user-images\image-20230612161948666.png)

    * 最大动态偏差（越小越好）：系统瞬间偏离给定值的最大程度，A=Bmax-r。
    * 超调量$\sigma=\frac{B_1}{y(\infty)}$
    * 余差（静差）$C=y(\infty)-r$（越小越好）

  * **快速性**

    * 调节时间$T_s$：从过渡过程开始到结束所需时间，当偏差进入稳态值的$+-5(2)\%$认为结束。（短好）
    * 振荡频率$f$：过渡过程中相邻两波峰之间的时间间隔的倒数。（大好）
    * 峰值时间$T_p$：指过渡过程开始，至被控参数到达第一个波峰所需要的时间。

* **控制过程系统类型**

  * 结构特点分类：单回路反馈控制、串级控制、前馈控制、比值控制等。
  * 设定值形式分类：定值控制系统（SP不变）、随动控制系统（SP变化）、程序控制系统（设定值按预定的时间程序变化）

### 3. 过程控制系统的任务与设计（非重点）

* 控制系统设计与实施的主要步骤
  1. 确定控制目标
  2. 选择被控变量CV
  3. 选择操作变量MV
  4. 分析主要扰动DV
  5. 确定控制方案
  6. 选择控制系统的软硬件
  7. 设计报警和连锁保护系统
  8. 控制系统的现场安装与调试

## 一、过程的动态特性与建模

### 1. 被控过程特性的一般描述（非重点）

* 对于单回路控制系统，广义被控对象由被控对象、执行器和变送器构成。

  ![image-20230612163905139](C:\Users\28113\AppData\Roaming\Typora\typora-user-images\image-20230612163905139.png)

* **静态特性与动态特性**
  * 静态：$y=f(u)$
  * 动态：$y=f(u,t)$
* **描述法**
  * 参数描述法：微分方程、传递函数、差分方程、脉冲传递函数、状态空间方程描述
  * 非参数描述法：阶跃响应、脉冲响应、频率响应（Bode）

### 2. 过程的动态特性分析

自衡过程：过程在扰动或输入作用下，平衡状态被破坏，依靠自身的能力，被控量逐渐达到新的平衡，具有自平衡能力，称为自衡过程

非自衡过程：指本身不具有自平衡能力的过程。

* **单容过程的动态特性（单容水槽为例）**

  ![image-20230612164604243](C:\Users\28113\AppData\Roaming\Typora\typora-user-images\image-20230612164604243.png)

  <img src="C:\Users\28113\AppData\Roaming\Typora\typora-user-images\image-20230612165117617.png" alt="image-20230612165117617" style="zoom:80%;" />

  <img src="C:\Users\28113\AppData\Roaming\Typora\typora-user-images\image-20230612165224477.png" alt="image-20230612165224477" style="zoom:80%;" />

  <img src="C:\Users\28113\AppData\Roaming\Typora\typora-user-images\image-20230612170043085.png" alt="image-20230612170043085" style="zoom:80%;" />

  * **过程增益**：稳态条件下输入导致输出变化的幅度、输出对输入变化的灵敏度、$K=\frac{\Delta{y}}{\Delta{u}}=\frac{y(\infty)-y_0}{\Delta{u}}$，包括**符号**、**数值**和**单位**。

  * **一阶时间常数**：对于单容过程，T为输出开始变化到全部变化的$63.2\%$所需时间。反映了输出变化的快慢，越小越块。

  * **纯滞后时间**：过程输入施加激励至过程输出开始变化所需时间。$\frac{\tau}{T}$越大，控制难度越大。

    ![image-20230612170316692](C:\Users\28113\AppData\Roaming\Typora\typora-user-images\image-20230612170316692.png)

  * 飞升速度：$\epsilon=K/T$是单位阶跃响应的最大变化速度。

  * 自平衡率：$\rho=\Delta{u}/y(\infty)=1/K$，越大自衡能力越强

    <img src="C:\Users\28113\AppData\Roaming\Typora\typora-user-images\image-20230612170520277.png" alt="image-20230612170520277" style="zoom:80%;" />

* **多容过程动态特性**

  <img src="C:\Users\28113\AppData\Roaming\Typora\typora-user-images\image-20230612181453075.png" alt="image-20230612181453075" style="zoom:80%;" />

<img src="C:\Users\28113\AppData\Roaming\Typora\typora-user-images\image-20230612181553533.png" alt="image-20230612181553533" style="zoom:80%;" />

<img src="C:\Users\28113\AppData\Roaming\Typora\typora-user-images\image-20230612181752711.png" alt="image-20230612181752711" style="zoom:80%;" />

<img src="C:\Users\28113\AppData\Roaming\Typora\typora-user-images\image-20230612181917428.png" alt="image-20230612181917428" style="zoom:80%;" />

<img src="C:\Users\28113\AppData\Roaming\Typora\typora-user-images\image-20230612182045403.png" alt="image-20230612182045403" style="zoom:80%;" />

<img src="C:\Users\28113\AppData\Roaming\Typora\typora-user-images\image-20230612182346564.png" alt="image-20230612182346564" style="zoom:80%;" />

<img src="C:\Users\28113\AppData\Roaming\Typora\typora-user-images\image-20230612182425373.png" alt="image-20230612182425373" style="zoom:80%;" />

* **非自衡单容过程动态特性（非重点）**

  <img src="C:\Users\28113\AppData\Roaming\Typora\typora-user-images\image-20230612182624868.png" alt="image-20230612182624868" style="zoom:80%;" />

### 3. 特殊过程的动态特性分析（非重点）

* **纯迟延**
  * 传输迟延：$G(s)=e^{-\tau s}$
  * 等效容积迟延：$G(s)=e^{-\pi s}\frac{K}{Ts+1}$
  * 迟延时间越大，越难控制，如加热炉温度变化的时间常数比较大，通常称为大惯性系统。 如果存在比较大的$\tau/T$，则称为大惯性大迟延系统，很难控。
* **工业过程动态特性的特点**
  * 被控对象传递函数特性大多是属于自衡过程，开环稳定；
    * 阶跃响应曲线通常单调，非振荡
  * 被控对象传递函数特性大多具有迟延特性
  * 被控对象传递函数大多具有非线性特性
  * **非线性**、**大迟延**、**分布参数**等特性是过程控制中常见的难点 问题，到目前仍未见特别有效的解决方案，许多研究工作正在继 续展开。

### 4. 过程建模的基本知识（非重点）

主要讨论动态模型。

* 机理法建模：根据生产过程中实际发生的（物理化学）变化机理，写出各 种有关的平衡方程，反映物体运动、传热、传质、化学反应等基本规律的运动 方程，以及物性参数方程，某些设备的特性方程等，从而获得所需的模型。

  * 三种衡算：

    * 质量衡算（物料衡算）：质量守恒定律

      <img src="C:\Users\28113\AppData\Roaming\Typora\typora-user-images\image-20230612183853373.png" alt="image-20230612183853373" style="zoom:80%;" />

    * 能量衡算（能量守恒定律和热力学第二定律）

      <img src="C:\Users\28113\AppData\Roaming\Typora\typora-user-images\image-20230612184550075.png" alt="image-20230612184550075" style="zoom:80%;" />

    * 动量衡算（动量守恒定律和牛顿第二运动定律）

* 实验法建模：也称为统计建模方法。一般只用于建立输入输出模型。它是根据工业过程的 输入和输出的实测数据进行某种数学处理后得到的模型。

### 5. 过程的实验建模方法与示例

* **过程动态特性响应曲线的测取**

  <img src="C:\Users\28113\AppData\Roaming\Typora\typora-user-images\image-20230612185139750.png" alt="image-20230612185139750" style="zoom:80%;" />

<img src="C:\Users\28113\AppData\Roaming\Typora\typora-user-images\image-20230612185242548.png" alt="image-20230612185242548" style="zoom: 67%;" />

<img src="C:\Users\28113\AppData\Roaming\Typora\typora-user-images\image-20230612185451225.png" alt="image-20230612185451225" style="zoom:67%;" />

* **由阶跃响应曲线拟合传递函数**

  <img src="C:\Users\28113\AppData\Roaming\Typora\typora-user-images\image-20230612185727252.png" alt="image-20230612185727252" style="zoom:67%;" />

<img src="C:\Users\28113\AppData\Roaming\Typora\typora-user-images\image-20230612185802570.png" alt="image-20230612185802570" style="zoom:67%;" />

<img src="C:\Users\28113\AppData\Roaming\Typora\typora-user-images\image-20230612190051478.png" alt="image-20230612190051478" style="zoom:67%;" />

<img src="C:\Users\28113\AppData\Roaming\Typora\typora-user-images\image-20230612190116822.png" alt="image-20230612190116822" style="zoom:67%;" />

<img src="C:\Users\28113\AppData\Roaming\Typora\typora-user-images\image-20230612190307780.png" alt="image-20230612190307780" style="zoom:67%;" />

<img src="C:\Users\28113\AppData\Roaming\Typora\typora-user-images\image-20230612190343415.png" alt="image-20230612190343415" style="zoom:67%;" />

<img src="C:\Users\28113\AppData\Roaming\Typora\typora-user-images\image-20230612190405123.png" alt="image-20230612190405123" style="zoom:80%;" />

<img src="C:\Users\28113\AppData\Roaming\Typora\typora-user-images\image-20230612190446110.png" alt="image-20230612190446110" style="zoom:67%;" />

