# Non-Heightfield Terrain

> 处理有山洞的地形    
方法1：在普通地形上放一个山洞或桥。   

P31   
## Dig a Hole in Terrain

![](./assets/06-12.png)   

> 方法 2：   
通过将顶点设为无效值的方式把洞口的面片删掉，再放一个隧道的模型上去。 

P32   
## Crazy Idea - Volumetric Representation

In 3D computer graphics, a voxel represents a value on a regular grid in three-dimensional space. As pixels in a 2D     
bitmap, voxels themselves do not typically have their position (i.e. coordinates) explicitly encoded with their values     

> 用体素来表达世界，并用一个值来描述每个体素上是否有物质以及物质的密度。    
再有 Marching Cube 将其转为 Mesh。    
实操时，考虑到水密性、LOD 等因素，会稍微复杂一点。     

P33   
## Marching Cubes

![](./assets/06-13.png)   

MARCHING CUBES: A HIGH RESOLUTION 3D SURFACE CONSTRUCTION ALGORITHM'; Computer Graphics, Volume 21, Number 4, July 1987    

P36    
Paint Terrain Materials

P38    
## Terrain Materials

![](./assets/06-14.png)   

> Splat Map：每一个 channel 定义了一种材质的权重。又称为材质混合。    

P39    
## Simple Texture Splatting

![](./assets/06-15-1.png)   

![](./assets/06-15-2.png)   

> 实际上材质过渡不是这种柔和渐变的过渡。

P40    
## Advanced Texture Splatting

![](./assets/06-16-1.png)   

Blending with Height    

float3 blend(float4 texture1, float height1, float4 texture2, float height2)    
{    
return height1 > height2 ? texture1.rgb : texture2.rgb;    
}       

![](./assets/06-16-2.png)   

> 解决方法：利用 height 调整权重   

P41    
## Advanced Texture Splatting - Biased

![](./assets/06-17-1.png)   

![](./assets/06-17-3.png)   

![](./assets/06-17-2.png)   

**Links:**     
<https://www.gamedeveloper.com/programming/advanced-terrain-texture-splatting>    

> 存在的问题，相机移到时有抖动现象     
解决方法：引入 height bias    

P42   
## Sampling from Material Texture Array

![](./assets/06-18.png)   

> 实践中会用到很多帧图，通常把它们 patch 成 Texture Array。   

P43   
## Parallax and Displacement Mapping

![](./assets/06-19-1.png)   

![](./assets/06-19-2.png)   

Parallax Mapping: Due to the height of the surface, the eye sees point B instead of point A. It creates a sense of dimensionality     

> 视差贴图。    

> 凹凸帧图能产生明暗分明的效果。但仍然会有平面感，因为眼睛看到的点和应该看到的点，有视差。常用做法，ray marching(Parallax mapping)        
缺点：(1) 几步测一下，比较贵     
(2) 只是产生视觉上的凹凸感，边界上还能看出 artifacts (光滑)    
Displacement mapping 真实修改地形     

P44    
## Expensive Material Blending    

- **Many Texturing** - Low performance when multiple materials are sampled too many times    

- **Huge Splat Map** - We only see a small set of terrain, but we load splat maps for 100 square km into video memory      

![](./assets/06-20.png)   

> 整个场景包含很多纹理，Texture Array 涉及内存的来回寻址，效率比较低。但实际上一个像素会用到的纹理种类很少。

P45    
## Virtual Texture

- Build a virtual indexed texture to represent all blended terrain materials for whole scene    
- Only load materials data of tiles based on view- depend LOD   
- Pre-bake materials blending into tile and store them into physical textures   

![](./assets/06-21.png)   

> 思想，只把用到的纹理加到内存、其它的纹理放在硬盘中。类似于mipmap＋oS 分页机制。    
优点：(1) 极大地减少了显存的占用    
(2) 像素的 blending，在 tile 被加载到内存时算好，就不动    
(3) 直到这个 tile 被置换出内存。    
这个是目前的主流方法。     

P46    
## VT Implementation, DirectStorage & DMA

![](./assets/06-22-1.png)   

![](./assets/06-22-2.png)   

![](./assets/06-22-3.png)   

> 这个方法涉及 GPU、内存、硬盘之间切换。    
新显卡的方式：硬盘数据只是从内存过一下，到 GPU 才解压，提升传输效率。   
DMA：硬盘直接往 GPU 写数据。   

P47    
## Floating-point Precision Error

> 浮点数的精度溢出    
float 存储数据时，数值越大精度越低。精度太低就会引起抖动。    
地图太大时，这种情况很常见。   

P48    
## Camera-Relative Rendering

- Translates objects by the negated world space camera position before any other geometric transformations affect them    
- It then sets the world space camera position to 0 and modifies all relevant matrices accordingly    

> 解决方法：坐标系调整到相机中心(很多引擎的标准做法)
仿真时也会有同样的问题。    

P49    
Integration with other world elements (rocks, trees, grass)    

