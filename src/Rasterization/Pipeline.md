Lecture 5
Raster nation hiring les) zz

光栅化的前提敏作：
0的比在[t,门子空间中

# 定义
## 定义一个 aebncil.ae 㺦 U.d.fi n

## 定义一飜 wboid:

对称。 1=-r, but
宽商比 Aspect ratio = Uh . 、
视角。 field g viewer on a,由
^
※ 、㡭心"𪈳㘜
可得出跳 tan 答=齿
只需要定义能和 Aspect ran,其它的都能赚推出、

## 定义一个屏幕

由䳰(pixel)组成的2日翻数组，
Raster.屏幕
Raster ize 光栅化、即把戚栖画在屏幕上
pixel.像素， picture element
一个小方块，且5块内颜色不变
屏幕定国在屏幕上的坐标系

像季坐标.
Terex 頾䵹，呲州 23
（0.0） [0， hight)
续素中心位于以10.5. y-105）

# cube → Screen

使用 trmstom.mx,
呵虊䴏：一䵼
i =22先不管
. hrnrnn.net hr­ni 三宿方又 平移

# Triangles → 12汉比 [25 w]

## 显示器

各种显示器及其物理原理，
与图形学算法相关度低，
跳过。
## Triangle Mesh.一三角形面片'

我为什么用三角形？
l. 最基础的多边形
其它多边形可拆成4.△可拼成其它多边形
2一个 o-定在一个平面上

去 0关于"内"。"外"的定义是明确的
4给定△三个顶点的属性，△内部任意点的 24
属性可通过插直得出.
obj 的表面是由 triangle mesh 拼成的。
通过 MVP,可以把 obj 上的每个0都映射到屏幕空间[43州

## o → pixel value 二维空间

[43：13]左、映射到屏幕 transitional
有用12吨 value 表示△
即判断 pixel 中心点与0的位置关系

###Sampling,采样方法[43：57]

[46：16] 以 n t
判断像素中心是否在△内，
勤是. inside it. ay)={1， 是
0， 否
o 像素 ci.jo 的中心是(it 0.5， jto.sn
② 如何判断点比心是否在三角形 t 内.
见12151，向量的叉乘
缺点。 chew all pixels.

### Bounding Box 缺点八-_-.^ i i

[56：00] . i ,这种情
0根据3个顶点计算 B Box itttfi 况㿟
、 i 较大的
② 只 check 1313以内的 pixel it.... i 多余㠆
### Incremental 三角形通西 -

[56：55]

t .
这一步的最终效果比02：38] [1：03：01]
锯齿→抗锯齿。走样→反走样 25
