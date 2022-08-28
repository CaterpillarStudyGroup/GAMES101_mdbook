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

- 可逆性

$$
f_r(\omega_i\rightarrow \omega_r) = f_r(\omega_r\rightarrow \omega_i)
$$

- 能量守恒

出射能量一定不多于入射能量。  

# BRDF的测量

好像跟算法没关系，不记了。

------------------------------

> 本文出自CaterpillarStudyGroup，转载请注明出处。  
> https://caterpillarstudygroup.github.io/GAMES101_mdbook/