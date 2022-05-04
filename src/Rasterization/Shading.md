# 可见性/遮挡

**背景：**

有多个物体，每个物体都有多个三角形，因此要处理摭挡问题。

**画家算法：**

![](../assets/画家算法.jpg)

由远及近的在画布上添加新物体

back-> front，覆盖

1. 排序 O(nlogn)
2. 光栅化
   
局限性[09:26]：无法决定深度

**Z-Buffer 算法**

名称：depth buffer， Z buffer，或深度缓存

> **&#x1F4CC;** 为了解决画家算法无法决定深度的局限性

[10:40]

为了便于计算，物体上每个点的Z坐标都取其绝对值（深度）

因此：
1. Z(depth) > 0
2. Z(depth) 小-->近， Z 大-->远

> **&#x1F4CC;** 我们约定摄像机在坐标原点，看向-Z轴，深度是一个物体距离摄像机的Z轴距离的绝对值。

每次生成2张图：

![](../assets/zbuffer.jpg)

1. frame buffer：存最终结果
2. depth buffer：存某个像素点对应的物体上的最小的depth（最近）

> **&#x1F4CC;** 
> 
> ![](../assets/depthbuffer.jpg)
> 
>  图中，A点是距离视点（摄像机）较近的点，所以颜色比较黑，B点是距离视点较远的点，所以颜色比较白。距离视点近的像素点，颜色就比较黑，反之比较白，这就是depth/Z buffer。


具体步骤

```
Initialize depth buffer to ∞
during rasterization：
    for triangle in triangles:
        for (x, y, z) in triangle:
            if z < zbuffer[x, y]:
                framebuffer[x,y] = rgb
                zbuffer[x,y] = z
            else:
                pass
```

1. depth buffer 所有像素初始化为无限远
2. 对每个三角形做光栅化，每次绘制三角形时，计算当前像素在三角形上的深度Z
   如果Z小于depth buffer上对应点的值，就绘制该点，且更新depth buffer。

> **&#x1F4CC;** 深度缓存发生在每个像素内。


算法特点
1. O(n)
2. 与三角形的绘制顺序无关
3. 可以与MSAA算法兼容
4. 适合GPU优化（因为与绘制顺序无关）


# Shading 着色

![](../assets/着色对比.jpg)

（左）不考虑着色的效果；（右）期望达到的效果。

纯色立方体的每个面每个时刻呈现的颜色有变化。使整体效果更真实。

课程中的shading:

- The process of applying a material to an object.

对不同物体应用不同材质的过程，不包含给object添加投影的过程。

> **&#x1F4CC;** 场景不变，光源发生变化，物体的位置没有改变但是颜色却变化了，这个过程就是着色。

> **&#x1F4CC;** 不同材质的物体看起来不一样，是因为不同材质与光源作用结果不同。



## Blinn-Phong 反射模型

（一个简单基础的模型）

![](../assets/reflection.jpg)

- 高光(Specular highlights): 光线反射到镜面反射附近
- 漫反射(Diffuse reflection): 光线被反射到各个方向上，
- 环境光(Ambient lighting): 假设任何一个点会接收到来自环境的常­量的光

**定义**

![](../assets/shadingpoint.jpg)

- shading point：当前要计算着色的点，位于物体表面。
- （n）Surface normal：假设点附近极小范围内是一个平面，n为平面指向外的法向量
- （v）Viewer direction：观测方向
- （l）Light direction：光源方向，与光照向point的方向相反

object 在 point 处的属性: color、shininess

**漫反射**

[47:35]

![](../assets/diffuse.jpg)

打到 point 上的光线被均匀地反射出去，（与观测点v没有关系）

![](../assets/lambert.jpg)

l 与 n 的夹角决定了 point 接收到的光线的强度(Lambert's cosine law)

![](../assets/lightfalloff.jpg)

[54:48] 圆心是点光源，向外辐射能量。

（能量守恒定理）不考虑传播损耗，每个圆上的能量之和不变，某点处的能量与它到光源的距离平方是反比。

\\[
L_d=k_d\left( I/r^2 \right) \max \left( 0,\boldsymbol{n}\cdot \boldsymbol{l} \right) 
\\]

- \\(L_d\\) 漫反射的能量
- \\(k_d\\) point对光的吸收率
- \\(\left( I/r^2 \right)\\) 有多少能量到达了point
- \\(\max \left( 0,\boldsymbol{n}\cdot \boldsymbol{l} \right) \\) 从正面照射的光，漫反射才有意义
- \\(\boldsymbol{n}\cdot \boldsymbol{l}\\) 表示有多少能量被point接收


Lecture 8
Shading 2 34

## Fi Bling-Phong 反射模型

高光项
R 为物体事镜面反射的方向。
当0和 R 接近时，会看到高光
108-25]：当0和几接近时，世1）的方向与几接近。
h. = |蕊、代表了 Ctl)的方向，
h. 称为半程向量 half vector
L. 二点_沁（1 maxton
通常认为 肯多少能量到 小儿和人的接近程度
高光颜色 达了 point.
是白色
Ls 同样应考虑有多少能量被接收，但 Bling thong 模型
将这个因素简化了。
Note..注意光线袚接收和被"吸收"的区别。
问：为什么用 n_n 代替 R.io?
答。因为 n.in 更容易计算
间、公式中为什么会有指数12？
答。[12：14]在保证函数趋势不变的同时让高光范围更集中
p 通管敬上心-200]

环境光照项
假设。所有 point 接收到来自环境光的强度 35
相同，且为常数
[a = K a I a 与1和0无关
L-l.cl t lot La
间。为什么不考虑 point 到0的距离对能量的影响？
答：这部分比较复杂、 Bling-phong 模型没有考虑这个问题
#着色频率[心打
图1.着色应用于一个平面上。整个平面共用一个人。(Flat Shading)
图2.着色应用三角形面片的顶点上，每个顶点计算乱 Garand
三角玛内通过插值计算出 L Shading)
图3、着色应用于像素，每个借谋计算一个 Lil Phong Shading
所40了不同着色频率和着色几何体的效果比较

## 计算一个点的法向量。

方法-利用几何特征
例如已知 object 是个球体。可直接球出球表面荒点的几
方法二。利用涌形面片。[3008]
N。= 医 Ni
Hirth 相邻面的 N 的平均
或加权平均一
方法三：利用插值[31229]

式 Real-time Rendering Pipeline
实时渲染管线1332123 36
[35：24]
建模→几何处理一光栅化
→ 着色→帧缓存
基于 OpenGL 的着色编程是工程问题，跳过
井纹理映射 Texture Mapping [54：50]
[55：59]
[a = K d *(I / k'） *(n.LI
Yfhlhtnht tnrnneezrott
不同点的颜色不同 小球上所有点处于相同的一光照环境下
object 在不同豳处的点需要定义不同的属性，
上面例子中的1化是其中一种属继

## 表面

3 D 物体的表面是21日敏、
纹理：一张有弹性、可拉伸的2口图
纹理映射。把2口图赚贴在的物体表面的的过程
假设映射关系是已知的
纹理坐标用 LU,0）表示， 范围[0，1]
映射关系只包含0顶点对应的(U、以
△ 内部点的 uh 通过插值得到

