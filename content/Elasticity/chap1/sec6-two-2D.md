# 两类平面问题

<span class="gray-text">
弹性体作为空间物体，其实际问题通常为空间问题。然而，当弹性体具有特殊形状，且受特定外力与约束时，可将空间问题简化为平面问题，从而降低计算复杂度，同时满足工程精度要求
</span>

接下来将讨论两类问题：
1. **平面应力问题**：足够薄，厚度方向的应力可以忽略，研究平面内的力学行为
2. **平面应变问题**：足够长，长度方向的变形可以忽略，研究截面内的变形行为

## 平面应力问题

下图展示了**等厚薄板**的受力情况，其中厚度远小于板的长度与宽度

```{figure} ../../../images/Elasticity/chap1/2D-stress.png
---
width: 400px
name: sec5-fig:2D-stress
---
等厚薄板的受力情况
```

```{margin}
微观结构分析：厚度方向的应力难以积累
```

薄板仅在边缘的 $x$ 轴截面和 $y$ 轴截面上受到不随厚度变化的外力，而在边缘的 $z$ 轴截面上无外力作用。由于薄板足够薄，因此在薄板内的任意一点都满足

$$
\sigma_{z}=0,\quad \tau_{zx} = 0,\quad \tau_{zy} = 0.
$$

此外，由切应力互等定理，有

$$
\tau_{xz} = 0,\quad \tau_{yz} = 0.
$$

因此，$\gamma_{zx} = \gamma_{zy} = 0$

由于薄板很薄，且作用力不随厚度变化，因此可以认为应力分量 $\sigma_{x},\sigma_{y}, \tau_{xy}$ 和应变分量 $\epsilon_{x},\epsilon_{y}, \gamma_{xy}$ 是关于 $x$ 和 $y$ 的函数，不随 $z$ 变化

这类问题被称为**平面应力问题**，
此时，方程 {eq}`sec5-eq:strain-stress-1` 可简化为

$$
\begin{equation}
\begin{aligned}
&\epsilon_x = \frac{1}{E} ( \sigma_x - \mu \sigma_y ),\\
&\epsilon_y = \frac{1}{E} (\sigma_y - \mu \sigma_x ),\\
&\gamma_{xy} = \frac{2(1+\mu)}{E} \tau_{xy}.
\end{aligned}
\end{equation}
$$ (sec6-eq:2D-stress-physical)

$\epsilon_z$ 可通过 $\epsilon_z=-\frac{\mu}{E} (\sigma_x + \sigma_y)$ 求得

```{note}
物质的宏观形变源于微观分子结构及分子间作用力的耦合效应。因此，即使某方向无外力作用，内部应力传递仍可能导致该方向形变。
```

在**平面应力问题**中，所求解的方程组是

```{margin}
平衡方程+几何方程+物理方程
```

$$
\begin{equation}
\begin{aligned}
&\frac{\partial \sigma_x}{\partial x} + \frac{\partial \tau_{yx}}{\partial y} + f_x = 0, \\
&\frac{\partial \sigma_y}{\partial y} + \frac{\partial \tau_{xy}}{\partial x} + f_y = 0,\\
&\epsilon_x = \frac{\partial u}{\partial x}, \\
&\epsilon_y = \frac{\partial v}{\partial y}, \\
&\gamma_{xy} = \frac{\partial v}{\partial x} + \frac{\partial u}{\partial y},\\
&\epsilon_x = \frac{1}{E} ( \sigma_x - \mu \sigma_y ),\\
&\epsilon_y = \frac{1}{E} (\sigma_y - \mu \sigma_x ),\\
&\gamma_{xy} = \frac{2(1+\mu)}{E} \tau_{xy},
\end{aligned}
\end{equation}
$$ (sec6-eq:2D-stress-eq)

求解变量为

$$
\sigma_{x}, \, \sigma_{y}, \, \tau_{xy}, \, \epsilon_{x}, \, \epsilon_{y}, \, \gamma_{xy}, \, u, \, v
$$

