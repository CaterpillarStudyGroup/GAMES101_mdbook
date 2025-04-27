# 材质与外观

外观是材质和光线作用的结果。因此本章要学的是**不同材质和光线相互作用的方式**。   

材质是渲染方程中的 BRDF 项

# BRDF的性质

- 非负性

$$
f_r(\omega_i\rightarrow \omega_r) \ge 0
$$

- 线性

可以把BRDF拆成很多块分别做path tracing再加起来，得到的结果与整个BRDF做path tracing的结果相同。  
> &#x2753; 拆成多块是什么意思？BRDF不是概率密度函数吗？为什么可以直接相加？不是对入射光做叠加吗？  

- 可逆性

$$
f_r(\omega_i\rightarrow \omega_r) = f_r(\omega_r\rightarrow \omega_i)
$$

- 能量守恒

出射能量一定不多于入射能量。  

- 各向同性：

$$
fr(\theta_i, \phi_i;\theta_r, \phi_r) = fr(\theta_i, \phi_i, \phi_r - \phi_i)
$$

其中\\(\theta_r\\), \\(\phi_r\\)为方位角

# BRDF的测量

好像跟算法没关系，不记了。

> &#x2705; 实际上BRDF的获取也是图形学的重要内容。  

------------------------------

> 本文出自CaterpillarStudyGroup，转载请注明出处。  
> https://caterpillarstudygroup.github.io/GAMES101_mdbook/