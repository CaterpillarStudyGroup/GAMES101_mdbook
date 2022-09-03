# Rigid Body （刚体）模拟

刚体运动本身不会发生形变，可以简单看作是粒子扩充

但刚体会考虑更多的物理量的模拟：  

|物理量|物理量的变化|
|---|---|
|X：position|\\(\dot X\\)：速度|
|\\(\theta\\)：旋转角度|\\(\omega\\)：角速度|
|\\(\dot X\\)：速度|\\(\frac{F}{M}\\)：加速度|
|\\(\omega\\)：角速度|\\(\frac{\Gamma}{I}\\)：角加速度|


------------------------------

> 本文出自CaterpillarStudyGroup，转载请注明出处。  
> https://caterpillarstudygroup.github.io/GAMES101_mdbook/