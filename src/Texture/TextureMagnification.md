# 问题描述

Texture Map 是256X256的，而要投影的屏幕是4K的，会导致多个屏幕像素对应一个纹理像素。

效果：

<img src="../assets/nearest.jpg" width = 400 />


# 双线性插值 Bilinear Interpolation

## 原理

<img src="../assets/bilinear.jpg" width = 500 />

1. 取对应格子的值
2. 取邻近四个纹理像素(a,b,c,d)再根据(u,v)在a,b,c,d中的位置插值出(u,v)处的值，即分别做一个横向插值和竖向插值

## 具体步骤

Linear interpolation(1D)：

\\[lerp\left( x,v_0,v_1 \right) =v_0+x\left( v_1-v_0 \right) \\]

Two helper lerps:

\\[u_0=lerp\left( s,u_{00},u_{10} \right) \\]

\\[u_1=lerp\left( s,u_{01},u_{11} \right) \\]

Final vertical lerp, to get result:

\\[f\left( x,y \right) =lerp\left( t,u_0,u_1 \right) \\]

## 效果

虽然还有点模糊，但不是颗粒感的

<img src="../assets/bilinear2.jpg" width = 400 />


# 双向三次插值 Bicubic

1. 取周围16个点
2. 三阶插值

效果：

<img src="../assets/bicubic.jpg" width = 400 />




------------------------------

> 本文出自CaterpillarStudyGroup，转载请注明出处。
>
> https://caterpillarstudygroup.github.io/GAMES101_mdbook/