P50    
## Tree Rendering

P51    
## Decorator Rendering

P52    
## Road and Decals Rendering

P54   
## Procedure Terrain Creation

P55    
## Sky and Atmosphere

P59    
## How to "Paint" Everything in the Sky

![](./assets/06-23.png)   

> 天空是一个球，云是可见的实体。背后是完全不同的表达方法，不可混为一谈。   

P60   
## Atmosphere

P61    
## Analytic Atmosphere Appearance Modeling

$$
\mathbb{F} (\theta ,\gamma )=(1+Ae^{\frac{B}{\cos \theta +0.01}})\cdot (C+De^{E\gamma }+F\cos ^2\gamma +G\cdot \chi (H,\gamma )+I\cdot \cos ^ {\frac{1}{2} }\theta )  
$$

$$
L_\lambda =\mathbb{F} (\theta ,\gamma )\cdot L_{M\lambda} 
$$

![](./assets/06-24-1.png)   

**Pros**    
- Calculation is simple and efficient    

**Cons**   
- Limited to ground view   
- Atmosphere parameters can’t be changed freely    

![](./assets/06-24-2.png)   

![](./assets/06-24-3.png)   

An Analytic Model for Full Spectral Sky-dome Radiance, ACM Trans 2012    

> 这是一种类似 Bling Phong 的经验模型。    

P62   
## Participating Media

- Volume filled with particles    
- Interact differently with light depending on its composition   

> 大气层有两种粒子构成(1) 各种气体分子 (2) 气溶胶   
这些是光的介质，是产生各种光学现象的原因。    

P63    
## How Light Interacts with Participating Media Particles?

![](./assets/06-25-1.png)   

![](./assets/06-25-2.png)   

> (1) 吸收 (2) 散射 (3) 自发光    

P64    
## Volume Rendering Equation (VRE)

![](./assets/06-26-1.png)  

![](./assets/06-26-2.png)  

> (1) 通透度 (2) 有多能量向视线方向辐射    

P65    
## Real Physics in Atmosphere

P66   
## Scattering Types

- **Rayleigh Scattering**   
Scattering of light by particles that have a diameter **much smaller than** the wavelength of the radiation (eg. air molecules)     

- **Mie scattering**   
Scattering of light by particles that have a diameter **similar to or larger than** the wavelength of the incident light (eg. aerosols)    

![](./assets/06-27.png)  

> 气体分子直径远小于光的波长，气溶胶的直径与光的波长相似，因此表现出完全不同的视觉效果，也对应两种不同的模型。    
(1) Rayleigh，用于气体分子。特点：    
——　均匀散射    
——　波长越短(紫)，散射越多    
(2) Mie，用于气溶胶。特点：    
——　有方向性，沿着光的方向会强一点   
——　对波长不敏感。      

P67    
## Rayleigh Scattering

- Certain directions receive more light than others front-back symmetry    
- Shorter wavelengths (eg. blue) are scattered more strongly than longer wavelengths (eg. red)    

![](./assets/06-28.png)  

**Rayleigh Scattering Distribution**

P68    
## Rayleigh Scattering Equation

![](./assets/06-29.png)  

> \\(\lambda\\)：波长。\\(\theta\\)：夹用。\\(h\\)：海拔高度。    

P69   
## Why Sky is Blue

![](./assets/06-30.png)  

P70   
## Mie Scattering

- Scatter light of all wavelength nearly equally
- Exhibit a strong forward directivity

![](./assets/06-31.png)  

P71   
## Mie Scattering Equation

![](./assets/06-32-1.png)  

- g > 0, scatters more forward Mie scattering    
- g < 0, scatters more backward   
- g = 0, Rayleigh scattering   

![](./assets/06-32-2.png)  

P72    
## Mie Scattering in Daily Life

- Exhibit a strong forward directivity (halo effects around sun)    
- Scatter light of all wavelength nearly equally (fog effects)    

![](./assets/06-33-1.png)  

![](./assets/06-33-2.png)  

P73   
> \\(O_3\\) 和 \\(CH_4\\) 吸收短波，使物体表现出蓝色。    
假设空气中 \\(O_3\\) 和 \\(CH_4\\) 是均匀分布的。   

P74   
## Single Scattering vs. Multi Scattering

![](./assets/06-34.png)  

P75   
## Single Scattering vs. Multi Scattering   

![](./assets/06-35.png)  

> Multi Scattering 现象与 GI 不同。因为空气中的粒子充满整个空间，所以 MS 的效果是连续的。    

P76    
## Ray Marching

- **Ray marching** is a popular method to integrate function along a path   
- We use ray marching to calculate final radiance for a given point by single scattering   
- The integrated radiance is usually stored in **look-up tables (LUT)**   

![](./assets/06-36.png)  

P77   
## Precomputed Atmospheric Scattering

![](./assets/06-37.png)  

<https://ebruneton.github.io/precomputed_atmospheric_scattering/>  

> 空间采样、预计算、查表。     

