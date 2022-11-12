# 流体 Fluid 模拟

把水看作是很多个 rigid body sphere 的水滴，通过模拟的有水滴的位置，来模拟水的运动.   
假设水珠不可压缩（刚体），修正目标为水珠的密度（与前面都是修正位置不同），类似前面的 position based 方法。

# 质点法 VS 网格法

- 质点法，又称为拉格朗日方法。依次分析每一个质点的运动。  
- 网格法，又称为欧拉方法（与前面提到的欧拉方法解ODE没有关系）。把场景分成网格，分析网格随着时间的变化。
- MPM，material point method，以上两种方法的结合。

> &#x2705; 这里的网格跟体素不是一回事。质点、体素都是对物理的描述，网格是对环境的描述。  

------------------------------

> 本文出自CaterpillarStudyGroup，转载请注明出处。  
> https://caterpillarstudygroup.github.io/GAMES101_mdbook/