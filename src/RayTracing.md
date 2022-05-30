Lecture 13
Ray Tracing 光线追踪 歼
光线追踪与光栅化是两种不同的是像方式
光栅化的局限性
cant handle global effect well
0轮阴影
② 和对反射即有点粗糙的镜子，或打模非常光滑的金属
③ 间接光照，即光线弹射不止一次
光栅化速度快，质量差， recline,
光线追踪速度慢，质量好。 offline
璵光线沿直线传播
2.光线远但不发生碰撞 避
3.光线以"无源出发，经过不断弹射，打入眼中.何逆）
#假设
人光源是点光源。
2.camera 是一个点
3.完美折射
在 Bathe 算法[20：4曲
UH、目良曰高向每个人象素抄一出一木艮光全成邀

2.光线和场景相交，求最近的交点
3.数点与光源连线，判断定是否在阴影中
4. 算着色 55
5.驷像素值
# Whited-风格算浇涵刘
世-[25、订
l. 经过反射和折射会经过多个弹射点的啊
2对每个弹射点都计算着色的鱼[25：42]
3.如果某个弹射点能被光源照时，
其着色鱼都会被加到所看的借谋上去[26：23]
-0㙽煳 反射能量十折曲射能量到
一些名词： primary rag, secondary ray, shadow rg
#tt Rg-Surface 交点
定义、
光线上（0.tl#比起点，方向）
光线上的某一点 0 ttd.at 30
###光线与球的这点
my R.lt)=0 ttd
恩 lp-cr.pro}⇒（0 ttd-c.FR:0
解出 t.

取大和且较小的 t
###光线与隐式曲面的这点 56
光线 rrctlwttd
曲面： ftp.io 了⇒ f(oetd)=0
解出6-
###光线与三角形面片的交点
话意个点与 mesh 求交，赚，澍刚
交点个数为奇数点在内
- -_-偶数。-_-外。
####光线和三角形的这点
与 用 在 这点
→ 叉垂为0代表垂直
霜上的一个野平面的法线
咒线上 rcttottd
组合 cottd-M.NO 解出 t
解得。 t = 心-03.N-rr.­de N
2-判断就是否在三角形内
或 MT 算法。 (P 37）
点在三角形内一点用三角形的重心坐标表示且满是 constrain
0 t t D =（1-b、一则 Potb.P.tb.pe
大写为3日已知向量
小写为未知标量

t r
卧在1㔐 》
判定键结果比的条件。 rzo.b.zo.bz 20. l-bib.io
####算法加速
Bounding Volumes 包围盒[56：40]
1.长方体.3个不同的对面形成的这集的冯6了
比的）
AABB.mn Aligned
※ 往㐜爨鸞的䪍，
tmn 和对 max
年对面 对面
光线进入 AABB 的时间为所有瓦 mint mad 的交集
tenter = mhtmwjtexisiminftmal­itenterctex.it ⇒光线5A ABB 相这
texistc.co ⇒不相载交
tuna oates。*→光源.在 AAB 日内

Q:为什么要用 AABB
A:光线与朋平面求交的计算简单 58
[k 心生9]
t =心些 普通平面
d. N ˙
t
t =口'二 AA 平面
dx

Lecture 14.
光线追踪2 59
#怎样利用 AA 的加速 ray tracing
##均匀的格子 Uniform Grids [8：13]
l. 找到场景的 Bounding Uohmn
2捌孔划分成格子
3.每判断每个 Grid 是否有物理体
4假设，光线与 Grid 求交很快，与 object 救很慢
判断光线与 Grid 是否相交，
皉内是否有 object
光线与 grid 内的 object 是否求交
grid 不能太疏或密 木邀一.位置均可
适用于 object 的大小和任罚一
不适用于 obpr 分在不均匀的场景
##空间划分 Spatial Partition
[18-59] Octree, KD tree, 138 P tree
视频以1的 Tree 为例子。
### 如母划的 Tree 的数据结构
- 中间结点
划分轴：人以飞轮氵礼

划分点根据特定的策嗨选择
child:2个
object: 不存 object 数据 60
-叶子结色
、 存 list of objects.
###Traverse.
𨫡归
##*1局限性
如何判断1孔与0相交。
{object 存在于多个1-叶子结蚛
##物体划分 Object linen
##=11 But [40：00]
优点解蚍让2全问题
局限性： BV 有重叠，
好的划分使重叠尽量少
####Gate
l. 计算 B V
2对吼内的将划分9
####在比比一
选择划分轴藜最长的轴划分
选择划分点20取中间的物体。
譢牛：13中的0个数

####Traverse
同上 6/
KD Tree 的 But [54河
井 Basic radio meting 辐射度量学
# tt Background.
（物理方法）。
1-用单位和方法定义光
2为先定义了一些属性
WHY → WHAT-> HOW
井井 Radiant Energy and Flux (Power)
定义：
Radiant Energy..能量 Q. 单定-J
Flux = lower:单位时间的能量 op
0人器，单优= W
[1：09：56]
###Radiant Intensity
定义： power per unit solid angle.
t
Iwǘ 器-7就=[剁

立体角。[1：13：19下了
212 0= Ìr, G [0.2到 62
3日：几二念， G [o 4到
单位嫩体角、
IN 431空间中一个方向用0和4表示，
叫， unit solid angle = snoddy
上炭

Lecture 15
Ray Tracing 3 63
#定义
Radiant energy:能量
Radiant flux:单位时间的能量
Radiant intensity:单位时间、单位面积上的能量
# Irradiance
power per unit area
E 比）三去礜，单位：[器]
人与光线垂直的面积
㊀ ·（一一 䭳鑾的工呲呲为
4[r'
当 r 变大.不是 Intensity 在衰减，
# Radiance [19人350了 而是 Irradiant 在衰减
power per 䢤㭪 per unit 投影面积
单位1点1

LCP.wjzd­dwd.lt 的0 64
理解1： Irradiance per 立体用
Ǜ 这是一个薄 unit Area.
它辐射的总能量为 Irradiance
它向方向 W 辐射的能量强度为 Radiance
理解2：
沿着 w 方向到达州的能是为 home
位有方向到达比1的能量的总和为 Irradiance
# BR.DE, 双向反射分布函数
输入。一个入的光线的角度和能是
输出。各个反射光线的能量饰，包含镜面反射和漫反射
f. (W i →州= 比- [36-16了
𧒄变出射角度 d Ei (Wi)
- dhlwr) unit area 向以辐射𡄯。
- netti unit ǎeawwi 接收到的
Li WH 的0 id Wi 能量
lip,叫=卜丛2e.tt?监测雌飍㴇
把 radians 给斯 radiance, 对同一出䑻向以
出游用 的趟大加起来

住的发射的 radiance 都会变成其它的，谢子 radiance,
即公式中的 Lilpwi)不一定来自光源 65
##渲染方程
L.42. w。）=自已发说十 The
来自其它的反射断直射光
定义积分域为上半球，即不考虑折射
理解1： 线
1个入射光海。[47州
理解不
多个八射光线 [47：57了
理解子，
1个面光源 [4830]
理解4：
考虑其它物体的反射光釉入射光线149上到
这里涉及到递归
简化公式得
In 二 Eethwikcud
能发光 hint 龌属性
未饢 to

进一步简化。
L = E t K L 66
解得.
Li Et KE t KE t HE t-'
飝照 hrntnn.no
间接光照
-
全局光照
！！
晀信息
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




------------------------------

> 本文出自CaterpillarStudyGroup，转载请注明出处。
>
> https://caterpillarstudygroup.github.io/GAMES101_mdbook/