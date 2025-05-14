# 第二类 Piola-Kirchhoff 应力张量

<span class="gray-text">
第二类 Piola-Kirchhoff 应力张量是对称张量，广泛应用于非线性力学分析。它同样以参考构形为基础，常用于建立大变形下的应力-应变关系，特别适合于推导和表达材料的本构关系及能量守恒等理论分析
</span>

第二类 Piola-Kirchhoff 应力张量（简记为 PK2 应力张量）定义为

$$
\mathbf{S}  = F^{-1}\mathbf{P} = JF^{-1}\boldsymbol{\sigma}F^{-T},
$$

[PK1 应力](./sec1-1stPiolaKirchhoff.md)描述的是**当前力在参考面积上的分布**，表示参考构型下单位面积上所受的当前构型下的力

PK2 应力描述的是**参考力在参考面积上的分布**，参考构型下单位面积上所受的力，该力用参考构型的基底表示

## 对称性

若 $\boldsymbol{\sigma}$ 对称，则 $\mathbf{S}$ 也对称

## 刚体旋转

对于刚体旋转，$F$ 是旋转变换矩阵

$$
\mathbf{x} = F\mathbf{X},\quad \text{或},\quad \mathbf{X} = F^{-1}\mathbf{x},
$$

此时

$$
\mathbf{S}  = F^{-1}\boldsymbol{\sigma}F^{-T},
$$

即 $\mathbf{S}$ 是 $\boldsymbol{\sigma}$ 在初始构型下的表示