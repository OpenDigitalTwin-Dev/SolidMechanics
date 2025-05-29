# 弹塑性本构方程


将[应变率张量](../../Tensor/chap3/sec1-velocity-gradient.md)分解为弹性部分和塑性部分

$$
\mathbf{D} = \mathbf{D}^{\text{e}} + \mathbf{D}^{\text{p}},
$$ (intro-eq:strain)

弹性部分给出了应变增量的可逆部分，满足

$$
\mathbf{D}^{\text{e}} = \mathbf{M}^{\text{e}}:\overset{\nabla}{\boldsymbol{\tau}},
$$ (intro-eq:strain-e)

```{admonition}  $\dot{\boldsymbol{\tau}}$ or $\overset{\circ}{\boldsymbol{\tau}}(\text{or }\overset{\nabla}{\boldsymbol{\tau}})$ ？

**注意：在涉及大变形的情形下，时间导数的计算通常采用客观应力率 $\overset{\circ}{\boldsymbol{\tau}}(\text{or }\overset{\nabla}{\boldsymbol{\tau}})$，而不是常规的材料导数 $\dot{\boldsymbol{\tau}}$，这是因为[客观应力率具有良好的框架无关性](../../Tensor/chap5/intro.md)，能够正确反映物理量在不同参考系下的一致性**

**需要特别指出的是，通常 $\dot{\boldsymbol{\tau}}\neq\overset{\circ}{\boldsymbol{\tau}}(\text{or }\overset{\nabla}{\boldsymbol{\tau}})$，两者只有在小变形、小旋转的情况下才近似相等。因此，这种处理其实是一种近似建模手段，其物理基础和适用范围需加以注意**

```


其中，$\overset{\nabla}{\boldsymbol{\tau}}$ 是 [Kirchhoff 应力的 Jaumann 应力率](../../Tensor/chap5/sec1-jaumann.md)，$\mathbf{M}^{\text{e}}$ 是四阶各向同性弹性材料的柔度张量（elastic compliance tensor），是弹性模量张量（弹性刚度张量）的逆

$$
\mathbf{M}^{\text{e}} = \frac{1}{2\mu}\left(\mathbf{I}^{s} - \frac{\lambda}{2\mu + 3\lambda}\mathbf{I}\otimes\mathbf{I}\right),
$$

或

$$
M_{ijkl}^{\text{e}} = \frac{1}{2\mu} \left[ \frac{1}{2} (\delta_{ik}\delta_{jl} + \delta_{il}\delta_{jk}) - \frac{\lambda}{2\mu + 3\lambda} \delta_{ij}\delta_{kl} \right],
$$

其中，$\lambda,\mu$ 是[拉梅常数](../../Elasticity/chap1/sec5-physical-equa.md)，$\mathbf{I}^{s}$ 是四阶对称恒等张量

$$
\mathbf{I}^{s}_{ijkl} = \frac{1}{2} (\delta_{ik}\delta_{jl} + \delta_{il}\delta_{jk}).
$$

## 关联塑性流动理论

<span class="gray-text">
关联塑性流动理论是指材料的塑性流动方向与屈服面法向一致，即塑性势函数 g 与屈服函数 f 完全相同（g=f）。该理论严格遵循最大塑性功原理，理论体系严密，数学处理简便，因而在金属等体积塑性变形不显著的材料本构建模中得到了广泛应用。然而，对于土壤、岩石等摩擦性材料，关联流动法则往往会显著高估材料的体积膨胀效应，导致其在描述此类材料实际力学行为时存在一定局限性
</span>

关联塑性流动理论假设塑性应变增量的方向垂直于屈服面

$$
\mathbf{D}^{\text{p}} = \dot{\gamma} \frac{\partial f}{\partial \boldsymbol{\sigma}}, \qquad \dot{\gamma} > 0,
$$ (intro-eq:ep1)


其中

- $\dot{\gamma}$：塑性乘子，标量，表示塑性流动的“强度”或速率
- $f$：屈服函数，用来描述材料屈服的条件
- $\frac{\partial f}{\partial \boldsymbol{\sigma}}$：屈服面在应力空间中的外法向量

```{note}
:class: dropdown

可以证明，这一正态规则源自塑性假设，该假设指出，在等温应变循环中，如果某个阶段涉及塑性变形，则净功必须为正值。在微小应变的背景下，Drucker基于应力循环引入了塑性假设，这也导致了正态规则和屈服面的凸性

塑性假设是在材料发生塑性变形（不可逆变形）时，对其力学行为所作的基本理论假设，包括屈服准则、流动法则、硬化规律、不可逆性假设、体积不变假设等
```

