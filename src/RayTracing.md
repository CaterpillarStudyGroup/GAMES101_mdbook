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

