# 提升分辨率

<img title="" src="../assets/时域采样和频域采样.jpg" alt="" width="536">  

分辨率上升 \\(\Longrightarrow \\) 像素格子小 \\(\Longrightarrow \\) 像素采样率上升 \\(\Longrightarrow \\) （b）间隔大 \\(\Longrightarrow \\) 混叠少 \\(\Longrightarrow \\) 减轻走样现象

缺点：受制于物理限制

# 反走样算法 [59:49]

1. 图像转为频域信号
2. 对频域信号做低通filter，过滤掉高频信息，使（b）变窄
3. 正常采样
   
   <img title="" src="../assets/采样.jpg" alt="" width="600">

# MSAA [1：05：17]

Multi Sample Anti-aliasing算法

1. Supersampling：一个象素内部划分成多个子（sub）像素 [1:05:17]
2. 判断每个子像素是否在三角形内 [1:06:59]
3. 对判断结果求平均值 [1:07:22], [1:08:55]

![](../assets/MSAA.jpg)

缺点：增加计算量

> **&#x2757;注意:** Supersampling 与提升分辨率的区别：
> 本算法并没有实质性地增加像素点

# FXAA

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
>
> https://caterpillarstudygroup.github.io/GAMES101_mdbook/
