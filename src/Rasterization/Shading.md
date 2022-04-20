Lecture 7
Shading 着色 31

# 可见性/蓬挡

讟
有多个物理体，每个物体都有多个4，因此要处理摭挡
问题。
原是画䟑滚
back-> front,覆盖
ⓛ 排序 Olnhgn)
ⓩ 光栅化
局限性、 [09：26了无法决定深度
Z-Buffer 算法[心403
为了便于计算， object 上每个点的䂳标都取其绝对焦
因此： 0 Z 20
② Z 小→近， E 大→远
每次生成2张图[14：38]
o frame buffer:存最终结果
② depth but。有某个俼谋点事对应的在0时上的最小
的2（最近）
ˊ 具体步骤
ⓥ depth buffer 初始化为0

② 每次绘制△时，计算当前12以比在△上的飞。
苦 Z <buffer Gaels,
制，绘制，并更新 butter 32
算法特点
0 0 M)
② 与△的绘制顺序无关
③ 可以与 MSAA 算法兼容
④ 适合 GPU 优化（因为20） .
# Shading 着色
[32：31]不考虑着色的效果 .
[32：55了期望达到的效果
纯色立方体的每个面每个时刻呈现的颜色有变化。使
整体效果更真实、
课程中的 shading:
The process of applying a material to an object.
对一个物体应用一个材质的过程，不包含给0分比溢䙍足影的过年是.

## Bling-Phong 反射模型

高光.。光线反射到镜面反射附近
漫反射=光线被反射到各个方向上，
环境光：主政伇任何一个点会接议到来自环境的常­量的光
Speeder high, Dye Reflection, Ambient Lighting


