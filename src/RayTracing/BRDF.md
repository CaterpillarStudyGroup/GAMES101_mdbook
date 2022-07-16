# BRDF, 双向反射分布函数

输入：一个入射光线的角度和能量  
输出：各个反射光线的能量分布，包含镜面反射和漫反射

[36:16]

\\[
f_r(w_i->w_r) = \frac{dL_r(w_r)}{dE_i(w_i)} = \frac{dL_r(w_r)}{L_i(w_r)\cos\theta_idw_i}
\\]

其中分子表示unit area向wr辐射的能量，分母表示unit area从wi接收到的能量

\\[
L_r(p,w_r) = \int_{H_2}f_r(p, w_1->w_2)Li(p, w_i)\cos\theta_idw_i
\\]

其中：   
fr：把radiance分给某个出射角  
Li：radiance  
dwi：每个入射角wi对同一出射方向wr的贡献的累积

任何的出射的 radiance 都会变成其它的入射的 radiance，即公式中的 Li(p, wi)不一定来自光源

# 渲染方程

Lo(p, wo) = 自己发光 + 来自其它的反射或直射光。  
定义的积分域为上半球，即不考虑折射。

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

#概率论
随机变量- X ~ pen
- 䨻乻，：：：新洲箭㵘𣁦
乍拽 ⇒比的二比忷了二/和輫的收

Lecture 16
Rag Facing 67
-#复习.渲染方程
##→ 自泼的光
lip, wo)= help, wo)
thilP_thi.fi wild
雦的光 谢繇与材质有差蓈䉮
井井概重论
PDF:概率密度不人数
##蒙特卡罗积分 Mont Carlo Integration
求定积分 Sdtxjh
在积分域内不断地采样。
后段设人口 fexidt.fi)。(b-a)
采多次，对结果作平均
另一种理解
求定积分 hit d,
使用人~124）为区的随机采样

Moh Carlo estimation
1元= Ì Efts 68
p 以门
好处：只需要能对[a b]以一定方式采样，
就可以求出定积分
# Path Tracing 路经追踪
Whited Style ray racing 的假设.
l. 光线打到光滑/小物体，会反射。
打到透明物体，会折射
打到普通物体，会漫反射
局限性，
[24：13]， glossy 物体被使用镜面反射处理了。
[26：36了漫反射也应该有多㲿崥射
Whited Style 算法有局限性，但 rendering 公式是正确的一
正确解出 rendering 公式，气得到正确的算法
##用 Mont Cali 方法解定积分
1=1##场景。
[32：18]，
只考虑直接光照，且被照射点不发光
入射光线为上半球们有 Wi
出的光线为 We,求 Wo

hip, who hii lp.wi.frlp.wi.ws cnwilawi
无自身发光页 儿照云霞来自光源、 G
用 Mate 继解定积分
hi MM =尤之「箭 佬薟蒲均匀采样
连续问题转化为离散问题
二式 ELilPNilfrlP.wi.wohnui.nrr.­hr/2E
其中心来目采样
Ft Ft#场景2 v 这是我自己抽象出来的
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