## 平面应变问题

假设有**无限长的等截面柱形体**，柱面上受有平行于 $z$ 轴截面且不随长度变化的力（面力、体力）或约束

```{margin}
柱体两端通常受到约束，使得长度方向的变形受到限制，即 $\epsilon_z = 0$
```

```{figure} ../../../images/Elasticity/chap1/2D-strain.png
---
width: 400px
name: sec5-fig:2D-strain
---
等截面柱形体的受力情况
```

假设柱体无限长，则任意 $z$ 轴截面上的应力、应变和位移分量均不随 $z$ 方向变化，仅为 $x$ 和 $y$ 的函数。
此外，由于对称性，位移仅沿 $x$ 和 $y$ 方向发生，且 $z$ 轴截面上各点的切应力均为 0，因此

$$
\epsilon_{z} = 0,\quad \tau_{zx} = 0,\quad \tau_{zy}=0.
$$

由胡克定律（见{eq}`sec5-eq:strain-stress-1`），有

$$
\gamma_{zx} = 0,\quad \gamma_{zy} = 0.
$$

```{margin}
$\sigma_{z}$ 一般不为 0，以抵消 $z$ 方向上可能产生的应变
```

代入 $\sigma_{z}=\mu(\sigma_x + \sigma_y)$ 消去 $\sigma_{z}$，方程 {eq}`sec5-eq:strain-stress-1` 可简化为

$$
\begin{equation}
\begin{aligned}
&\varepsilon_x = \frac{1 - \mu^2}{E} \left( \sigma_x - \frac{\mu}{1 - \mu} \sigma_y \right), \\
&\varepsilon_y = \frac{1 - \mu^2}{E} \left( \sigma_y - \frac{\mu}{1 - \mu} \sigma_x \right), \\
&\gamma_{xy} = \frac{2(1 + \mu)}{E} \tau_{xy}.
\end{aligned}
\end{equation}
$$ (sec6-eq:2D-strain-physical)

在**平面应变问题**中，所求解的方程组是

```{margin}
平衡方程+几何方程+物理方程
```

$$
\begin{equation}
\begin{aligned}
&\frac{\partial \sigma_x}{\partial x} + \frac{\partial \tau_{yx}}{\partial y} + f_x = 0, \\
&\frac{\partial \sigma_y}{\partial y} + \frac{\partial \tau_{xy}}{\partial x} + f_y = 0,\\
&\epsilon_x = \frac{\partial u}{\partial x}, \\
&\epsilon_y = \frac{\partial v}{\partial y}, \\
&\gamma_{xy} = \frac{\partial v}{\partial x} + \frac{\partial u}{\partial y},\\
&\varepsilon_x = \frac{1 - \mu^2}{E} \left( \sigma_x - \frac{\mu}{1 - \mu} \sigma_y \right), \\
&\varepsilon_y = \frac{1 - \mu^2}{E} \left( \sigma_y - \frac{\mu}{1 - \mu} \sigma_x \right), \\
&\gamma_{xy} = \frac{2(1 + \mu)}{E} \tau_{xy},
\end{aligned}
\end{equation}
$$ (sec6-eq:2D-strain-eq)

求解变量为

$$
\sigma_{x}, \, \sigma_{y}, \, \tau_{xy}, \, \epsilon_{x}, \, \epsilon_{y}, \, \gamma_{xy}, \, u, \, v
$$

```{note}
在平面应力问题的方程 {eq}`sec6-eq:2D-stress-physical` 中，如果将 $E$ 和 $\mu$ 分别替换为

$$
\frac{E}{1-\mu^2},\quad \frac{\mu}{1-\mu}
$$

就能够得到平面应变问题。如果已经得到平面应力问题的（解析）解，只需将 $E$ 和 $\mu$ 作同样的转换，就可以得到相应的平面应变问题的解
```
