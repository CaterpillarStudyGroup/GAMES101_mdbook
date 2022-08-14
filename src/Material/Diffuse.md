# 材质与处观

材质是渲染方程中的 BRDF 项

# 漫反射材质

## 场景一

假设：入射光是 Uniform 的，出射光是漫反射，也是 uniform 的，那么BRDF项为fr = c（c 的数值与颜色有关）

\\[
L_o(w_o) = \int L_i * f_r * cos dw_i
\\]

这种情况下，Li*fr这一部分是常数，可以提取到wi外面，得：

\\[
L_o(w_o) = L_i * f_r * \int_{H^2}cos\theta_i dw_i = \pi f_r L_i
\\]

\\[
fr = frac{1}{\pi} frac{L_o}{L_i}
\\]

\\(frac{L_o}{L_i}\\)是散射率albedo，范围[0，1]，数值与颜色有关

## 场景二[16:14]

类似镜面反射的材质。例如铜镜

## 场景三[17:40]

折射 + 反射，例如玻璃和水

### 反射公式

入射角 = 出射角

\\[
w_i + w_o = 2(w_i \ dot n ) n
\\]

说明：  
\\(w_i\\)：入射光  
\\(w_o\\)：出射光  
\\(2(w_i \ dot n )\\)：大小为wi在n的投影长度的2倍  
n：方法向法线方向相同

[?]第2种方法没听懂？

### 折射

折射定率[28:00]：

\\[
\eta_i sin \theta_i = \eta_t \sin \theta_t
\\]

说明：  
\\(eta_i\\)：不同材质有不同折射率。  
\\(theta_i\\)：入射角  
\\(theta_t\\)：出射角  

当入射材质折射率>出射材质折射率，有可能折射变为全反射

BSDF(散射) = BRDF(反射) + TDF(折射)

# 菲涅耳项 [36：11]

反射和折射同时发生时，分别各多少  
答：与入射角有关，计算公式[41：55]


------------------------------

> 本文出自CaterpillarStudyGroup，转载请注明出处。  
> https://caterpillarstudygroup.github.io/GAMES101_mdbook/