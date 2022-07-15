# Ray-Surface 交点

## 定义

光线：(o, t)，即（起点，方向）  
光线上的某一点： o+td, t>=0

## 光线与球的交点

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
