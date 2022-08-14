# 反走样

## 提升分辨率/采样率

<img title="" src="../assets/时域采样和频域采样.jpg" alt="" width="536">  

分辨率上升 \\(\Longrightarrow \\) 像素格子小 \\(\Longrightarrow \\) 像素采样率上升 \\(\Longrightarrow \\) （b）间隔大 \\(\Longrightarrow \\) 混叠少 \\(\Longrightarrow \\) 减轻走样现象

缺点：受制于物理限制

## 反走样算法 [59:49]

在物理条件不变的情况下解决走样问题

### 原理：把可能混叠的部分切掉

   <img title="" src="../assets/采样.jpg" alt="" width="600">

### 具体方法：

1. 使三角形变模糊
 - 对于三角色形上任意一个像素点，原来是根据像素点中心是否在三角形内来判断着色。
 - 现在的做法是，判断整个像素点有多少面积在三角形内来计算着色（卷积）。  

![](../assets/32.PNG)  

2. 正常采样
   
### 局限性

面积难以计算

## MSAA [1：05：17]

Multi Sample Anti-aliasing算法，反走样算法的近似算法

### 具体方法

1. Supersampling：一个象素内部划分成多个子（sub）像素 [1:05:17]
2. 判断每个子像素是否在三角形内 [1:06:59]
![](../assets/MSAA.jpg)    
实际在这一步中不会这样均匀的划分，而是采样更合理的方法，在达到效果的同时尽量少地提升计算量。  
3. 对判断结果求平均值 [1:07:22], [1:08:55]  
![](../assets/33.PNG)

### 局限性

缺点：增加计算量  

> **&#x2757;注意:** Supersampling 与提升分辨率的区别：
> 本算法并没有实质性地增加像素点

## FXAA

Fast Approxiamte Anti-aliasing算法

1. 用常规方法得到带锯齿图像
2. 通过图像匹配的方法找到边界
3. 把边界换成没有锯齿的边界

优点：速度快， 与采样无关

# TAA [1：15：10]

Temporal Sample Anti-aliasing算法

> &#x1F50E;
Temporal： 时间上的

大概意思是，边界上的点，有时显示在上一帧，有时显示在这一帧


----------------------------

> 本文出自CaterpillarStudyGroup，转载请注明出处。  
> https://caterpillarstudygroup.github.io/GAMES101_mdbook/
