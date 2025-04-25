P16    
# Fog

P17    
## Depth Fog

> 随着距离降低透明度。   

Linear fog:   
factor = (end-z)/(end-start)   

Exp fog:   
factor = exp(- density\\(\ast \\)z)   

**Exp Squared fog:**    
factor = exp(- (density\\(\ast \\)z)^2)   

![](../assets/07-11.png)   

P18    
## Height Fog

- Height Fog integration along view diretion   

$$
\mathrm{D(h)=D _{max}\cdot e ^{-\sigma \cdot max(h-H _s,0)}}
$$
   
$$
\begin{align*}
 = & \mathrm {D_{\max}\cdot d\int_{0}^{1}e^{-\sigma \cdot \max (v_z+t\ast d_z-H_s,0)}dt} \\\\
  = & \mathrm {D_{\max}\cdot d\cdot e^{-\sigma \cdot \max(v_z-Hs,0)}\frac{1-e^{-\sigma \cdot d_z}}{\sigma \cdot d_z}}
\end{align*}
$$

- Fog color after transmission

FogInscatter=1\\(- \\)exp\\(^{-FogDensityIntegration}\\)    
FinalColor=FogColor\\(\cdot\\) FogInscatter    

![](../assets/07-12.png)   

> 十年前的常用方法。   

P19   
## Voxel-based Volumetric Fog

> 根据视锥构造非均匀体素。    
计算方法与上一节的体素云类似。    
可以构造出雾中的光柱效果。    

![](../assets/07-13-1.png)   



P20   
## Anti-aliasing

> 反走样。    

P21   
## Reason of Aliasing

- Aliasing is a series of rendering artifact which is caused by high-frequency signal vs. insufficient sampling of limited rendering resolutions   

![](../assets/07-14.png)   

> 走样的本质：渲染的采样频率与真实世界的频率不一致。    

P22    
## Anti-aliasing

- The general strategy of screen-based antialiasing schemes is using a sampling pattern to **get more samples** and then **weight and sum samples** to produce a pixel color    

$$
p(x,y)=\sum_{i=1}^{n}  w_ic(i,x,y)
$$

![](../assets/07-15-1.png)   

![](../assets/07-15-2.png)   

> 多采样再取平均，产生过渡区域。    

P23    
## Super-sample AA (SSAA) and Multi-sample AA (MSAA)

- Super sampling is the most straightforward solution to solve **AA**    

![](../assets/07-16-1.png)   

![](../assets/07-16-2.png)   

> 目前硬件部已支持 MSAA。    
但现在的高精模型可能比一个像素还小，这种方法就失效了。    

P24    
## FXAA (Fast Approximate Anti-aliasing)

Anti-aliasing based on 1x rendered image　  
- Find edge pixels by luminance　　　
- Compute offset for every edge pixel　　　
- Re-sample edge pixel by its offset to blend with a neighbor　　　

![](../assets/07-17-1.png)   

![](../assets/07-17-2.png)   

> 提取边界，并在边界做插值。   
优点：(1) 效果好    
(2) 速度快，利用 GPU 的并行计算，没有多余的计算。   
(3) 计算简单。   

P26   
## Edge Searching Algorithm

![](../assets/07-18-1.png)   

![](../assets/07-18-2.png)   

P27    
## Calculate Blend Coefficient

- Compute blender coefficient

**targetP** is the nearer edge end of **CurrentP**    

![](../assets/07-19-2.png)   

![](../assets/07-19-5.png)   

![](../assets/07-19-4.png)   

P28   
## Blend Nearby Pixels

- Compute blender coefficient   

![](../assets/07-20.png)   

**PixelNewColor = Texture(CurrentP_UV + offset_direction * offset_magnitude )**

P29   
## FXAA Result

![](../assets/07-21.png)   


P30   
## TAA (Temporal Anti-aliasing)

Utilize spatial-**temporal** filtering methods to improve AA stability **in motion**   

![](../assets/07-22-1.png)   

![](../assets/07-22-2.png)   

