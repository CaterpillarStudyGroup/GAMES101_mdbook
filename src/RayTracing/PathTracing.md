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
L_o(p, w_o) = \approx \frac{1}{N} \sum \frac{L_i(p, w_i)f_r(p, w_i, w_o)(n\dot w_i)dw_i}{1/2\pi}
\\]

其中wi来自采样

### 场景2[42:41]

 v 这是我自己抽象出来的
一个函数
[42-41] fml Wi)
Lol p, Wil 元 È Etienne
fun ={心 ·卜· 心， if 心来自光源
shadelq-wilt.fr a cog. if U 来自其
- 它物体{
来自9点的直接光照
[46：48] rays = N#口灬心 会爆炸
因此取 N = l （即 path tracing)
比9：41毗足够多，会缓解心带来的噪声

##g gene 嗮
的心了 70
1.在一个鲢内采样儿个事 same'
2. sample shoot a rag
3.如果 my 碰中物体 p,
喵 pixd-radianati.hr. shade (p, sample)
4. return pixel_radiance
##如蒋解递归问题
人为定义谦 bounce 的海沙数，后面的心掉。
这会带来能量损失。
解决方案 Russian Roulette 俄罗斯轮盘赌
即不明确定义次数，而是以一定概率决定是否继续 bounce
p.
最后得到的结果除以13.
鞠其期望结果与无限 bounce 的理论结果相同
E = P 大(Lol P) t.cl-P)大 O = 6
##1张 Tracing 的性能与效率
[1200232]
###再断 随机采样
[1：02212] or
当光源大时，心1比较容易遇到光源
光源小时，大多数邶通机采样袯浪费"了

解决方法
上半球均匀采样->只在光漉上采样，
如果我来做会指使高斯分布来采样.可以控制重点 7/
采样区域的位置和大小
在上半球积分->在光源上积分
世上二巡矮y一在上半球部分优置年一
门为化公不连封毛也改成灰光源上定样~呢？-
d w = dicier
总结 [1讪汀 比从112 位体角定义）
直接高照和间接光照分开体处理
在光源上积分赛判断一个 say 出的光线是否被挡住
期##其它，
点光源当成面积很小的光源处理
是怎样对一个函或均匀采样？
3均匀采样→重要性采样
4-随机飊量对算法的影响
5. 把上毛球采样与光源采样结合起来
6. pixel reconstruction filter
7. radiance → colon, gamma 校止


------------------------------

> 本文出自CaterpillarStudyGroup，转载请注明出处。
>
> https://caterpillarstudygroup.github.io/GAMES101_mdbook/