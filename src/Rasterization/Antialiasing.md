# 走样

<img src="../assets/走样.jpg" title="" alt="" width="425">

当按照像素中心是否在三角形内的采样方式采样后，得到了不理想的结果。

产生了锯齿！（jaggies）

消除锯齿是图像学致力于解决的重要问题。

抗锯齿，也叫反走样。

# Antialiasing 反走样的定性分析与解决方法

## 采样理论

Photo是对image的采样  
video是在时间维度的采样[07:33]  
它们都是将连续的信息离散化。  

采样会产生 Artifact，例如：

- 锯齿[09:17]
- 摩尔纹[09:30]
- 车轮效应

Artifact的本质原因：信号变化太快，采样速度跟不上

## 反走样方法

[14:05]

object --> 模糊化 --> 采样

模糊化，即滤波。

采样后，中心点红色，边界点粉红色

![](../assets/模糊采样.jpg)



----------------------------
> 本文出自CaterpillarStudyGroup，转载请注明出处。
>
> https://caterpillarstudygroup.github.io/GAMES101_mdbook/
