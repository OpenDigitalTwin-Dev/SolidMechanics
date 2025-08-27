# 第二类 Piola-Kirchhoff 应力张量

<span class="gray-text">
第二类 Piola-Kirchhoff 应力张量是对称张量，广泛应用于非线性力学分析。它同样以参考构形为基础，常用于建立大变形下的应力-应变关系，特别适合于推导和表达材料的本构关系及能量守恒等理论分析
</span>

第二类 Piola-Kirchhoff 应力张量（简记为 PK2 应力张量）定义为

$$
\mathbf{S}  = \mathbf{F}^{-1}\mathbf{P} = J\mathbf{F}^{-1}\boldsymbol{\sigma}\mathbf{F}^{-T},
$$


[PK1 应力](./sec1-1stPiolaKirchhoff.md)描述的是**当前力在参考面积上的分布**，表示参考构型下单位面积上所受的当前构型下的力

PK2 应力描述的是**参考力在参考面积上的分布**，该参考力并非真实存在的力，而是通过逆变形梯度 $\mathbf{F}^{-1}$ 将真实力 $\mathrm{d}\mathbf{f}$ 映射回参考构型的等效力 $\mathrm{d}\mathbf{F}_{\text{ref}}$

也可以用 $\mathbf{S}$ 表示 $\boldsymbol{\sigma}$

$$
\boldsymbol{\sigma} = J^{-1}\mathbf{F}\mathbf{S}\mathbf{F}^{T}.
$$

## 对称性

若 $\boldsymbol{\sigma}$ 对称，则 $\mathbf{S}$ 也对称

## 客观性

对于刚体旋转，$\mathbf{F}' = R\mathbf{F}$，$R$ 是旋转变换矩阵，满足 $RR^{T} = \mathbf{I}$，且 

$$
J' = \det(\mathbf{F}') = \det(R)\det(\mathbf{F}) = \det(\mathbf{F}) = J,
$$

此时

$$
\mathbf{S}'  = J'\mathbf{F}'^{-1}\boldsymbol{\sigma}'\mathbf{F}'^{-T} = J\mathbf{F}^{-1}R^{-1}(R\boldsymbol{\sigma}R^{T})R\mathbf{F}^{-T} = \mathbf{S},
$$

即 PK2 应力在刚体旋转下保持不变，具有客观性


## 内功率

由于

$$
\dot{\mathbf{E}} = \frac{1}{2}\frac{\mathrm{d}}{\mathrm{d}t}(\mathbf{F}^{T}\mathbf{F}-\mathbf{I}) = \frac{1}{2}(\mathbf{F}^{T}\dot{\mathbf{F}}+\dot{\mathbf{F}}^{T}\mathbf{F}) = \mathbf{F}^{T}\mathbf{D}\mathbf{F},
$$

故

$$
\mathbf{D} = \mathbf{F}^{-T}\dot{\mathbf{E}}\mathbf{F},
$$

由于相似变换保迹，于是

$$
\begin{equation}
\begin{aligned}
\boldsymbol{\sigma}:\mathbf{D} &= \boldsymbol{\sigma}:\mathbf{F}^{-T}\dot{\mathbf{E}}\mathbf{F} = \text{tr}(\boldsymbol{\sigma}\mathbf{F}^{-T}\dot{\mathbf{E}}\mathbf{F}) \\
&= \text{tr}(\mathbf{F}^{-1}\boldsymbol{\sigma}\mathbf{F}^{-T}\dot{\mathbf{E}}) = \mathbf{F}^{-1}\boldsymbol{\sigma}\mathbf{F}^{-T}:\dot{\mathbf{E}}\\
&=J^{-1}\mathbf{S}:\dot{\mathbf{E}},
\end{aligned}
\end{equation}
$$

于是

$$
P_{\text{int}} = \int_{V}\boldsymbol{\sigma}:\mathbf{D}\ \mathrm{d}V = \int_{V_{0}}\mathbf{S}:\dot{\mathbf{E}}\ \mathrm{d}V_{0}.
$$