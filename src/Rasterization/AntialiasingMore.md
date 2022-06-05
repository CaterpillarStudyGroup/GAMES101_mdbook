# 提升分辨率

<img title="" src="../assets/时域采样和频域采样.jpg" alt="" width="536">  

分辨率上升 \\(\Longrightarrow \\) 像素格子小 \\(\Longrightarrow \\) 像素采样率上升 \\(\Longrightarrow \\) （b）间隔大 \\(\Longrightarrow \\) 混叠少 \\(\Longrightarrow \\) 减轻走样现象

缺点：受制于物理限制

### 反走样算法

1. 信号转频域
2. 低通filter，过滤高频信息，使（b）变窄
3. 采样
   
   <img title="" src="../assets/采样.jpg" alt="" width="600">


###  其他反走样算法

[1：05：17]

#### MSAA

1. 一个象素内部划分成多个子（sub）像素
2. 判断每个点是否在三角形内
3. 把判断的结果平均

![](../assets/MSAA.jpg)


> **&#x2757;注意:** Supersampling 与提升分辨率的区别：
> 本算法并没有实质性地增加像素点
>
> 缺点：增加计算量


#### FXAA

1. 用常规方法得到带锯齿图像
2. 通过图像匹配的方法找到边界
3. 把边界换成没有锯齿的边界

优点：速度快， 与采样无关

#### TAA 

[1：15：10]

**T** ：Temporal .时间上的

大概意思是,边界上的点，有时显示在上一帧，有时显示在这一帧

### 其它问题

#### Super Resolution 超分辨率

- 低分辨率图拉大成高分辨率出现的锯齿问题
- 解决方法，一 DLSS
- Deep Learning Super Sampling

#### Super Sampling 上采样

跟上面是同一个问题。

----------------------------
> 本文出自CaterpillarStudyGroup，转载请注明出处。
>
> https://caterpillarstudygroup.github.io/GAMES101_mdbook/
