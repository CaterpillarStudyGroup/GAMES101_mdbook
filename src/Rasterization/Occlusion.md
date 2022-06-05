# 背景

有多个物体，每个物体都有多个三角形，因此要处理摭挡问题。

# 画家算法

![](../assets/画家算法.jpg)

由远及近的在画布上添加新物体，新添加的物体将已有的物体覆盖

主要步骤：

1. 排序 O(nlogn)
2. 光栅化
   
局限性[09:26]：无法决定深度

# Z-Buffer 算法

名称：depth buffer， Z buffer，或深度缓存

> **&#x1F4CC;** 可以解决画家算法无法决定深度的局限性

## 预处理

[10:40]由于MVP之后，约定摄像机在坐标原点，物体在视角的z轴负方向，因此物体的z都是负的。为了便于计算，物体上每个点的Z坐标都取其绝对值（深度）。

因此：  

1. Z(depth) > 0
2. Z(depth) 小-->近， Z 大-->远
3. 深度是一个物体距离摄像机的Z轴距离的绝对值。

## 具体过程

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

----------------------------
> 本文出自CaterpillarStudyGroup，转载请注明出处。
>
> https://caterpillarstudygroup.github.io/GAMES101_mdbook/