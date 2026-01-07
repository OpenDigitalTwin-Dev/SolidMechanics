# 客观性

客观性是指某一物理量或物理状态在不同观察者或参考系下保持不变，即其物理意义不依赖于描述者的选择。例如，密度、弹性模量和应力状态等物理量应具有客观性

然而，有些物理量在描述时需要借助参考坐标系，例如应力张量、速度矢量等。在不同的参考系下，这些物理量的坐标分量可能会发生变化，导致其表达形式具有参考系依赖性，这种现象被称为“不客观”

因此，对于那些本质上应保持客观性的物理量，我们需要制定明确的变换准则，使它们在不同的参考系下能够遵循特定的变换规则，从而保证其物理意义的一致性

```{margin}
$\mathbf{c}(t)$ 是平移向量，$\mathbf{Q}(t)$ 是旋转矩阵
```

当坐标框架发生运动（这种运动是相对于物体的）

$$
\mathbf{x}^{*}=\mathbf{c}(t)+\mathbf{Q}(t)\mathbf{x}
$$

时，常量、向量、张量当且仅当满足下述要求，被称为客观的

1. 常量：$\phi^{*}(\mathbf{x}^{*},t^{*})=\phi(\mathbf{x},t)$
2. 向量：$\mathbf{u}^{*}(\mathbf{x}^{*},t^{*})=\mathbf{Q}(t)\mathbf{u}(\mathbf{x},t)$
3. 张量：$\mathbf{S}^{*}(\mathbf{x}^{*},t^{*})=\mathbf{Q}(t)\mathbf{S}(\mathbf{x},t)\mathbf{Q}^{T}(t)$
4. 双点二阶张量：$\mathbf{F}^{*}(\mathbf{x}^{*},t^{*})=\mathbf{Q}(t)\mathbf{F}(\mathbf{x},t)$

其中，$\mathbf{t}^{*}=t-a$，$a$ 是常数

```{admonition} 双点二阶张量
:class: tip, dropdown

双点张量是指指标分别属于不同的空间或参考系，如变形梯度矩阵 $\mathbf{F}$，满足

$$
\mathrm{d}\mathbf{x} = \mathbf{F}\mathrm{d}\mathbf{X},
$$

一方面

$$
\mathrm{d}\mathbf{x}^{*}=\mathbf{F}^{*}\mathrm{d}\mathbf{X},
$$

另一方面

$$
\mathrm{d}\mathbf{x}^{*}=\mathbf{Q}^{*}\mathrm{d}\mathbf{x}=\mathbf{Q}^{*}\mathbf{F}\mathrm{d}\mathbf{X},
$$

故

$$
\mathbf{F}^{*} = \mathbf{Q}^{*}\mathbf{F}.
$$

```

## 应变

考虑映射

$$
\mathbf{x}^{*}(\mathbf{X},t^{*})=\mathbf{c}(t)+\mathbf{Q}(t)\mathbf{x},\quad t^{*}=t-a
$$

在新的构型或参考坐标（相对运动）下，Cauchy-Green 应变张量和 Green-Lagrange 应变张量满足

$$
\begin{aligned}
\mathbf{C}^{*}&=(\mathbf{F}^{*})^{T}\mathbf{F}^{*}=(\mathbf{Q}\mathbf{F})^{T}(\mathbf{Q}\mathbf{F}) = \mathbf{F}^{T}\mathbf{F} = \mathbf{C}\\
\mathbf{E}^{*}&=\frac{1}{2}(\mathbf{C}^{*}-\mathbf{I}^{*}) = \mathbf{E} 
\end{aligned}
$$

速度场显然不是客观的

$$
\mathbf{v}^{*}(\mathbf{x}^{*},t)=\frac{\mathrm{d}\mathbf{x}^{*}}{\mathrm{d}t^{*}}=\frac{\mathrm{d}}{\mathrm{d}t}(\mathbf{c}(t)+\mathbf{Q}(t)\mathbf{x})=\dot{\mathbf{c}}(t)+\dot{\mathbf{Q}}(t)\mathbf{x}+\mathbf{Q}(t)\mathbf{v}
$$

速度梯度场

$$
\begin{aligned}
\mathbf{l}^{*} = \nabla_{*}\mathbf{v}(\mathbf{x}^{*},t^{*})&=\nabla_{*}\left(\dot{\mathbf{c}}(t)+\dot{\mathbf{Q}}(t)\mathbf{x}+\mathbf{Q}(t)\mathbf{v}
\right)\\
&=\frac{\partial }{\partial \mathbf{x}}\left(\dot{\mathbf{c}}(t)+\dot{\mathbf{Q}}(t)\mathbf{x}+\mathbf{Q}(t)\mathbf{v}
\right)\frac{\partial \mathbf{x}}{\partial\mathbf{x}^{*}}\\
&=\dot{\mathbf{Q}}(t)\mathbf{Q}^{T}(t)+\mathbf{Q}(t)\mathbf{l}\mathbf{Q}^{T}(t)
\end{aligned}
$$

变形率张量

$$
\begin{aligned}
\mathbf{d}^{*}&=\frac{1}{2}(\mathbf{l}^{*}+(\mathbf{l}^{*})^{T})\\
&=\frac{1}{2}(\dot{\mathbf{Q}}\mathbf{Q}^{T}+\mathbf{Q}\mathbf{l}\mathbf{Q}^{T} + \mathbf{Q}\dot{\mathbf{Q}}^{T}+\mathbf{Q}\mathbf{l}\mathbf{Q}^{T})\\
&=\mathbf{Q}\mathbf{d}\mathbf{Q}^{T}
\end{aligned}
$$

是客观的

其中，最后一步等式是因为

$$
\mathbf{0}=\dot{\mathbf{I}} = \frac{\mathrm{d}}{\mathrm{d}t}(\mathbf{Q}\mathbf{Q}^{T}) = \dot{\mathbf{Q}}\mathbf{Q}^{T} + \mathbf{Q}\dot{\mathbf{Q}}^{T}
$$

## 应力

对于 Cauchy 应力张量，有

$$
\mathbf{t}=\boldsymbol{\sigma}\mathbf{n},\quad \mathbf{t}^{*}=\boldsymbol{\sigma}^{*}\mathbf{n}^{*},
$$

另一方面

$$
\mathbf{t}^{*}=\mathbf{Q}\mathbf{t},\quad \mathbf{n}^{*}=\mathbf{Q}\mathbf{n},
$$

两式结合对比

$$
\boldsymbol{\sigma}^{*} = \mathbf{Q}\boldsymbol{\sigma}\mathbf{Q}^{T}
$$

故 Cauchy 应力张量是客观的

对于 PK1 应力张量

$$
\mathbf{P}^{*}=J^{*}\boldsymbol{\sigma}^{*}(\mathbf{F}^{*})^{T}=J\mathbf{Q}\boldsymbol{\sigma}\mathbf{Q}^{T}(\mathbf{Q}\mathbf{F})^{-T} = J\mathbf{Q}\boldsymbol{\sigma}\mathbf{F}^{-T} = \mathbf{Q}\mathbf{P}
$$

故 PK1 应力张量是客观的

对于 PK2 应力张量

$$
\mathbf{S}^{*}=J^{*}(\mathbf{F}^{*})^{-1}\boldsymbol{\sigma}^{*}(\mathbf{F}^{*})^{T}=J\mathbf{F}^{-1}\mathbf{Q}^{-1}\mathbf{Q}\boldsymbol{\sigma}\mathbf{Q}^{T}(\mathbf{Q}\mathbf{F})^{-T} = \mathbf{S}
$$

故 PK2 应力张量在刚体运动下保持不变