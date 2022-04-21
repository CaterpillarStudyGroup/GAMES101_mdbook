# View Transformation

## 定义camera的view

- position：\\(\vec{e}\\)
- gaze direction：\\(\hat{g}\\)
- up direction：\\(\hat{t}\\)

> ![](../assets/tge.jpg) 
> 
> \\(\vec{e}\\) 是摄像机的位置；\\(\hat{g}\\) 是摄像机的方向（看哪个方向的画面）；\\(\hat{t}\\) 是固定摄像机的向上的方向。\\(\hat{g}\\) 和 \\(\hat{t}\\) 确定了view的视角。

> **&#x2753;疑问：** \\(\vec{t}\\) 和 \\(\hat{t}\\) 的区别？
> \\(\hat{t}\\) 是单位矢量。

## 期望的camera参数

- position：原点
- gaze direction：看向-Z轴
- up direction：Y轴

我们期望一个摄像机（view）能够有如上参数，这样方便计算，但是真实的camera view不会和我们期望的相同，所以我们需要对camera的上述三个向量做转换，使得view在原点上。

## view的变换

1. 平移 \\(\vec{e}\\) 
   
   \\[
   T_{view}=\left[ \begin{matrix}
    1&        0&        0&        -x_e\\\\
    0&        1&        0&        -y_e\\\\
    0&        0&        1&        -z_e\\\\
    0&        0&        0&        1\\\\
   \end{matrix} \right] 
   \\]

2. 旋转\\(\hat{g}\\)和\\(\hat{t}\\)
   将 \\(\hat{g}\\) 和 \\(\hat{t}\\) 旋转到-Z轴和Y轴，求出旋转矩阵 \\(R\\) 并不容易，但是由-Z轴和Y轴旋转到 \\(\hat{g}\\) 和 \\(\hat{t}\\) 就比较简单了，当我们得到 \\(R^{-1}\\) 后，如何进行逆运算，将 \\(R^{-1}\\) 转换为 \\(R\\) 呢？ 需要注意，约定的 \\(\hat{g}\\) 和 \\(\hat{t}\\) 是垂直的，那么就满足 \\(R^{-1}=R^{T}\\)，于是有 \\(R=(R^{-1})^{T}\\)。
   
   \\[
   R_{view}^{-1}=\left[ \begin{matrix}
    x_{\hat{g}\times \hat{t}}&        x_t&        x_{-g}&        0\\\\
    y_{\hat{g}\times \hat{t}}&        y_t&        y_{-g}&        0\\\\
    z_{\hat{g}\times \hat{t}}&        z_t&        z_{-g}&        0\\\\
    0&        0&        0&        1\\\\
   \end{matrix} \right] 
   \\]
   
   \\[
   R_{view}^{}=\left[ \begin{matrix}
    x_{\hat{g}\times \hat{t}}&        y_{\hat{g}\times \hat{t}}&        z_{\hat{g}\times \hat{t}}&        0\\\\
    x_t&        y_t&        y_{-g}&        0\\\\
    x_{-g}&        y_{-g}&        z_{-g}&        0\\\\
    0&        0&        0&        1\\\\
   \end{matrix} \right] 
   \\]

3. 如果object与camera做相对运动，那么即便view的坐标变换了，得到的视图也不会改变，也就是说，model也需要和view做相同的平移和旋转。
