纹理，原义为贴图。广义上，纹理=内存 + 范围查询（滤图）。通过这样的技术，可以得到很多实用的功能。

# 用纹理记录环境光照

以一个点出发，向其四周都能看到光，把这些光记录下来，就是环境光照。用纹理来描述环境光照，并环境光照渲染其他物体。

例如：这是某个点的环境光照

<img src="../assets/environment1.jpg" width = 400 />

用这个环境光照来渲染茶壶，就得到了这样的效果

<img src="../assets/environment2.jpg" width = 400 />

用纹理记录环境光照时，对光做了一些假设和简化：  
   
- 假设环境光的光源无限远，只记录某个方向上的光的信息（强度、颜色等），不记录光源的深度。
- 在记录光照信息时，不区分光照的种类。

## [12:35] Spherical 环境图：

如果对一个点的周围均匀采样，得到的是一个球。因此，记录环境光照的纹理图是一个球面的图（左）。

<img src="../assets/environment3.jpg" width = 600 />

但把球面的环境光照纹理图展开，会出现扭曲：

<img src="../assets/environment4.jpg" width = 600 />

## Cube Map 

球表面点和立方体表面点可以一一对应。只要计算出这种对应关系，就能球面上的光照信息存储到立方体表面。

![](../assets/cubemap.jpg)

Cube Map展开后不会扭曲

![](../assets/cubemap2.jpg)

# 凹凸贴图 - 用复杂纹理代替复杂几何

用纹理定义某个点的相对高度，在object triangle mesh不变的条件下，得到视觉上的表面凹凸效果，即：用复杂纹理代替复杂几何

原理：高度-->法线-->着色或法线-->着色

## 法线贴图 - 用纹理记录顶点的法线

Bump Mapping效果：

<img src="../assets/bump1.jpg" width = 600 />

以2D为例：

1. 在p点定义局部坐标系，令原始方向向上，为(0,1)或(0,0,1)
2. 想要让p表现出在p'处的效果，需要计算出在局部坐标系下，p'处的切线方向和法线方向
<img src="../assets/bump.jpg" width = 600 />
3. 根据dp（通过纹理记录的值），直接使用以下公式就可以计算出p'处的切线方向和法线方向
<img src="../assets/bump2.jpg" width = 600 />

||2D|3D|
|---|---|---|
|p的法线方向|(0,1)|(0,0,1)|
|p'的切线方向 |(1,dp)|(1, dp/du, dp/dv)|
|p'的法线方向 |(-dp, 1)| (-dp/du, -dp/dv, 1)|


4. 在此局部坐标系中求切线方向和法线方向，求出后再切回实际坐标系。

5. 根据新的切线

凹凸贴图的局限性：

![](../assets/displacement.jpg)

1. 边缘处会露馅
2. 缺少“自己阴影投影到自己身上”

## 位移贴图 - 用纹理记录顶点的高度偏移

输入：原始mesh，高度贴图

输出：mesh的顶点被改变

代价：要求原始mesh的三角形足够细

改进：动态三角形细分

# 3D纹理

<img src="../assets/displacement2.jpg" width = 600 />

纹理不只有表面，内部也有值，即空间任意一点都有值。

纹理并非实际定义，而是通过noise生成（[35:01]右）

## 3D纹理用于体积渲染

用于记录3D空间信息

# 用纹理记录之前算好的信息

[35:35]

好处：很多计算可以提前算好


------------------------------

> 本文出自CaterpillarStudyGroup，转载请注明出处。
>
> https://caterpillarstudygroup.github.io/GAMES101_mdbook/