# 向量

## 向量叉乘在图形学中的作用

1. 判定左和右

   > **&#x1F4CC;左右：** 目标向量逆时针旋转指向的区域，是目标向量的左侧，反之是右侧。

   <img src="../assets/左右.png" title="" alt="" width="290">
   
   如果\\( \vec{a}\times \vec{b} \\) 的结果是正值，即与 \\(Z\\) 轴方向相同，就表示 \\(\vec{b}\\) 在 \\(\vec{a}\\) 的左侧。
   
> &#x2753; 叉乘的结果是一个向量，向量没有正负属性，什么叫**结果是正的**？  
> 答：这里假设a和b都是xy平面上的向量，即  
$$
a^\top = (x_a, y_a, 0) \\\\
b^\top = (x_b, y_b, 0)
$$
\\(c = a \times b\\)，那么  
$$
c^\top = (0, 0, z_c)
$$
在这种情况下，\\(z_c > 0\\)认为结果是正的，b在a的左侧。  
离开了前面的假设，就不能用这种方法简单的判断了。  

2. 判断内和外
   
   <img src="../assets/内外.jpg" title="" alt="" width="290">
   
   > **&#x2705;如何判断P点在A、B、C的内部？**
   > 
   > \\( AB\times AP \\)，可以得到 \\(AP\\) 在 \\(AB\\) 的左侧。\\( BC\times BP \\)，可以得到 \\(BP\\) 在 \\(BC\\) 的左侧。\\( CA\times CP \\)，可以得到 \\(CP\\) 在 \\(CA\\) 的左侧。这样，就可以判断出P点在A、B、C的内部（P点在这三条边的**同一侧**）。

3. 构建右手坐标系
   
   有三个单位向量，两两垂直：
   
   \\(||\vec{u}||=||\vec{v}||=||\vec{w}||=1\\)
   
   \\(\vec{u}\cdot \vec{v}=\vec{v}\cdot \vec{w}=\vec{u}\cdot \vec{w}=0\\)
   
   且 \\(\vec{w}=\vec{u}\times \vec{v}\\)
   
   则这三个向量构成一个右手坐标系。
   
   可以把任意一个向量分解到轴上去：
   
   \\(\vec{p}=\left( \vec{p}\cdot \vec{u} \right) \vec{u}+\left( \vec{p}\cdot \vec{v} \right) \vec{v}+\left( \vec{p}\cdot \vec{w} \right) \vec{w}\\)
   
   - \\(\left( \vec{p}\cdot \vec{u} \right)\\) 是投影长度
   - \\(\vec{u}\\) 是方向

 
 

----------------

> 本文出自CaterpillarStudyGroup，转载请注明出处。  
> https://caterpillarstudygroup.github.io/GAMES101_mdbook/