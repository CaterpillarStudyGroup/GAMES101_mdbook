# Ray-Surface 交点

## 定义

光线是一根射线，包含起点和方向，用(o, t)表示，即（起点，方向）  

![](../assets/87.PNG)  

ray equation：  

$$
r(t) = o+td, 0\le t < \infty
$$

## 光线与球的交点

ray: \\(R(t) = o + td\\)  
圆: \\((p - c) ^ 2 - R^2 = 0\\)  
⇒ \\((o + td - c) ^ 2 - R^2 = 0\\)  

![](../assets/88.PNG)  

解出t，根据物理意义可知，t应满足：（1）t是实数，（2）t>0，（3）如果有两个解，取较小的那个

## 光线与任意隐式曲面的交点

ray: \\(R(t) = o + td\\)  
曲面： f(p) = 0

⇒ f(o + td)=0
解出t

------------------------------

> 本文出自CaterpillarStudyGroup，转载请注明出处。  
> https://caterpillarstudygroup.github.io/GAMES101_mdbook/