P78   
## Precomputed Atmospheric Scattering

![](./assets/06-38.png)  

> 人的视角 (2D)＋阳光角度 (2D) ＝4D    
如何参数化地表达 4D 数据    

P79   
## Precomputed Atmospheric Scattering

**Multi Scattering LUT**

![](./assets/06-39.png)  

> 一般 N 取 3-4 够用了。预计算部算好，实时部分变得简单高效
非常经典的方法。    
大气环境不变前提下，人和太阳可以在任意位置，都能有比较好的效果。    

P81    
## Challenges of Precomputed Atmospheric Scattering

- Precomputation Cost    
  - Multi-scattering iterations are very expensive   
  - Hard to generate atmosphere LUT on low-end devices (ie. mobile)   
- Authoring and **Dynamic Adjustment of** Environments   
  - Artist can't change scattering coefficients on the fly   
  - Hard to render effects like weather from sunny to rain fog, space travel among planets   
- Runtime Rendering Cost   
  - Expensive **per-pixel multi high dimensional texture sampling** for transmittance LUT and multi scattering LUT (always need to down-sample for efficiency)   

**A Scalable and Production Ready Sky and Atmosphere Rendering Technique**     
<https://diglib.eg.org/bitstream/handle/10.1111/cgf14050/v39i4pp013-022.pdf>    

P82   
## Production Friendly Quick Sky and Atmosphere Rendering

Simplify Multi-scattering Assumption   
- Scattering events with order greater or equal to 2 are executed using an **isotropic phase function**   
- All points within the neighborhood of the position we currently shade **receive the same amount of second order scattered light**   
- **Visibility is ignored**     

$$
G_{n+1}=G_n\ast f _{ms}
$$

$$
\mathbf{ F_{ms}=1+f_{ms}+f^2_{ms}+f^3_{ms}+\dots = \frac{1}{1-\mathbf{f_{ms}} } }
$$

$$
\mathbf{\Psi _ {ms} }=\mathbf{L_ {2^{nd}order} F_ {ms} }
$$

> 假设“散射是各向同性的”。那么，“均匀的入射光到均匀的出射光”的过程，只是一个简单的能衰减过程。所以只需要求出衰减比例，每 bounce 一次就按这个比例衰减就可以了。    

P83   
## Production Friendly Quick Sky and Atmosphere Rendering

Fixed view position and sun position to remove 2 dimensions out of LUT   

![](./assets/06-40.png)  

> 对上文中的 LUT 的简化：    
(1) 假设人所在的高度不变，去掉 height 维    
(2) 假设太阳位置不变，去掉入射角的维度仅留下出射光的维度(天顶角、环角)     

P84    
## Production Friendly Quick Sky and Atmosphere Rendering

- Generated a 3D LUT to evaluate aerial-perspective effects by ray marching    

![](./assets/06-41.png)  

> 这个方法不保证物理正确，但好处是：    
(1) 艺术家友好      
(2) 可以创造异星世界效果     
(3) 硬件友好     

P85    
## Good Balance of Performance and Effect

- Scalable from mobile to high-end PCs

![](./assets/06-42.png)  

Performance for each step of method, as measured on PC (NV 1080) and a mobile device (iPhone 6s)    

P87   
## "Paint" Cloud

P88    
## Cloud Type

![](./assets/06-43.png)  

P89   
## Mesh-Based Cloud Modeling

![](./assets/06-44.png)  

**Pros**   
- High quality   

**Cons**   
- Overall expensive   
- Do not support dynamic weather   

> Mesh＋腐蚀等算法。    
现在已经没人用了。      

P90   
## Billboard Cloud

**Pros**   
- Efficient   

**Cons**   
- Limited visual effect   
- Limited cloud type    

![](./assets/06-45.png)  

> 半透明插片＋\\(\alpha \\) 混合    
十年前常用     

P91    
## Volumetric Cloud Modeling

![](./assets/06-46.png)  

**Pros**    
- Realistic cloud shapes    
- Large scale clouds possible    
- Dynamic weather supported    
- Dynamic volumetric lighting and shadowing   

**Cons**   
- Efficiency must be considered    

> 优点：(1) 全动态，CPU 实时生成。(2) 云可以表现出很多变化    
局限性：(1) 复杂 (2) expensive    

P92    
## Weather Texture

![](./assets/06-47-1.png)  

![](./assets/06-47-2.png)  

>  texture＋厚度 channel    
对 texture 做挠动可以产生云的变化。     

P93   
## Noise Functions

![](./assets/06-48-1.png)  

![](./assets/06-48-2.png)  

P94    
## Cloud Density Model

![](./assets/06-49.png)  

>  用低频 noise 雕刻出造型，再用高频加上细节。    

P95    
## Rendering Cloud by Ray Marching

![](./assets/06-50.png)  

> 不会把云转成 Mesh 去渲染，而是当作大气来渲染。     
但由于云的通透性很低，可以对公式作大量假设和简化。     