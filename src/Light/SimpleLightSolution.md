# Simple Light Solution

假设简单场景，只有一个主光源    

## 直接光照

由于直接一个光源，可以直接计算直接光照。  
可以直接入射光方向与物体表面法向方向决定是否表现是高光效果。

## 间接光照   

自定义一个常数环境光    

![](./assets/69-12-1.png)     

P13     
## 光在材质上的效果

### Environment Map Reflection

> 增加物体反射光线的效果。   

![](./assets/69-13-1.png)     

**Early stage exploration of image- based lighting**      

方法：六面体环境贴图 cudemap    

## 总结

> 本质上，把一个半球形的光场模拟为均匀的环境光。环境光中高频内容用 envirnment map 表达。 


P15   
## Blinn-Phong Materials

![](./assets/69-15-1.png)   

$$
\begin{align*}
 L_0 &=\int f_{BRDF}\cdot L_idw  \\\\
  & =\int f_{BRDF}\cdot (L_a+L_d+L_s)dw  \\\\
  &=\int (f_{BRDF}\cdot L_a)dw+\int (f_{BRDF}\cdot L_d)dw+\cdots   \\\\
  &=k_a+k_d+k_s+\cdots  
\end{align*}
$$

> 光可叠加原理。    

P16   
### Problem of Blinn-Phong

- Not energy conservative Unstable in ray-tracing   

![](./assets/69-16-1.png)   

- Hard to model complex realistic material    

![](./assets/69-16-2.png)   

P17    
## Shadow    

- Shadow is nothing but space when the light is blocked by an opaque object   
- Already obsolete method   
  - planar shadow   
  - shadow volume   
  - projective texture   

![](./assets/69-17.png)   

P18    
> 从光的视角渲染一张场景深度图。   
判断真实视角下的每一个点在光视角下是否可见。若不可见，则为阴影。   

P19    
### Problem of Shadow Map

![](./assets/69-19.png)   

> 深度图的采样频率和渲染的采样频率一致，会引发 artifacts.    

P20    
## Basic Shading Solution

- Simple light + Ambient   
  - dominent light solves No.1b   
  - ambient and EnvMap solves No.3 challanges   
- Blinn-Phong material       
  - solve No.2 challange   
- Shadow map   
  - solve No.1a challange   

P21    
Cheap, Robust and Easy Modification