> 引擎中的主流方法。   

P31   
## TAA (Temporal Anti-aliasing)

![](../assets/07-23.png)   

P34   
## Post-process

Post-process in 3D Graphics refers to any algorithm that will be applied to the final image. It can be done for stylistic reasons (color correction, contrast, etc.) or for realistic reasons (tone mapping, depth of field, etc.)    

![](../assets/07-24.png)   

P35   
## Bloom Effect

P36   
## What is Bloom

- The physical basis of bloom is that, in the real world, lenses can never focus perfectly    
- Even a perfect lens will convolve the incoming image with an <u>**Airy disk**</U>    

![](../assets/07-25.png)   

P37   
## Detect Bright Area by Threshold

![](../assets/07-26.png)   

Find Luminance (Y) apply the standard coefficients for sRGB:    

$$
Y=R_{lin}\ast 0.2126+G_{lin}\ast 0.7152+B_{lin}\ast 0.0722
$$

> 取出非常亮的部分，做与 5\\(\times \\)5 高斯 blur。    

P38   
## Gaussian Blur   

![](../assets/07-27.png)   

P39    
## Pyramid Guassian Blur

![](../assets/07-28.png)   

We can't do all that filtering at high resolution, so we need a way to **downsample** and **upsample** the image Need a weight coefficient to tweak final effect   

> 在低精度图上 blur 再放大，可以得到大区域的 blur 效果同时较小的计算量。   

P40   
## Bloom Composite

![](../assets/07-29.png)   

P41   
![](../assets/07-30.png)   

P42   
## Tone Mapping

> 真实世界的亮度 range 非常大，如果曝光没调好，会出现亮部过亮或暗部过暗的效果。    

P43   
## Tone Mapping

- No way to directly display HDR image in a SDR device    
- The purpose of the **Tone Mapping** function is to map the wide range of high dynamic range (HDR) colors into standard dynamic range (SDR) that a display can output    

![](../assets/07-31.png)   

> 用一条曲线把 HDR 映射到 SDR。   
filmic curve 是一个拟合出来的所项式曲线。      

P45   
## ACES

- **A**cademy **C**olor **E**ncoding **S**ystem    
  - Primarily for Film & Animation    
  - Interesting paradigms and transformations   
- The useful bits   
  - Applying Color Grading in HDR is good   
  - The idea of a fixed pipeline up to the final OTD transforms stage is good   
     - Separates artistic intent from the mechanics of supporting different devices   

![](../assets/07-32-1.png)   

> ACES 曲线不但效果更好，还可以通注增加一个后处理，无差别适配到任何终端。    

P46    
## HDR and SDR Pipeline

- Visual consistency between HDR / SDR   
- Similar SDR results to previous SDR color pipeline   
- High quality   
- High performance   
- Minimal disruption to art teams   
  - Simple transition from current color pipeline   
  - Minimal additional overhead for mastering HDR *and* SDR   

![](../assets/07-33.png)   

P47    
## Tone Mapping Curve Comparison

![](../assets/07-34-1.png)   
![](../assets/07-34-2.png)   

P48   
## Color Grading

P49   
## Lookup Table (LUT)

- LUT is used to remap the input color values of source pixels to new output values based on data contained within the LUT    

- A LUT can be considered as a kind of color preset that can be applied to image or footage    

![](../assets/07-35.png) 

> 用一个表格实现从原始色相空间到目标色相空间的映射。    

P53    
## Rendering Pipeline

P59   
## Rendering Pipeline

- **Rendering pipeline** is the management order of all rendering operation execution and resource allocation    

![](../assets/07-36.png) 

P60   
## Forward Rendering

for n meshes   
\\(\quad\\) for m lights    
\\(\quad \quad\\)color += shading(mesh, light)    

P61    
## Sort and Render Transparent after Opaque Objects

![](../assets/07-37.png) 

> 透明物质必须最后绘制。    
多个透明物质则由远及近绘制，因为不同绘制顺序产生的结果是不一样的。   
透明物体的排序很容易引起各种 BuG。    
十几年前的主流 Pipeline。    

