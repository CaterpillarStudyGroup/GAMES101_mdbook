# Path Tracing 路径追踪

## Whited Style ray racing 的假设

光线打到光滑/小物体，会反射。  
打到透明物体，会折射  
打到普通物体，会漫反射  

局限性:  
[24：13]， glossy 物体被使用镜面反射处理了。  
[26：36] 漫反射也应该有多次弹射

Whited Style 算法有局限性，但 rendering 公式是正确的。正确解出 rendering 公式，会得到正确的算法。

## 用 Monto Calio 方法解定积分

### 场景1[32：18]

只考虑直接光照，且被照射点不发光。则入射光线为上半球所有Wi，出射光线为 Wo,求 Wo

\\[
L_o(p, w_o) = \int_{\omega^+}L_i(p, w_i)f_r(p, w_i, w_o)(n\dot w_i)dw_i
\\]

从公式可以看出，无自身发光项，且直接光照只来自光源。  

用Monto Carlio解定积分，假设使用均匀采样，将公式代入以上公式，可将连续问题转化为离散问题，得到：  

\\[
L_o(p, w_o) \approx \frac{1}{N} \sum \frac{L_i(p, w_i)f_r(p, w_i, w_o)(n\dot w_i)dw_i}{1/2\pi}
\\]

其中wi来自采样

### 场景2[42:41]

\\[
L_o(p, w_o) \approx \frac{1}{N} \sum \frac{func(w_i)}{1/2\pi}
\\]

当wi来自光源时，

\\[
fun = Li * Fr * cos
\\]

当wi来自其它物体q时，

\\[
fun = shade(q - wi) * fr * cos
\\]

[46：48] 光线路径数rays = \\(N^{#bouns}\\) 这个量级下计算量会爆炸

因此取 N = l （即 path tracing)

[49：4] path足够多，会缓解N=1带来的噪声

## ray generation [51:17]

1. 在一个像素内采样N个sample
2. sample shoot a rag
3. 如果 ray 碰中物体 p，则pixel-radiance += 1/N * shade (p, sample)
4. return pixel_radiance
 
## 如何解递归问题

人为定义 bounce 的次数，后面的cut掉，这会带来能量损失。
解决方案： Russian Roulette 俄罗斯轮盘赌
即不明确定义次数，而是以一定概率决定是否继续 bounce，最后得到的结果除以p.
其期望结果与无限 bounce 的理论结果相同
E = P * (Lo/ P) + (1-P) * 0 = Lo

## Path Tracing 的性能与效率[1:00:32]

### 分析[1：02：12]

当光源大时，N=1随机采样比较容易遇到光源
当光源小时，大多数次随机采样被“浪费”了。

解决方法：上半球均匀采样->只在光源上采样，
> 如果我来做会指使高斯分布来采样.可以控制重点

采样区域的位置和大小
在上半球积分->在光源上积分

\\[
dw = \frac{dA \cos\theta'}{||x'-x||^2}
\\]

立体角定义

## 总结 [1：11：26]

直接光照和间接光照分开处理
在光源上积分需要判断一个 sample 出的光线是否被挡住

## 其它

1. 点光源当成面积很小的光源处理
2. 怎样对一个函数均匀采样？
3. 均匀采样→重要性采样
4. 随机数质量对算法的影响
5. 把上半球采样与光源采样结合起来
6. pixel reconstruction filter
7. radiance → color, gamma 校正


------------------------------

> 本文出自CaterpillarStudyGroup，转载请注明出处。  
> https://caterpillarstudygroup.github.io/GAMES101_mdbook/