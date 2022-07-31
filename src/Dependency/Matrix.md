# 矩阵

## 矩阵乘法

[45：00]

$$
A_{M\times N}B_{N\times P} = C_{M\times P}
$$

- \\(AB\ne BA\\) （不满足交换律）
- \\(\left( AB \right) C=A\left( BC \right) \\) （结合律）
- \\(\left( A+B \right) C=AC+BC\\)  （分配律）

矩阵与向量相乘时，可以把向量看作是\\(M \times 1\\)的矩阵

$$
a \cdot b = a^\top b \\\\
a \times b = A^* b
$$

## 矩阵转置

转置：行列互换，用\\(A^\top\\)表示

- \\(\left( AB \right) ^T=B^TA^T\\)

## 矩阵的逆

逆矩阵：用\\(A^{-1}\\)表示，方阵才有逆矩阵
I：单位矩阵，对角线上全1、其余元素全0的矩阵

- \\(AA^{-1}=A^{-1}A=I\\)
- \\(\left( AB \right) ^{-1}=B^{-1}A^{-1}\\)

## 变换合成与分解

- 复杂变换可以通过简单变换一步一步达到
- 变换顺序非常重要，ABC不等于ACB（矩阵乘法性质）

变换合成：

<div align="left"><img src="../assets/结合律.jpg" width = 400 /></div>

变换分解：

<div align="left"><img src="../assets/分解.jpg" width = 500 /></div>

以C点为中心的旋转，可以分解为：

1. 从C点平移到原点
2. 旋转
3. 再从原点平移到C点

