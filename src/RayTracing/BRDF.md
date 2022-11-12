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

> &#x1F4A1; 老师没有详细介绍BRDF是什么样的函数。我理解就是一个概率密度函数。漫反射是均匀概率，高光是高斯概率。  

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

> &#x1F4A1; 把渲染过程中的量抽象成符号并归纳成公式，这就是刘老师所说的对问题建模的能力。  
> 同一问题，建了什么样的模型就能得到什么样的结果，因此建模的能力是最重要的。  

------------------------------

> 本文出自CaterpillarStudyGroup，转载请注明出处。  
> https://caterpillarstudygroup.github.io/GAMES101_mdbook/