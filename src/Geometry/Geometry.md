几何的表达方式分为隐式表达和显式表达。  

隐式表达[46:35]是指，不提供点的具体位置，只提供点应满足的约束f(x,y,z)=0

显式表达是指，直接给出所有点的具体位置，或者给出点的映射关系，例如\\(f:R^2 \rightarrow R^3\\)

实际场景中，会根据需要使用不同的表达方式

###隐式表达举例
Algebraic She。[58-10] x 班飞到
一 Constructive solid Come my。[58.233 hole 运算 .
Distinct Function Til 啊可对距离欧敌 blending .
level St Method tho:22]
Fractals 分形 [1：12：44了
优点容易描述， compact 表达 .
容易计算离表面的距离'
容易插通牌光线与表面的头角
缺点难以描述兄来对家
.


#显式几何
##点云 point cloud
list of pants
可以表示任意的几何形状
常用于扫描输出
常被转换为其它方式的使用
长井 Polygon Mesh
应用最广泛。
以三角形、四边形为主
obj 文件格式：
1 0：顶点坐标
M:法点，数量同0
比：纹理坐标，最多为顶点数糆片数个


----------------------------
> 本文出自CaterpillarStudyGroup，转载请注明出处。
>
> https://caterpillarstudygroup.github.io/GAMES101_mdbook/


Lecture 11
Geometry 2 46




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
