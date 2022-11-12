# 纹理映射

目的：把纹理应用到渲染中，使屏幕上的点p=(x,y)呈现出颜色

1. 找出p在投影前的坐标p'=(x,y,z)
2. 计算p'的(u,v)，如果p'不是顶点，则需要用到上一节的插值。  
3. 从texture中取出(u,v)点的值pv
4. 设置p的值为(u,v)点的值为pv

> &#x1F4A1; pv值对应漫反射项公式中的kd，高光项中的ks通常设置为白色。视频中没有说环境光照项中的ka怎么定义，但肯定是跟pv无关的，因为pv是每个点都不同的。


------------------------------

> 本文出自CaterpillarStudyGroup，转载请注明出处。  
> https://caterpillarstudygroup.github.io/GAMES101_mdbook/