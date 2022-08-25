# BRDF, 双向反射分布函数【29：00】

Bidirectional Reflected Distribution Function

输入：一个入射光线的角度和能量  
输出：各个反射光线的能量分布，包含镜面反射和漫反射

## 反射

反射可以理解为从某个入射角度\\(\omega\\)打到指定区域的能量radiance。  
这些radiance被区域吸收，并从这个区域向各个方向辐射。  

> &#x2705; 从吸收的视角来理解是radiance，从辐射的视角来理解是irradiance，但是所承载的能量大小是相同的。
  
## BRDF

BRDF则描述了这些irradiance会如何分配到各个立体角上去，即向某个方向辐射的radiance。  
BRDF用比例的方式来描述这种分配关系。提供某个立体角上的radiance占的irradiance的多少。  

![](../assets/122.PNG)

以上图为例：  
从\\(\omega_i\\)向指定区域辐射到的能量，也可以说是指定区域从\\(\omega_i\\)方向吸收到的能量，为：

$$
dE(\omega_i) = L(\omega_i)\cos\theta_i d\omega_i
$$

这些吸收到的能量又从这个区域被辐射出去，向\\(\omega_r\\)方向辐射的能量为：  

$$
dL_r(\omega_r)
$$

BRDF为“从某个角度辐射的能量”与“来自某个入射角度并向所有角度辐射的总能量”的比例[36:16]，或者说是“从某个角度辐射的能量”与“从某个角度接收的能量”的比例：

$$
f_r(w_i\rightarrow w_r) = \frac{dL_r(w_r)}{dE_i(w_i)} = \frac{dL_r(w_r)}{L_i(w_r)\cos\theta_idw_i}
$$

其中分子表示unit area向\\(\omega_r\\)辐射的能量，分母表示unit area从\\(\omega_i\\)接收到的能量

不同的材质会有不同BRDF。  

# 反射方程

BRDF为描述某个角度入射光对某个角度出射光的能量贡献，把得到入射角度都积分起来，得到是这个区域往某个角度辐射的能量总量。  

$$
L_r(p,w_r) = \int_{H^2}f_r(p, w_i\rightarrow w_r)L_i(p, w_i)\cos\theta_idw_i
$$

其中：   
\\(\int ... dw_i\\)：对所有入射方向的积分,，每个入射角wi对同一出射方向wr的贡献的累积  
\\(L_i(p, w_i)\\)：这个入射方向的打到区域的能量，是radiance  
\\(\cos\theta_i\\)：考虑入射方向与被辐射区域的夹角  
\\(fr(p, w_i\rightarrow w_r)\\)：把radiance分给某个出射角  

> &#x2753; [?] p是什么？代表这个区域？

> &#x2757; 任何的出射的 radiance 都会变成其它的入射的 radiance，即公式中的 \\(L_i(p, w_i)\\)不一定来自光源。
因此，**这是一个递归问题**。

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

- 理解1：1个入射光线。[47:44]
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