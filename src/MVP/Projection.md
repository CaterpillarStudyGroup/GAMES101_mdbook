# Projection hangman 投影变换 [39.00]

- 投影： 3D --> 2D
  正交投影:（左），用于工程制图
  透视投影：（右），类似于人眼
  ![](../assets/两种投影.jpg)

- 数学上的区别。
  正交投影: 相机是近处的一个点
  正交投影: 相机位于无限远处

## 正交投影 [43：00]

![](../assets/正交投影.jpg)

### 投影的一种计算过程：

1. 把相机 view 变换为期望 view（转换到原点）
   object 需要乘以一个矩阵来做到
   [参考view transformation](View.md)

2. 把 object 的Z轴坐标去掉
   3D信息变成了2D信息。

3. 变换和缩放使得object范围为[-1， 1]
   业界惯例

### 用更专业的方法来描述
长方体：
- [l, r] 左右
- [b, t] 上下
- [f, n] 远近
将该长方体直接转换成\\([-1, 1]^3\\)这样的立方体

\\[
M_{ortho}=\left[ \begin{matrix}
	\frac{2}{r-l}&		0&		0&		0\\\\
	0&		\frac{2}{t-b}&		0&		0\\\\
	0&		0&		\frac{2}{n-f}&		0\\\\
	0&		0&		0&		1\\\\
\end{matrix} \right] \left[ \begin{matrix}
	1&		0&		0&		-\frac{r+l}{2}\\\\
	0&		1&		0&		-\frac{t+b}{2}\\\\
	0&		0&		1&		-\frac{n+f}{2}\\\\
	0&		0&		0&		1\\\\
\end{matrix} \right] 
\\]


## 透视投影 [53:10]

Hire 253之心
！人必
if 非洲
-1

① 把和𡃴澜成 aroid M
观察：从侧面看 squish
i­feng.nyfxyz.j­o 长点-1
y =是. yxif.t­n 齐次坐标
卧阔𠠬鬬劐
ā 5 E
i = Mā, 求 M
可得出，唯㱍
观察二：追平面上的点1区二时挤压后不变

即： 一
间= m.阅 20
㦖雦1
可得出： m = P 鰿剴且 Ant B =心
观察三远平面器等挤压后飞不变，取点100.1-1代入公式。
请|= M.管了 可得出 Aft 13=小
两式结合可解出。 A = htt. B: nf
因此' m =说是靠智\
② 用 P 17中的方法进行天文投影
环 Mma = M 正文 M 透视
思考题、 cwboid 蛐间呈䲄点理(most)，
被挤的殴大还是变小？

逃 逃键一吼飞 斗
ˊ zzi-zz.tt f T z-叶•
Z = In
-
z>器、 时， z'-E 20，变近
过以0）和 cnn.hr
开口向下的二滩线
开 EGG。四时420-
由于 ZCO.EE (f.nl 时， ZYzt­zh.EC 0
2-变大。即变近
