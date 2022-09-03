# 漫反射材质

漫反射是指：任何方向的光线进来，都会被均匀地反射到各个方向去。  

假设：入射光是 Uniform 的，出射光是漫反射，也是 uniform 的，那么BRDF项为fr = c（c 的数值与颜色有关）

$$
L_o(\omega_o) = \int L_i f_r \cos\theta_i d\omega_i
$$

这种情况下，Li*fr这一部分是常数，可以提取到wi外面，得：

$$
L_o(\omega_o) = L_i f_r \int_{H^2}\cos\theta_i d\omega_i = \pi f_r L_i
$$

化简得：  

$$
fr = \frac{1}{\pi} (\frac{L_o}{L_i})
$$

假设材质不吸收任何能量，根据能量守恒，\\(L_i = L_o\\)，则：  

$$
fr = \frac{1}{\pi}
$$

但如果材质会吸收任何能量，则：  

$$
\rho = \frac{L_o}{L_i} \lt 1
$$

\\(\rho\\)称为散射率albedo，范围[0，1]，数值与颜色有关。  



------------------------------

> 本文出自CaterpillarStudyGroup，转载请注明出处。  
> https://caterpillarstudygroup.github.io/GAMES101_mdbook/