即：\\(X'=MX=T\left( c \right) \cdot R\left( \alpha \right) \cdot T\left( -c \right) \cdot X\\)

再次来看矩阵旋转 \\(X'=R_{\theta}X\\) :

我们将 \\(X\\) 旋转 \\(\theta\\) 度， \\(R_{\theta}\\) 为：

\\[
R_{\theta}=\left( \begin{matrix}
    \cos \theta&        -\sin \theta\\\\
    \sin \theta&        \cos \theta\\\\
\end{matrix} \right) 
\\]

如果要逆转回来，恢复原来的矩阵，需要旋转 \\(-\theta\\) 度，根据上述旋转的推导，可以得到：

\\[
R_{-\theta}=\left( \begin{matrix}
    \cos \theta&        \sin \theta\\\\
    -\sin \theta&        \cos \theta\\\\
\end{matrix} \right) 
\\]

而 \\(R_{-\theta}\\) 恰好是 \\(R_{\theta}\\) 的转置矩阵 \\(R_{\theta}^{T}\\)， 即：

\\[
R_{-\theta}=R_{\theta}^{T}
\\]

由 “当一个变换是通过\\(M\\)得到的，那么可以通过\\(M\\)的逆\\(M^{-1}\\)来恢复变换” 可知，\\(R_{\theta}^{-1}\\) 与刚刚旋转 \\(-\theta\\) 推导得到的 \\(R_{\theta}\\) 相等，即：

\\[
R_{\theta}^{-1}=R_{-\theta}
\\]

于是有：

\\[
R_{-\theta}=R_{\theta}^{-1}=R_{\theta}^{T}
\\]

# 3D变换(3D Transformation)

如果用齐次坐标来表示三维的点或向量，和二维的情况相似：

- 3D point = \\((x, y, z, 1)^{T}\\)
- 3D vector = \\((x, y, z, 0)^{T}\\)

则一个齐次坐标 \\((x, y, z, w)^{T}\\) \\((w\ne 0)\\) 表示的点为  \\(\left( \frac{x}{w},  \frac{y}{w},  \frac{z}{w} \right)\\)

## 缩放(Scale)

\\[
S\left( s_x, s_y, s_z \right) =\left( \begin{matrix}
    s_x&        0&        0&        0\\\\
    0&        s_y&        0&        0\\\\
    0&        0&        s_z&        0\\\\
    0&        0&        0&        1\\\\
\end{matrix} \right) 
\\]

## 平移(Translation)

\\[
T\left( t_x, t_y, t_z \right) =\left( \begin{matrix}
    1&        0&        0&        t_x\\\\
    0&        1&        0&        t_y\\\\
    0&        0&        1&        t_z\\\\
    0&        0&        0&        1\\\\
\end{matrix} \right) 
\\]

## 旋转(Rotation)

### 自然旋转

> **&#x1F4CC;自然旋转：** 绕着某一个轴旋转。

> **&#x1F4A1;思考：** 当绕着x轴旋转时，矩阵在x轴上的坐标值是不变的，因此在变换矩阵中，与X相乘的部分，是 \\((1 ,0 , 0)\\)，绕y、z轴同理。

绕x轴旋转：

\\[
R_x\left( \alpha \right) =\left( \begin{matrix}
    1&        0&        0&        0\\\\
    0&        \cos \alpha&        -\sin \alpha&        0\\\\
    0&        \sin \alpha&        \cos \alpha&        0\\\\
    0&        0&        0&        1\\\\
\end{matrix} \right) 
\\]

绕y轴旋转：

\\[
R_y\left( \alpha \right) =\left( \begin{matrix}
    \cos \alpha&        0&        \sin \alpha&        0\\\\
    0&        1&        0&        0\\\\
    -\sin \alpha&        0&        \cos \alpha&        0\\\\
    0&        0&        0&        1\\\\
\end{matrix} \right) 
\\]

> **&#x1F4A1;思考：** 上式的变换矩阵，与x、z不同，是 \\(R_{-\theta}\\) 而不是 \\(R_{\theta}\\)，这是为什么呢？
> 
> 因为绕y旋转，如果使用 \\(R_\theta\\)，那么可以认为在计算过程中x和z坐标在变化，有 \\(\left( \begin{array}{c}
>     X'\\\\
>     Z'\\\\
> \end{array} \right) =R_{\theta}\cdot \left( \begin{array}{c}
>     X\\\\
>     Z\\\\
> \end{array} \right) =\left( \begin{matrix}
>     \cos \theta&        -\sin \theta\\\\
>     \sin \theta&        \cos \theta\\\\
> \end{matrix} \right) \left( \begin{array}{c}
>     X\\\\
>     Z\\\\
> \end{array} \right) \\) , 但是， \\(\vec{x}\times \vec{z}=-\vec{y}\\)，也就是说，使用 \\(R_\theta\\) 会导致绕y旋转是顺时针旋转，而我们约定了，旋转默认是逆时针旋转，所以需要用 \\(R_{-\theta}=\left( \begin{matrix}
>     \cos \theta&        \sin \theta\\\\
>     -\sin \theta&        \cos \theta\\\\
> \end{matrix} \right) \\)

绕z轴旋转：

\\[
R_z\left( \alpha \right) =\left( \begin{matrix}
    \cos \alpha&        -\sin \alpha&        0&        0\\\\
    \sin \alpha&        \cos \alpha&        0&        0\\\\
    0&        0&        1&        0\\\\
    0&        0&        0&        1\\\\
\end{matrix} \right) 
\\]

### 一般旋转

任意一个3D旋转，可以写成：

\\[
R_{xyz}\left( \alpha , \beta , \gamma \right) =R_x\left( \alpha \right) R_y\left( \beta \right) R_z\left( \gamma \right) 
\\]

也就是说，一般旋转可以由绕x、y、z轴的自然旋转组合而成。

在图形学中，任意旋转用矩阵表达为（Rodrigues' Rotation Formula）：

\\[
R\left( \mathbf{n},\alpha \right) =\cos \left( \alpha \right) \mathbf{I}+\left( 1-\cos \left( \alpha \right) \right) \mathbf{nn}^{\mathrm{T}}+\sin \left( \mathrm{\alpha} \right) \underset{\mathrm{N}}{\underbrace{\left( \begin{matrix}
    0&        -n_z&        n_y\\\\
    n_z&        0&        -n_x\\\\
    -n_y&        n_x&        0\\\\
\end{matrix} \right) }}
\\]

> 公式推导：(暂无)

为解决旋转插值问题，参考四元数[link](暂无)。

> **&#x1F4A1;我的思考：** 
> 
> 1.复杂问题都可以分解为互相独立的简单问题，但需要保证分解出的子问题是独立的。简单操作也可以组合成复杂操作，但需要保证组合的效果是预期的，而不会引入奇怪的问题。
> 
> 前面两处使用了这种思路
> 
> （1）简单线性变换 复杂仿射变换
> 
> （2）基于不同轴的简单旋转 VS 基于特定方向的旋转
> 
>         但这两个问题的子问题都没有完全独立，因此都存在子问题的顺序要求。
> 
> 2.当学到一个新的概念/方法时，可以想一想，为什么要引入这个概念/方法？
> 
> 是为了了解什么问题？
> 
> 以前是用什么方法来解决的？它有什么问题？
> 
> 这个方法是否解决了以前方法的问题？这个方法有什么局限性？
> 
> 两者能否结合？
> 
> 两者如何取舍？






-----------

> 本文出自CaterpillarStudyGroup，转载请注明出处。
>
> https://caterpillarstudygroup.github.io/GAMES101_mdbook/