假定响应线性增加，则塑性乘子的表达式为

$$
\dot{\gamma} = \frac{1}{H} \left( \frac{\partial f}{\partial \boldsymbol{\sigma}} : \overset{\nabla}{\boldsymbol{\tau}} \right),
$$ (intro-eq:ep2)

其中，$H$ 是[硬化模量](../chap1/sec2-uniaxial.md)，依赖于变形历史，可以通过一致性条件，即材料持续处于屈服状态：$\dot{f} = 0$，来求解 $H$

当材料处于硬化范围 $H>0$ 时，根据应力增量的方向，可以识别出三种类型的响应

$$
\frac{\partial f}{\partial \boldsymbol{\sigma}} : \overset{\nabla}{\boldsymbol{\tau}}
\begin{cases}
> 0, & \text{plastic loading,} \\
= 0, & \text{neutral loading,} \\
< 0, & \text{elastic unloading.}
\end{cases}
$$

将 {eq}`intro-eq:ep2` 代入到 {eq}`intro-eq:ep1`，得到

$$
\mathbf{D}^{\text{p}} = \frac{1}{H} \left( \frac{\partial f}{\partial \boldsymbol{\sigma}} : \overset{\nabla}{\boldsymbol{\tau}} \right) \frac{\partial f}{\partial \boldsymbol{\sigma}},
$$ (intro-eq:strain-p)

物理意义上，变形率张量的塑性增量 $\mathbf{D}^{\text{p}}\mathrm{d}t$ 是指在施加并去除应力增量 $\overset{\nabla}{\boldsymbol{\tau}}\mathrm{d}t$ 的一个循环后，所剩下的残余应变增量

根据 $H$ 的正负，存在三种类型的响应

$$
\begin{equation}
\begin{aligned}
H > 0, \quad & \frac{\partial f}{\partial \boldsymbol{\sigma}} : \overset{\nabla}{\boldsymbol{\tau}} > 0, \quad \text{hardening,} \\
H < 0, \quad & \frac{\partial f}{\partial \boldsymbol{\sigma}} : \overset{\nabla}{\boldsymbol{\tau}} < 0, \quad \text{softening,} \\
H = 0, \quad & \frac{\partial f}{\partial \boldsymbol{\sigma}} : \overset{\nabla}{\boldsymbol{\tau}} = 0, \quad \text{ideally plastic.}
\end{aligned}
\end{equation}
$$

- **硬化（Hardening）**：材料变得更“坚硬”，屈服面扩大，应力点会随着加载超出原屈服面，向外移动
- **软化（Softening）**：材料变得更“软”，屈服面缩小，应力点会向屈服面内部移动
- **理想塑性（Ideally plastic）**：屈服面既不扩展也不收缩，应力点只能沿着屈服面切线方向移动

在软化阶段，应变率张量 $\mathbf{D}$ 并不由应力率 $\overset{\nabla}{\boldsymbol{\tau}}$ 唯一确定，这是因为**在软化阶段，应力减小时，材料既可能发生弹性卸载，也可能仍保持塑性流动，甚至可能是两者的组合。这种多种响应路径的可能性，使得本构关系失去唯一性**

由于

$$
\overset{\nabla}{\boldsymbol{\tau}}：\mathbf{D}^{\text{p}} = \frac{1}{H} \left( \frac{\partial f}{\partial \boldsymbol{\sigma}} : \overset{\nabla}{\boldsymbol{\tau}} \right)^2,
$$

因此，上式在硬化阶段为正，软化阶段为负。其逆形式为

$$
\overset{\triangledown}{\tau} = 
\left[
\boldsymbol{\Lambda}^{\text{e}} - \frac{1}{h} 
\left( 
\boldsymbol{\Lambda}^{\text{e}} : \frac{\partial f}{\partial \boldsymbol{\sigma}} 
\right) 
\left( 
\frac{\partial f}{\partial \boldsymbol{\sigma}} : \boldsymbol{\Lambda}^{\text{e}} 
\right)
\right] : \mathbf{D},
$$

其中，$\boldsymbol{\Lambda}^{\text{e}}$ 是弹性刚度张量（$\mathbf{M}^{\text{e}}$ 的逆）

$$
\boldsymbol{\Lambda}^{\text{e}} = 2\mu \mathbf{I}^{s}+\lambda \mathbf{I}\otimes\mathbf{I},
$$

或

$$
\boldsymbol{\Lambda}^{\text{e}}_{ijkl} = \mu (\delta_{ik}\delta_{jl} + \delta_{il}\delta_{jk}) + \lambda\, \delta_{ij}\delta_{kl},
$$

