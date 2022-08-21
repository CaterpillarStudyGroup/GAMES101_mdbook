光线追踪与光栅化是两种不同的呈像方式，但光栅化具有“can't handle global effect well”的局限性，不能呈现出以下的效果：  

![](../assets/83.PNG)  

- 软阴影  
- glossy反射。glossy是指即有点粗糙的镜子，或打模非常光滑的金属的一种材质  
- 间接光照，即光线弹射不止一次  

因此有了光线追踪技术。

光栅化速度快，质量差， 能达到real-time。光线追踪速度慢，质量好，通常用于offline。

# 光线追踪最基本的假设

1. 光线沿直线传播
2. 光线可以交叉但不发生碰撞
3. 光线从光源出发，经过不断弹射，打入眼中。
4. 光路可逆。可以理解为从眼睛出发，追踪光路直到光源。  


------------------------------

> 本文出自CaterpillarStudyGroup，转载请注明出处。  
> https://caterpillarstudygroup.github.io/GAMES101_mdbook/