# 第一类 Piola-Kirchhoff 应力张量

<span class="gray-text">
第一类 Piola-Kirchhoff 应力张量是非对称应力张量，常用于非线性力学分析。它以参考构形为基础，能够方便地处理边界条件、建立大变形下的应力-应变关系，并在推导平衡方程时起到关键作用
</span>

## Nanson 公式

Nanson 公式描述了连续介质变形过程中参考构型（未变形状态）与当前构型（变形后状态）之间面积元素的转换关系

$$
\mathbf{n}\ \mathrm{d}a = J\mathbf{F}^{-T}\mathbf{N}\ \mathrm{d}A,
$$

其中，$\mathbf{n}\ \mathrm{d}a$ 和 $\mathbf{N}\ \mathrm{d}A$ 分别是当前构型和初始构型的面积向量，$\mathbf{n}$ 和 $\mathbf{N}$ 为相应的法向量

```{admonition} 证明
:class: tip, dropdown

在参考构型中，取两个微小线元，$\mathrm{d}\mathbf{X}_{1}$ 和 $\mathrm{d}\mathbf{X}_{2}$，于是

$$
\mathbf{N}\ \mathrm{d}A = \mathrm{d}\mathbf{X}_{1}\times\mathrm{d}\mathbf{X}_{2},
$$

在当前构型中，有 $\mathrm{d}\mathbf{x}_{i} = \mathbf{F}\mathrm{d}\mathbf{X}_{i}$，于是

$$
\begin{equation}
\begin{aligned}
\mathbf{n}\ \mathrm{d}a = \mathrm{d}\mathbf{x}_{1}\times\mathrm{d}\mathbf{x}_{2} &= (\mathbf{F}\mathrm{d}\mathbf{X}_{1})\times(\mathbf{F}\mathrm{d}\mathbf{X}_{2})\\
&=\det(\mathbf{F})\mathbf{F}^{-T}(\mathrm{d}\mathbf{X}_{1}\times\mathrm{d}\mathbf{X}_{2})\\
&=J\mathbf{F}^{-T}\mathbf{N}\ \mathrm{d}A,
\end{aligned}
\end{equation}
$$


**证明：** $(\mathbf{F}\mathbf{b})\times(\mathbf{F}\mathbf{c})=\det(\mathbf{F})\mathbf{F}^{-T}(\mathbf{b}\times\mathbf{c})$ 


若 $\mathbf{a},\mathbf{b},\mathbf{c}$ 线性无关且可逆，则

$$
\frac{\mathbf{F}\mathbf{a}\cdot(\mathbf{F}\mathbf{b}\times \mathbf{F}\mathbf{c})}{\mathbf{a}\cdot(\mathbf{b}\times \mathbf{c})}=
\frac{\det\left(\begin{bmatrix}
\mathbf{F}\mathbf{a}&\mathbf{F}\mathbf{b}&\mathbf{F}\mathbf{c}
\end{bmatrix}\right)}{
\det\left(\begin{bmatrix}
\mathbf{a}&\mathbf{b}&\mathbf{c}
\end{bmatrix}\right)
} = \det(\mathbf{F}),
$$

分别取 $\mathbf{a} = \mathbf{e}_{1},\mathbf{e}_{2},\mathbf{e}_{3}$ 代入，得到结论

```


## 第一类 Piola-Kirchhoff 应力张量

根据 Nanson 公式，有

$$
\mathrm{d}\mathbf{f} = \boldsymbol{\sigma}\mathbf{n}\ \mathrm{d}a = \boldsymbol{\sigma}J\mathbf{F}^{-T}\mathbf{N}\ \mathrm{d}A = \mathbf{P}\mathbf{N}\ \mathrm{d}A,
$$

其中

$$
\mathbf{P}=J\boldsymbol{\sigma}\mathbf{F}^{-T}
$$ (sec1-eq:pk1)

定义为第一类 Piola-Kirchhoff 应力张量（也称名义应力张量），简记为 PK1 应力张量

[Cauchy 应力](../../Elasticity/chap1/sec1-stress_strain_displ.md)描述的是**当前力在当前面积下的分布**，表示当前构型下单位面积上所受的当前构型下的力

PK1 应力描述的则是**当前力在参考面积上的分布**，表示参考构型下单位面积上所受的当前构型下的力



PK1 应力张量一般是非对称张量，因为它涉及到与变形梯度 $\mathbf{F}$ 的混合

此外，由于

$$
\mathbf{P}\mathbf{N} = \frac{\mathrm{d}\mathbf{f}}{\mathrm{d} A},
$$

因此，第一类 Piola-Kirchhoff 应力张量可以看作是一维工程应力（初始面积上的力）在三维情况下的自然推广

### 内功率

根据式 {eq}`sec1-eq:pk1`，有

$$
\boldsymbol{\sigma}=J^{-1}\mathbf{P}\mathbf{F}^{T},
$$

于是

$$
\boldsymbol{\sigma}:\mathbf{D} = \boldsymbol{\sigma}:\mathbf{L} = J^{-1}\text{tr}(\mathbf{P}\mathbf{F}^{T}\mathbf{L}^{T}),
$$

代入 $\mathbf{L} = \dot{\mathbf{F}}\mathbf{F}^{-1}$，得到

$$
\boldsymbol{\sigma}:\mathbf{D} = J^{-1}\text{tr}(\mathbf{P}\mathbf{F}^{T}\mathbf{L}^{T}) = J^{-1}\text{tr}(\mathbf{P}\dot{\mathbf{F}}^{T}) = J^{-1}\mathbf{P}:\dot{\mathbf{F}},
$$

于是

$$
P_{\text{int}} = \int_{V}\boldsymbol{\sigma}:\mathbf{D}\ \mathrm{d}V = \int_{V_{0}}\mathbf{P}:\dot{\mathbf{F}}\ \mathrm{d}V_{0}.
$$


### 边界条件

由于 PK1 应力张量的定义是基于参考构型的面积和当前力，采用 PK1 应力后，可以直接在初始构型上施加和计算边界条件，无需在整个分析过程中追踪当前构型的边界和应力状态，大大简化了大变形问题中的边界条件处理