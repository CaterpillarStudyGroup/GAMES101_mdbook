# 概率论基础

省略，见[机器学习数学基础](https://windmissing.github.io/mathematics_basic_for_ML/)

PDF：概率密度函数

# 复习渲染方程

复习渲染方程，回顾求积分的业务背景

\\[
L_o(p, w_o) = L_e(p, w_o) + \int_{\omega^+}L_i(p, w_i)f_r(p, w_i, w_o)(n\dot w_i)dw_i
\\]

其中：  
第一项：自己发的光  
Li：接收到的光  
fr：反射参数，与材料有关  
n*wi：夹角  
dwi：积累所有的方向

# 蒙特卡罗积分 Monto Carlo Integration

目标：求定积分\\(\int_a^bf(x)dx\\)  
方法：在积分域内不断地采样，并对采样结果平均，则：  
\\[
\int_a^bf(x)dx \approx E(f(x))(b-a)
\\]

另一种理解：  
使用\\(X_i ~ p(x)\\)为[a, b]的随机采样，可以是任意的采样方式。则：  

\\[
F_N = \frac{1}{N}\sum\frac{f(X_i)}{p(X_i)}
\\]

好处：只需要能对[a b]以一定方式采样，就可以求出定积分


------------------------------

> 本文出自CaterpillarStudyGroup，转载请注明出处。
>
> https://caterpillarstudygroup.github.io/GAMES101_mdbook/