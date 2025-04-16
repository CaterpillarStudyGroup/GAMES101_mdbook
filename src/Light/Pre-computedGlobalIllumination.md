# Background

## Why Global Illumination is Important

![](../assets/69-28-3.png)   

> ambient 可以做间接光照效果，但会使整个场景统一变亮。看上去会有平面感。因此真实计算间接光照，而不是用一个简单的常数值。  

P26    
## Why Pre-computed Global Illumination    

> 假设场景中90%的东西是不动的，大量数据预计算，空间换时间。    

## 预计算GI的关键问题
  
> 预计算的GI，是对一个球面空间的采样。   

How to Represent Input Indirect Light
   
(1) GI的数据量非常大。     
用极少的数据表达一整张图像的大致样子    
(2) 如何让材质与GI做积分。   
频域上的一次卷积相当于对图像域上每个像素做加权平均    

&#x1F50E;[傅利叶变换](../Rasterization/TimeVsFrequency.md) 的作用

> 使用几个球谐基系数，可以把球面的光照信号大致表达出来。   
由于 GI 只需要表达低频，使用到 1 阶就足够了。   

P34   
#### Sampling Irradiance Probe Anywhere

> 在任何一个点取 Irradiance Probe 信息，展开为下图    

![](./assets/69-34-1.png)  

P35   
#### Compress Irradiance Probe to SH1

![](./assets/69-35.png)  

EA. (2018). Precomputed Global Illumination in Frostbite. Retrieved from https://www.ea.com/frostbite/news/precomputed-global-illumination-in-frostbite    

> 用 1 阶球谐基(对应 4 个系数)压缩后还原得到图 2。     
图 2 足以表达光的明暗，且数据非常连续。    
通一个简单的线性运算，就可以从图中查询出任意一个方     

P37   
### SH Lightmap: Precomputed GI

![](./assets/69-37-1.png)

#### Pipeline   

- Parameterized all scene into huge 2D lightmap atlas    
- Using offline lighting farm to calculate irradiance probes for all surface points   
- Compress those irradiance probes into SH coefficients    
- Store SH coefficients into 2D atlas lightmap textures   

P38   
#### Lightmap: UV Atlas

![](./assets/69-38.png)   

**Lightmap density**   
- Low-poly proxy geometry   
- Fewer UV charts/islands   
- Fewer lightmap texels are wasted    

P39   
#### Lightmap: Lighting

**Indirect lighting, final geometry**   
- Project lightmap from proxies to all LODs   
- Apply mesh details
- Add short-range, high￾frequency lighting detail by HBAO   

P40   
#### Lightmap: Lighting + Direct Lighting

**Direct + indirect lighting,final geometry**    
- Compute direct lighting dynamically    

P41   
#### Final Shading with Materials

**Final frame**    
- Combined with materials   

P42   
#### Lightmap 总结

- **Pros**   
  - Very efficient on runtime   
  - Bake a lot of fine details of GI on environment   
- **Cons**   
  - Long and expensive precomputation (lightmap farm)   
  - Only can handle **static scene and static light**   
  - Storage cost on package and GPU   

P43   
### Light Probe: Probes in Game Space

![](./assets/69-43.png)   

P45    
### Reflection Probe

![](./assets/69-45.png)   

> Reflection Probe 的特点：    
(1) 数量少    
(2) 精度高，因为高光对高频很敏感。    

P46   
### Light Probes + Reflection Probes

- **Pros**   
  - Very efficient on runtime   
  - Can be applied to both **static and dynamic objects**   
  - Handle both diffuse and specular shading      

- **Cons**   
  - A bunch of SH light probes need some precomputation   
  - Can not handle fine detail of GI. I.e, soft shadow on overlapped structures   
