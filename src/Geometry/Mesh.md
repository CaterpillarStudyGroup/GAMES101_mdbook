# Basic

通过定义点的位置和点之间的连续关系，来描述一个曲面。

在mesh上的操作有：  
- 网速细分：引入更多三角形，并调整顶点坐标。使表面更光滑
- 网格简化
- 网格 Regularization：使网格更接近正三角形

# 网格细分 [09：26]

目的：引入更多三角形，并调整顶点坐标。使表面更光滑

## Loop 细分算法

[11:30] (loop 是人名，不代表循环）

- 第一步： 划分三角形

![../assets/9.PNG]

- 第二步：更新new顶点的位置

![](../assets/10.PNG)

new顶点被两个old三角形共享，更新公式为：

\\[
p = frac{3}{8}(A+B) + frac{1}{8}(C+D)
\\]

- 更新old顶点的位置

![](../assets/11.PNG)

old 顶贞被多个 old 三角形共享

更新公式为：  

\\[
p = (1 - n * u) * v + n * v'
\\]


n:与old顶点连接的边数

u:一个经验值

v:old顶点更新前的位置

v': old顶点的邻居的位置 # [?]邻居的平均值？

## Catmull-Clark 细分

loop 细分只能用于三角形面片，而此算法则更通用

### 定义

Quad face：四边形面片

Non-quad face：非四边形面片

奇异点： degree不为4的点，degree 表示与点相邻的边数

### 具体步骤

- 第一步：取所有边上的中点与面上的中点

把边中点与面中总用一条线连起来
操作后，增加的奇异点个数与 操作前的non-quad face 数相同，且所有的面都变为 quad face

- 第二步： 更新面中心的新增点，

![](../assets/12.PNG)

更新公式为：

\\[
f = \frac{v_1 + v_2 + v_3 + v_4}{4}
\\]

- 第三步： 更新边中心的新增点

![](../assets/13.PNG)

更新公式为：

\\[
e = \frac{v_1 + v_2 + f_1 + f_2}{4}
\\]

- 更新 old 顶点

![](../assets/14.PNG)

更新公式为：

\\[
p' = \frac{f_1 + f_2 + f_3 + f_4 + 2(e_1 + e_2 + e_3 + e_4)}{16}
\\]


# Mesh 简化

## 边坍缩 Edge Collapse

### Quadris Error Matrics 二次误差度量

二次误差度量用于选择被坍缩的边

如果用一个点来代替原始的多个点，怎么放这个点得到的形状与原始形状最接近？

答：使用二次说美来度量。[41：17]。即 new point 到 old edge 的距离平方和最小

对任意一条边，坍缩并把 new point 放在与原始 mesh 的误­差最小的地方。 

把所有边都尝试坍缩，并计算坍缩误差，看哪条边坍缩产生的误差最小，就实际地坍缩这条边。

存在的问题：

坍缩一条边会对它周围的边造成影响。因此不能提前离线算好所有过的误差大小和排序

解触方法：

优先队列。动态更新受影响的边


----------------------------
> 本文出自CaterpillarStudyGroup，转载请注明出处。
>
> https://caterpillarstudygroup.github.io/GAMES101_mdbook/