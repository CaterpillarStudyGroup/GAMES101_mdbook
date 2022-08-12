# 着色频率

BlinnPhong模型描述了单点如何着色。  
着色频度描述如果对所有点着色。即以什么样的策略对每个点运用BlinnPhong。  
[20:50]

对于同一个几何模型，不同的着色频率会产生不同的效果：

![](../assets/36.PNG)

以下是几种不同的着色频率（着色策略）：

## 着色就用于平面

1. 着色应用于一个平面上,整个平面共用一个L（Flat Shading）
   
   <img src="../assets/flatshading.jpg" width = 300 />

2. 着色应用三角形面片的顶点上，每个顶点计算一个L，三角形内通过插值计算出L（Gouraud Shading）
   
   <img src="../assets/gouraudshading.jpg" width = 300 />

3. 着色应用于像素，每个像素计算一个L（Phong Shading）
   
   <img src="../assets/phongshading.jpg" width = 300 />


不同着色频率和着色几何体的效果比较：

<div align="center"> <img src="../assets/shadingcompare.jpg" width = 600 /> </div>

------------------------------

> 本文出自CaterpillarStudyGroup，转载请注明出处。
>
> https://caterpillarstudygroup.github.io/GAMES101_mdbook/