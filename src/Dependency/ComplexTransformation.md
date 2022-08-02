# 变换合成与分解

- 复杂变换可以通过简单变换一步一步达到
- 变换顺序非常重要，ABC不等于ACB（矩阵乘法性质）

变换合成：

<div align="left"><img src="../assets/结合律.jpg" width = 400 /></div>

变换分解：

<div align="left"><img src="../assets/分解.jpg" width = 500 /></div>

以C点为中心的旋转，可以分解为：

1. 从C点平移到原点
2. 旋转
3. 再从原点平移到C点

即：\\(X'=MX=T\left( c \right) \cdot R\left( \alpha \right) \cdot T\left( -c \right) \cdot X\\)


-----------

> 本文出自CaterpillarStudyGroup，转载请注明出处。
>
> https://caterpillarstudygroup.github.io/GAMES101_mdbook/