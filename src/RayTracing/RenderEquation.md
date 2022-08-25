# 渲染方程

Lo(p, wo) = 自己发光 + 来自其它的反射或直射光。  

$$
L_o(p,w_o) = L_e(p,w_o) + \int_{\Omega^+}L_i(p, w_i)f_r(p, w_i, w_r)(n \cdot \omega_i)dw_i
$$

说明：  
\\(H^2\\)或\\(\Omega^+\\)：都是表示半球  
\\((n \cdot \omega_i)\\)：和\\(\cos\theta\\)是一个意思。参考[link](../Dependency/Vector.md)  
定义的积分域为上半球，即不考虑折射。  
第一项：自己发光超某个方向辐射的能量。  
第二项：从各个角度来的反射光或直射光向某个方向辐射的能量。  

# 理解1：1个入射光线。[47:44]

![](../assets/123.PNG)  


- 理解2：多个八入射光线 [47：57]
- 理解3：1个面光源 [48：30]
- 理解4：考虑其它物体的反射光作为入射光线[49:31]
这里涉及到递归，简化公式得：  

\\[
I(u) = e(u) + \intI(v)k(u,v)dw
\\]

其中：  
I(u)：未知量  
e(u)：自己发的光  
I(v)：未知量  
k(u,v)dw：材料属性

进一步简化得:

L = E + K L 

解得:

\\[
L = E + KE + K^2E + k^3E + \dots
\\]

其中：  
前2项为光栅化信息  
除第一项以外都是全局光照  
1次项KE为直接光照  
后面项为间接光照  

------------------------------

> 本文出自CaterpillarStudyGroup，转载请注明出处。  
> https://caterpillarstudygroup.github.io/GAMES101_mdbook/