其中

$$
\begin{equation}
h = H + \frac{\partial f}{\partial \boldsymbol{\sigma}} : \boldsymbol{\Lambda}^{\text{e}} : \frac{\partial f}{\partial \boldsymbol{\sigma}}.
\end{equation}
$$

将式 {eq}`intro-eq:strain-e` 和 {eq}`intro-eq:strain-p` 代入到 {eq}`intro-eq:strain`，得到

$$
\begin{equation}
\begin{aligned}
\mathbf{D} &= \mathbf{M}^{\text{e}}: \overset{\nabla}{\boldsymbol{\tau}} +\frac{1}{H} \left( \frac{\partial f}{\partial \boldsymbol{\sigma}} : \overset{\nabla}{\boldsymbol{\tau}} \right) \frac{\partial f}{\partial \boldsymbol{\sigma}}\\
&=\mathbf{M}^{\text{e}}: \overset{\nabla}{\boldsymbol{\tau}} + \frac{1}{H} \left( \frac{\partial f}{\partial \boldsymbol{\sigma}}\otimes\frac{\partial f}{\partial \boldsymbol{\sigma}} \right): \overset{\nabla}{\boldsymbol{\tau}}\\
&=\left(\mathbf{M}^{\text{e}} + \frac{1}{H} \left( \frac{\partial f}{\partial \boldsymbol{\sigma}}\otimes\frac{\partial f}{\partial \boldsymbol{\sigma}} \right)\right): \overset{\nabla}{\boldsymbol{\tau}}.
\end{aligned}
\end{equation}
$$ (intro-eq:strain-t)

```{admonition} $(A\otimes B):C = (B:C)A$
:class: tip, dropdown

$A,B,C$ 为二阶张量，张量积运算为

$$
\left(A\otimes B\right)_{ijkl} = A_{ij}B_{kl},
$$

于是

$$
\left(\left(A\otimes B\right):C\right)_{ij} = A_{ij}B_{kl}C_{kl} = (B:C)A.
$$


```

## 非关联塑性流动理论

<span class="gray-text">
非关联塑性流动理论是指材料的塑性流动方向与屈服面法向不一致，即塑性势函数 g 与屈服函数 f 不同。这一理论不再严格遵循最大塑性功原理，在数学处理上较为复杂，但能够更灵活地描述摩擦性材料（如土壤、岩石、混凝土等）的剪胀效应和体积变化，更贴近实际工程中的材料变形特性
</span>

非关联塑性流动理论假设塑性应变增量的方向垂直于塑性势面

$$
\mathbf{D}^{\text{p}} = \dot{\gamma} \frac{\partial g}{\partial \boldsymbol{\sigma}}, \qquad \dot{\gamma} > 0,
$$ (intro-eq:ep3)

其中，$g$ 是塑性势函数。根据材料持续处于屈服状态的一致性条件 $\dot{f} = 0$，得到

$$
\dot{\gamma} = \frac{1}{H} \left( \frac{\partial f}{\partial \boldsymbol{\sigma}} : \overset{\nabla}{\boldsymbol{\tau}} \right),
$$

因此

$$
\mathbf{D}^{\text{p}} = \frac{1}{H} \left( \frac{\partial f}{\partial \boldsymbol{\sigma}} : \overset{\nabla}{\boldsymbol{\tau}} \right) \frac{\partial g}{\partial \boldsymbol{\sigma}},
$$

类似地

$$
\mathbf{D}=\left(\mathbf{M}^{\text{e}} + \frac{1}{H} \left( \frac{\partial g}{\partial \boldsymbol{\sigma}}\otimes\frac{\partial f}{\partial \boldsymbol{\sigma}} \right)\right): \overset{\nabla}{\boldsymbol{\tau}},
$$

由于 $g\neq f$，因此应变张量 $\mathbf{D}$ 不具有对称性。其逆形式为

$$
\overset{\triangledown}{\tau} = 
\left[
\boldsymbol{\Lambda}^{\text{e}} - \frac{1}{h} 
\left( 
\boldsymbol{\Lambda}^{\text{e}} : \frac{\partial g}{\partial \boldsymbol{\sigma}} 
\right) 
\left( 
\frac{\partial f}{\partial \boldsymbol{\sigma}} : \boldsymbol{\Lambda}^{\text{e}} 
\right)
\right] : \mathbf{D},
$$

其中

$$
\begin{equation}
h = H + \frac{\partial f}{\partial \boldsymbol{\sigma}} : \boldsymbol{\Lambda}^{\text{e}} : \frac{\partial g}{\partial \boldsymbol{\sigma}}.
\end{equation}
$$