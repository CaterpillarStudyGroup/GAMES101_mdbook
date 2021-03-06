# 高级 Appreǎue 建模

## 非表面模型 [38：38]

### 反射介质

例如：雾、云
特点：
光线打到一个介质颗粒上，会被分散（散射）至到各个方向上（图3），也会接受到来自其它方向散射而来的光（图4）
怎么散射：  
1. diffuse 表面：均匀散射到各个方向
2. 介质颗粒：散射由 phase function 来定义
怎么生成 path? [42：07]
1. 根据 phase function 决定 bounce 方向
2. 根据介质对光线吸收呈度决定 distance
3. 形成 ray path

### Hair 表面 [45:45]

无色高光，有色高光

#### kajiya-Kay 模型
把每一根头发看成是圆柱，会把光线产生圆雉形的反射和各个方向的散射
效果：[47：05]

#### Marahner 模型
把光线的效果分解。
1. 反射，圆锥形方向。 R
2. 进入（折射） + 出去（折射），圆雉， T T
3. 进入（折射） + 内壁（反射） + 出去（折射）， IRT
[49：24右]  
效果：[49：46]

### Fur 表面

Hair 模型缺少 Medulla 的模拟，因此用在动物上效果不好。

#### Double Cylinder 模型 [55：13]

增加 TTs 和 TRTs

### Granular 材质
[58：37] 颗粒物质的建模，非常耗时

## 表面模型

### 半透明材质

例如：玉
物理特点： [1：01：58]左  
次表面反射：入射点 \\(\ne\\) 出射点 (BSSRDF)
BRDF的入射点=出射点，因此要把BRDF中各个方向积分改为各个方向积分各个入射点积分

#### Dipole 近似

用两个光源照射表面，能得到类似次表面映射的结果.[1:05:07]

### 布料 Cloth

布料结构[1：09：24]
纤维(fiber) → 股(ply) → 线(yarn) → 布(cloth)

#### Rendering as Surface

根据编织的形状请计算
适用场景：[1：11：28左] 布料表面是平面  
不适用场景：[1：11：28右] 布料表面不是平面

#### Render as Participating Media

把 cloth 看作是空间体积，划分为细小的格子.

#### Render as Fiber

暴力计算

### 细节模型

# 程序化生成外观 [1:27:21]

定义函数f(x, y, z)，用于查询空间中某一点的纹理

------------------------------

> 本文出自CaterpillarStudyGroup，转载请注明出处。
>
> https://caterpillarstudygroup.github.io/GAMES101_mdbook/