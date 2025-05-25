# 弹塑性本构方程


将[应变率张量](../../Tensor/chap3/sec1-velocity-gradient.md)分解为弹性部分和塑性部分

$$
\mathbf{D} = \mathbf{D}^{e} + \mathbf{D}^{p},
$$

弹性部分给出了应变增量的可逆部分，满足

$$
\mathbf{D}^{e} = \mathbf{M}^{e}:\overset{\nabla}{\boldsymbol{\tau}},
$$

其中，$\overset{\nabla}{\boldsymbol{\tau}}$ 是 [Kirchhoff 应力的 Jaumann 应力率](../../Tensor/chap5/sec1-jaumann.md)，$\mathbf{M}^{e}$ 是四阶弹性柔量张量（elastic compliance tensor），是弹性模量张量的逆

$$
M_{ijkl}^e = \frac{1}{2\mu} \left[ \frac{1}{2} (\delta_{ik}\delta_{jl} + \delta_{il}\delta_{jk}) - \frac{\lambda}{2\mu + 3\lambda} \delta_{ij}\delta_{kl} \right],
$$

$\lambda,\mu$ 是[拉梅常数](../../Elasticity/chap1/sec5-physical-equa.md)

在关联塑性理论中，变形速率张量的塑性部分与应力空间中屈服面的外法线方向一致

$$
\mathbf{D}^{p} = \dot{\gamma} \frac{\partial f}{\partial \boldsymbol{\sigma}}, \qquad \dot{\gamma} > 0,
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
> 0, & \text{塑形加载,} \\
= 0, & \text{自然加载,} \\
< 0, & \text{弹性卸载.}
\end{cases}
$$

将 {eq}`intro-eq:ep2` 代入到 {eq}`intro-eq:ep1`，得到

$$
\mathbf{D}^{p} = \frac{1}{H} \left( \frac{\partial f}{\partial \boldsymbol{\sigma}} : \overset{\nabla}{\boldsymbol{\tau}} \right) \frac{\partial f}{\partial \boldsymbol{\sigma}},
$$

物理意义上，变形率张量的塑性增量 $\mathbf{D}^{p}\mathrm{d}t$ 是指在施加并去除应力增量 $\overset{\nabla}{\boldsymbol{\tau}}\mathrm{d}t$ 的一个循环后，所剩下的残余应变增量






于是，总的弹塑性本构方程结构是

$$
\mathbf{D} = \mathbf{M}^e: \overset{\nabla}{\boldsymbol{\tau}} +\frac{1}{H} \left( \frac{\partial f}{\partial \boldsymbol{\sigma}} : \overset{\nabla}{\boldsymbol{\tau}} \right) \frac{\partial f}{\partial \boldsymbol{\sigma}}.
$$