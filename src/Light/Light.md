这一节处理渲染方程中Input Light相关的部分。

![](../assets/69-28-4.png)  

全局光照 = 直接光照 + 间接光照

要解决的问题：   
(1) 如何快速地获取来自各个方向的Input Light？  
(2) 如果预计算Input Light，数据量非常大，怎样高效地存储？      
(3) 如何让材质与Input Light做积分。    