
# 高级光线传播

## 无偏 unbiased Vs 有偏 biased

Path tracing 中使用 Monte Carlo 计算估计值。
E（估计值） = 真实值，称为无偏估计，否则为有偏估计。少量样本时有偏而极限情况下无偏，则称为consistence.

## 双向路经追踪 BDPT
方法[07：55]：  
1. 从眼睛（即摄像机）打出一条半路经
2. 从光源打出一条半路经
3. 把两条路往连起来，

缺点：  
实现非效复杂、速度非常慢

效果：[08:13]  
由于光源向上，场景大部分光来自间接光。因此大多数精情况下 path tracing 的第1个 bounce 是 diffuse，导致不好控制它打到能量集中的区域去

## Metropolis(人名) Light Transport (MLT)

原理：用"马尔可夫链"采样。  
方法：根据当前样本，生成与它靠近的下一个样本。
Monto Carlo 性质：当f(x)与 p(x) 形状一致时， bias 最小，
马尔可夫链性质：可以使得采样样本符合特定的 p(x)[14：19]
效果：  
[14：17] 适用于复杂困难的光路传播。  
缺点:  
难以估计算法的收敛速度。  
每个像素的收敛情况都不一样，多帧画面效果为抖动。  

## 光子映射

适用于渲染 caustics.[20：48]
是有偏算法
caustics： 由于光线聚集形成非常强的图案。
适于用 specular-diffuse-specular­

## Photon Mapping 方法

- Stage 1
光源向外辐射光子，光子 bounce 直到遇到diffuse表面

- Stage 2
从 camera 出发，打出 sub path, bounce,直到遇­到 diffuse 表面

- Stage 3,
计算 local density estimation，光子越集中的地方应该越亮  
对于任意一个着色点，取最近N个光子，计算 N 个光子所占的面积 A，可算出光子密度为­N/A。  
N 太小会有噪声，N太大会糊
由于光子密度是通过 N/A 估计出来的，因此该算法是有偏算法、
当 Stage 1中的光子数趋于\\(\inf\\)时， Stage 3的A趋于0，密度估计趋于正确值。因此该算法是bias but consistent 算法。

## VCM: Vertex Connection and Merging 双向路经追踪 + 光子映射

原理：[31:15]
1. 将光子停留位置（红）与 ray 停留位置（绿）连成一条 ray path.
2. 如果红点和绿点非常接近，就把它们合并
[?] 怎么理解合并这个概念。

## IR: Instant Radiosity

原理：已被照亮的这些地方，也被认为是光源
具体做法：  
1. 从光源打出很多sub Path，最终停在某些地方
2. 停住的地方会成为新的光源
3. 从当 camera 看某个着色点时，用新的光源照这­个着色点
优点：速度快  
缺点：  
1. 有一些地方莫名其妙地发光[34:51]
2. 不能处理 glossy 物体


tt 高级 Appreǎue 建模 80
##非表面模型巨8：38了
反射介质，例如.雾.云
特点 （散射），
光线打到一个介质颗粒上，会被分散至每到各个方向上（图3）
也会接受到来自其它方向的射而来的光（图4）
怎么靗射？ 越
ⓘ diffuse 表面：均匀靗射到各个方向
② 介质颗粒：散射由 phase function 来定义
怎么生成 path? [420门
l. 根据 phase function 决定 bounce 方向
2.根据介质对光线吸收难度决定 distance
3. 形成 my path
士1#Hair 表面
[45-45
无色高光，有色高光
##ttkajiya-Kay 模型
把头发看成是圆柱
会把光线产生圆雉形键射
和各个方向的散射
就又果[生7：05了

###Marahner 模型
把光线的效果分解。 81
1.反射，圆锥形方向。 R
2.进入（折射） t 出去1折射了，圆雉， T T
3. 进入1折射） t 内壁（反射） t 出去断射）、 IRT
[49=24在了
效果。[49246]
##Fur 表面
Hair 模型缺少 Medulla 的模拟，因此用在动物上效果
不好。
##Fl Double Cylinder 模型
[55：13]
增加 T T。和 T RTs
##Granular 材质
[58：37了 䍙颗粒物质的建模
非常耗时
##表面模型
###半透明材质，例如二
物理特点。 [1：01：58了在
二人表面反射：入射点生出射点 （13155的门
BRDF: 八射点=出射点
各个方向积分→各个方面积分各个惆有点积分

####Dipole 近仆人
用两个光源照射表面，能得到类似况表面映射的结果.
I:屿啊 82
###布料 Cloth
布料结数栋[1：09：24]
䨻→豳→嚃-鼠
Rendering as Surface
根据编织的形状请计算
适用场景：[1：11：28在了布料麺是平面
越适用场景。[1：儿讨在了 -_-。不是平面
Render as Participating Media
把 cloth 看作是空间体积
划分为细小的格子.
Render as Fiber
暴力计算
##细节模型
#程序化生成外观 Il:27=21]
定义函数拟， y、区），
用于查询空间中某一点的纹理






------------------------------

> 本文出自CaterpillarStudyGroup，转载请注明出处。
>
> https://caterpillarstudygroup.github.io/GAMES101_mdbook/