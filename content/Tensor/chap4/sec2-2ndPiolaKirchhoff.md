# 第二类 Piola-Kirchhoff 应力张量

<span class="gray-text">
第二类 Piola-Kirchhoff 应力张量是对称张量，广泛应用于非线性力学分析。它同样以参考构形为基础，常用于建立大变形下的应力-应变关系，特别适合于推导和表达材料的本构关系及能量守恒等理论分析
</span>

第二类 Piola-Kirchhoff 应力张量（简记为 PK2 应力张量）定义为

$$
\mathbf{S}  = F^{-1}\mathbf{P} = JF^{-1}\boldsymbol{\sigma}F^{-T},
$$


[PK1 应力](./sec1-1stPiolaKirchhoff.md)描述的是**当前力在参考面积上的分布**，表示参考构型下单位面积上所受的当前构型下的力

PK2 应力描述的是**参考力在参考面积上的分布**，该参考力并非真实存在的力，而是通过逆变形梯度 $F^{-1}$ 将真实力 $\mathrm{d}\mathbf{f}$ 映射回参考构型的等效力 $\mathrm{d}\mathbf{F}_{\text{ref}}$


## 对称性

若 $\boldsymbol{\sigma}$ 对称，则 $\mathbf{S}$ 也对称

## 刚体旋转

对于刚体旋转，$F$ 是旋转变换矩阵

$$
\mathbf{x} = F\mathbf{X},\quad \text{或},\quad \mathbf{X} = F^{-1}\mathbf{x},
$$

此时

$$
\mathbf{S}  = F^{-1}\boldsymbol{\sigma}F^{-T} = F^{-1}\boldsymbol{\sigma}F,
$$

即 $\mathbf{S}$ 是 $\boldsymbol{\sigma}$ 在初始构型基底下的表示

## 应变能

```{margin}
超弹性材料，又称伪弹性材料，是一类在较大应变范围（5%~10%）内能够完全恢复原始形状的材料
```

应变能密度函数 $\Psi$ 是材料在变形过程中单位参考体积储存的能量，仅依赖于变形状态。对于超弹性材料，$\Psi$ 是 Green-Lagrange 应变张量 $\mathbf{E}$ 的函数：

$$
\Psi = \Psi(\mathbf{E}).
$$

其物理意义是：**材料在变形过程中抵抗变形所做的功全部转化为弹性势能**

PK2 应力 $\mathbf{S}$ 与 Green-Lagrange 应变 $\mathbf{E}$ 共轭：

$$
\mathbf{S} = \frac{\partial \Psi}{\partial \mathbf{E}}.
$$

### 功率守恒

功率守恒要求参考构型与当前构型的应力功率相等：

$$
\mathbf{S}:\dot{\mathbf{E}}\ \mathrm{d}V_{0} = \boldsymbol{\sigma}:\mathbf{D}\ \mathrm{d}V,
$$

其中，$\mathbf{D} = \frac{1}{2}(\mathbf{L} + \mathbf{L}^{T})$ 是应变率张量，$\mathrm{d}V = J\mathrm{d}V_{0}$ 是体积变化

由于