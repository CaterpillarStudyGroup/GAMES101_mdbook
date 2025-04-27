# 3D纹理应用

纹理不只有表面，内部也可以有值。给空间任意一点都定义一个值，就是3D纹理。

## 用于生成随机的3D物体表面

<img src="../assets/displacement2.jpg" width = 600 />

纹理并非实际定义，而是通过noise函数生成（[35:01]右）。

> &#x1F4A1; 提前准备好的方式有很多，不一定非要把每个需要的值算出来的，关键是运行时能不能很快的获取到某个值。  

## 用于体渲染

存储3D信息并用于渲染

------------------------------

> 本文出自CaterpillarStudyGroup，转载请注明出处。  
> https://caterpillarstudygroup.github.io/GAMES101_mdbook/