P64    
## Deferred Rendering

![](../assets/07-38-1.png)   

![](../assets/07-38-2.png) 

![](../assets/07-38-3.png) 

![](../assets/07-38-4.png) 

> 由于光的种类非常复杂，引入延迟渲染技术，即先绘制物体，再考虑与光的关系。   
近十年最主流的 Pipeline.    

P65    
## Deferred Rendering

**Pros**   
- Lighting is only computed for visible fragments     
- The data from the G-Buffer can be used for post- processing   

**Cons**   
- High memory and bandwidth cost     
- Not supporting transparent object     
- Not friendly to MSAA    

![](../assets/07-39.png)   

P66   
## Pilot Engine Deferred Rendering

![](../assets/07-40.png)   

P67    
## Tile-based Rendering

![](../assets/07-41-1.png)     

![](../assets/07-41-2.png)     

![](../assets/07-41-3.png)     

> 这个 pipeline 用于移动端。因为移动端最关心发热问题。    
DRAM 存储大、速度慢、功耗高。On-chip 中的 SRAM 则相反。    
因此，把整个 G-buffer 切成小的 tile 在 SRAM 计算，算好存成framebuffer。    

P68   
## Light Culling by Tiles

![](../assets/07-42.png)     

P69    
## Depth Range Optimization

- Get Min/Max depth per tile from Pre-z pass    
- Test depth bounds for each light   

![](../assets/07-43.png)     

> tile-based 是现代引擎的主流方案。    
tile 的额外好处是简化光的计算。    

P71    
## Forward+ (Tile-based Forward) Rendering

- Depth prepass (prevent overdraw / provide tile depth bounds)     
- Tiled light culling (output: light list per tile)   
- Shading per object (PS: Iterate through light list calculated in light culling)    

P72   
## Cluster-based Rendering

![](../assets/07-44.png)     

> 对 Z 空间也做切分。一个小块称为 cluster。    

P73    
## Visibility Buffer

![](../assets/07-45.png)     

> 几何信息 (V-Buffer) 和材质信息 (G-Buffer) 剥离开。   
因为现在的几何越来越复杂，甚至几何密度超过像素密度。    
这是现代引擎的发展方向。     

P74   
![](../assets/07-46.png)     

P75   
## Challenges

- Complex parallel work needs to synchronize with complex resource dependency    
- Large amount of transient resource whose lifetime is shorter than one frame    
- Complex resource state management     
- Exploit newly exposed GPU features without extensive user low level knowledge    

P76   
## Frame Graph

A Directed Acyclic Graph (DAG) of pass and resource dependency in a frame, not a real visual graph    

![](../assets/07-47.png)     

> Frame Graph 是未来重要的发展方向。    

P77    
## Render to Monitor

P78    
## Screen Tearing

![](../assets/07-48.png)     

P79    
## Screen Tearing

In most games your GPU frame rate will be highly volatile    
When new GPU frame updates in the middle of last screen frame, screen tearing occurrs       

![](../assets/07-49.png)     


P80    
## V-Sync Technology

Synchronizing buffer swaps with the Vertical refresh is called V-sync    
V-Sync can be used to prevent tearing but framerates are reduced, the mouse is lagging & stuttering ruins gameplay   

![](../assets/07-50.png)     

P81    
## Variable Refresh Rate

![](../assets/07-51.png)     

P82    
## Homework 2

- You are supposed to...    
  - Implement ColorGrading shader code   
  - Generate own style ColorGrading result    
  - Add a new post-process pass that you want (advanced)   
  - Write a report document that contains screenshots of
your results   

- Download at    
  - Course-site:    
<https://games104.boomingtech.com/sc/course-list>   
  - Github:   
<https://github.com/BoomingTech/Pilot/tree/games104/homework02-rendering>    

![](../assets/07-52.png)     


---------------------------------------

> 本文出自CaterpillarStudyGroup，转载请注明出处。  
> https://caterpillarstudygroup.github.io/GAMES101_mdbook/
