# 本构方程

<span class="gray-text">
本构方程揭示了应变与应力之间的内在联系。通过实验研究与理论推导，对材料在不同载荷条件下的变形行为进行分析，建立了描述应力与应变关系的方程
</span>

在理想弹性体中，应变与应力的分量满足**广义胡克定律**

```{margin}
应力作用方向与应变方向之间的差异性

在之后的内容中，统一使用 $\sigma$ 表示切应力
```

$$
\begin{equation}
\begin{aligned}
&\varepsilon_{xx} = \frac{1}{E} \left[ \sigma_{xx} - \nu (\sigma_{yy} + \sigma_{zz}) \right],\\
&\varepsilon_{yy} = \frac{1}{E} \left[ \sigma_{yy} - \nu (\sigma_{zz} + \sigma_{xx}) \right],\\
&\varepsilon_{zz} = \frac{1}{E} \left[ \sigma_{zz} - \nu (\sigma_{xx} + \sigma_{yy}) \right],\\
&\gamma_{yz} = \frac{1}{G} \sigma_{yz}, \quad \gamma_{zx} = \frac{1}{G} \sigma_{zx}, \quad \gamma_{xy} = \frac{1}{G} \sigma_{xy},
\end{aligned}
\end{equation}
$$ (sec5-eq:strain-stress-1)

其中

```{margin}
由于假定材料具有完全弹性、均匀性和各向同性，这些常数不随应力应变的大小、位置或方向发生变化
```

1. $E$（**拉压弹性模量**）：又称**弹性模量**，是衡量材料在弹性范围内抵抗拉伸或压缩形变能力的物理量，反映材料的刚性或硬度
2. $G$（**切变模量**）：又称**剪切模量**或**刚度模量**，是描述材料在弹性范围内抵抗剪切形变能力的物理量，反映材料在受剪切力作用下的刚性
3. $\nu$（**泊松比**）：又称**泊松系数**，是描述材料在一个方向受拉伸或压缩时，横向形变与轴向形变之比的物理量，反映材料**变形**的各向异性特征

它们之间满足

$$
G = \frac{E}{2(1+\nu)}.
$$ (sec5-eq:strain-stress-2)

应力与应变的关系可以写为

$$
\boldsymbol{\sigma}=\mathbf{D}:\boldsymbol{\varepsilon},
$$

其中，$\boldsymbol{\sigma}$ 是应力张量，$\boldsymbol{\varepsilon}$ 是应变张量，$\mathbf{D}$ 是四阶本构张量

$$
D_{ijkl} = \lambda\delta_{ij}\delta_{kl}+\mu(\delta_{ik}\delta_{jl}+\delta_{il}\delta_{jk})
$$

其中，$\lambda=\frac{E \nu}{(1+\nu)(1-2\nu)}$ 是第一拉梅常数，$\mu=G=\frac{E}{2(1+\nu)}$ 是第二拉梅常数，于是

$$
\boldsymbol{\sigma}_{ij}=\mathbf{D}_{ijkl}\boldsymbol{\varepsilon}_{kl}
$$

也可以写为 Voigt 形式

$$
\boldsymbol{\sigma}=\mathbf{D}\boldsymbol{\varepsilon},
$$

其中，$\boldsymbol{\sigma}$ 是应力向量，$\boldsymbol{\varepsilon}$ 是应变向量，$\mathbf{D}$ 是本构矩阵

$$
\begin{equation}
\boldsymbol{\sigma}=
\begin{bmatrix}
\sigma_{xx}\\\sigma_{yy}\\\sigma_{zz}\\\sigma_{xy}\\\sigma_{xz}\\\sigma_{yz}
\end{bmatrix},\quad
\boldsymbol{\varepsilon}=
\begin{bmatrix}
\varepsilon_{xx}\\\varepsilon_{yy}\\\varepsilon_{zz}\\2\varepsilon_{xy}\\2\varepsilon_{xz}\\2\varepsilon_{yz}
\end{bmatrix},\quad
\mathbf{D} =
\begin{bmatrix}
\lambda + 2\mu & \lambda & \lambda & 0 & 0 & 0 \\
\lambda & \lambda + 2\mu & \lambda & 0 & 0 & 0 \\
\lambda & \lambda & \lambda + 2\mu & 0 & 0 & 0 \\
0 & 0 & 0 & \mu & 0 & 0 \\
0 & 0 & 0 & 0 & \mu & 0 \\
0 & 0 & 0 & 0 & 0 & \mu
\end{bmatrix}.
\end{equation}
$$

其中，$\lambda$ 和 $\mu$ 是拉梅常数