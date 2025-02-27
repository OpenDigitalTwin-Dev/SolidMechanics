# 位移法和应力法

[](./sec6-two-2D.md)讨论了两类平面问题，即平面应力问题 {eq}`sec6-eq:2D-stress-physical` 和平面应变问题 {eq}`sec6-eq:2D-strain-physical`。这些问题的求解过程涉及多个方程与变量的联立求解，具有较高的复杂性，常常采用**消元法**对其进行求解，主要分为两类方法：

1. **位移法**：以位移分量为基本未知量，消去应力和应变分量，导出仅含位移的方程进行求解
2. **应力法**：以应力分量为基本未知量，消去应变和位移分量，导出仅含应力的方程进行求解

## 位移法

对于**平面应力问题**，在 {eq}`sec6-eq:2D-stress-physical` 中反解出应力

$$
\begin{equation}
\begin{aligned}
\sigma_x &= \frac{E}{1 - \mu^2} \left( \varepsilon_x + \mu \varepsilon_y \right), \\
\sigma_y &= \frac{E}{1 - \mu^2} \left( \varepsilon_y + \mu \varepsilon_x \right), \\
\tau_{xy} &= \frac{E}{2(1 + \mu)} \gamma_{xy},
\end{aligned}
\end{equation}
$$

将几何方程 {eq}`sec4-eq:geometry` 代入到式

$$
\begin{equation}
\begin{aligned}
\sigma_x &= \frac{E}{1 - \mu^2} \left( \frac{\partial u}{\partial x} + \mu \frac{\partial v}{\partial y} \right), \\
\sigma_y &= \frac{E}{1 - \mu^2} \left( \frac{\partial v}{\partial y} + \mu \frac{\partial u}{\partial x} \right), \\
\tau_{xy} &= \frac{E}{2(1 + \mu)} \left( \frac{\partial v}{\partial x} + \frac{\partial u}{\partial y} \right),
\end{aligned}
\end{equation}
$$ (sec8-eq:stress-displ)

将上式代入到平衡方程 {eq}`sec3-eq:balance`，整理得到

```{margin}
将 $E$ 和 $\mu$ 分别替换成 $\frac{E}{1-\mu^2}$ 和 $\frac{\mu}{1-\mu}$ 就能够得到平面应变问题按位移求解的方程
```

$$
\begin{equation}
\begin{aligned}
\frac{E}{1 - \mu^2} \bigg(
\frac{\partial^2 u}{\partial x^2}
+\frac{1 - \mu}{2} \frac{\partial^2 u}{\partial y^2}
+\frac{1 + \mu}{2} \frac{\partial^2 v}{\partial x \partial y}
\bigg) + f_x &= 0, \\
\frac{E}{1 - \mu^2} \bigg(
\frac{\partial^2 v}{\partial y^2}
+\frac{1 - \mu}{2} \frac{\partial^2 v}{\partial x^2}
+\frac{1 + \mu}{2} \frac{\partial^2 u}{\partial x \partial y}
\bigg) + f_y &= 0.
\end{aligned}
\end{equation}
$$ (sec8-eq:solution-displ)

在应变法中，应变被作为基本未知量。
在物理方程 {eq}`sec5-eq:strain-stress-1` 中，应变与应力呈线性关系，因此可以通过应变轻松表示应力。进一步结合几何方程 {eq}`sec4-eq:geometry`，应力可以方便地用位移表示，如方程 {eq}`sec8-eq:stress-displ` 所示。这种特性使得位移法能够**灵活地适应各种边界问题的求解**，无论是位移边界条件、应力边界条件，还是二者的组合

## 相容方程

据几何方程 {eq}`sec4-eq:geometry`，可以推导出**相容方程**

```{margin}
也称 **形变协调方程**
```

$$
\frac{\partial^2 \varepsilon_x}{\partial y^2} + \frac{\partial^2 \varepsilon_y}{\partial x^2}
= \frac{\partial^3 u}{\partial x \partial y^2} + \frac{\partial^3 v}{\partial y \partial x^2}
= \frac{\partial^2}{\partial x \partial y} \left( \frac{\partial u}{\partial y} + \frac{\partial v}{\partial x} \right)= \frac{\partial^2 \gamma_{xy}}{\partial x \partial y},
$$ (sec8-eq:compatibility)

相容方程表明，连续体的应变分量 $\epsilon_x, \epsilon_y, \gamma_{xy}$ 不是相互独立的

## 应力法

对于**平面应力问题**，将物理方程 {eq}`sec6-eq:2D-stress-physical` 代入到方程 {eq}`sec8-eq:compatibility` 中，得到

```{margin}
方程中仅保留了 $\mu$
```

$$
\frac{\partial^2}{\partial y^2} (\sigma_x - \mu \sigma_y) + \frac{\partial^2}{\partial x^2} (\sigma_y - \mu \sigma_x) = 2(1 + \mu) \frac{\partial^2 \tau_{xy}}{\partial x \partial y}.
$$ (sec8-eq:stress-1)

联立平衡方程 {eq}`sec3-eq:balance`，共三个方程和三个求解变量：$\sigma_{x},\sigma_{y},\tau_{xy}$

代入平衡方程可得

```{margin}
切应力互等定理
```

$$
\begin{equation}
\begin{aligned}
2\frac{\partial^2 \tau_{xy}}{\partial x \partial y} &= \frac{\partial}{\partial y}\left(\frac{\partial \tau_{xy}}{\partial x}\right) + \frac{\partial}{\partial x}\left(\frac{\partial \tau_{yx}}{\partial y}\right)\\
&=  -\frac{\partial}{\partial y}\left(\frac{\partial \sigma_{y}}{\partial y} + f_y\right) - \frac{\partial}{\partial x}\left(\frac{\partial \sigma_{x}}{\partial x} + f_y\right)\\
&=-\frac{\partial^2 \sigma_x}{\partial x^2} - \frac{\partial^2 \sigma_y}{\partial y^2} - \frac{\partial f_x}{\partial x} - \frac{\partial f_y}{\partial y},
\end{aligned}
\end{equation}
$$

将上式代入到方程 {eq}`sec8-eq:stress-1`，得到应力表示的相容方程

```{margin}
将 $\mu$ 替换成 $\frac{\mu}{1-\mu}$ 就能够得到平面应变问题按应力求解的方程
```

$$
\left( \frac{\partial^2}{\partial x^2} + \frac{\partial^2}{\partial y^2} \right) (\sigma_x + \sigma_y) = - (1 + \mu) \left( \frac{\partial f_x}{\partial x} + \frac{\partial f_y}{\partial y} \right).
$$ (sec8-eq:solution-stress-1)

在应力法中，应力作为基本未知量，通过物理方程 {eq}`sec5-eq:strain-stress-1` 表示应变，并结合几何方程 {eq}`sec4-eq:geometry` 间接表示位移；然而，几何方程是一个微分方程组，求解过程较为复杂，这使得通过应力表示位移变得困难。因此，应力法通常仅适用于**边界条件全部为应力边界条件**的问题

### 常体积力的情况

在许多情况下，体积力是常量，例如重力或在恒定加速度下的惯性力。此时，按应力求解得到的方程组如下

```{margin}
$\sigma_x + \sigma_y$ 是调和函数
```

$$
\begin{equation}
\begin{aligned}
&\frac{\partial \sigma_x}{\partial x} + \frac{\partial \tau_{yx}}{\partial y} + f_x = 0, \\
&\frac{\partial \sigma_y}{\partial y} + \frac{\partial \tau_{xy}}{\partial x} + f_y = 0,\\
&\left( \frac{\partial^2}{\partial x^2} + \frac{\partial^2}{\partial y^2} \right) (\sigma_x + \sigma_y) = 0.
\end{aligned}
\end{equation}
$$ (sec8-eq:solution-stress-2)

方程中不包含任何弹性体的材料参数，如 $E$、$G$、$\mu$

```{margin}
针对平面应力问题或平面应变问题
```

这表明，当体积力为常量时，如果两个弹性体**具有相同边界形状和应力边界条件**，那么无论这两个弹性体的材料性质是否相同，也无论它们处于平面应力还是平面应变状态，其**应力的分布都将完全一致**

```{admonition} Example
:class: dropdown
在实验应力分析中：
1. 用便于测量的材料制成模型，替代原本不便于测量的结构材料
2. 用平面应力条件下的薄板模型替代平面应变条件下的长柱形结构
```

```{seealso}
:class: dropdown
应力方程 {eq}`sec8-eq:solution-stress-2` 的求解：

首先考虑平衡方程的求解，非齐次微分方程组的解由任意一个特解与齐次方程的通解相加组成，特解可以取为

$$
\sigma_x = -f_x \, x, \quad \sigma_y = -f_y \, y, \quad \tau_{xy} = 0.
$$

对于其齐次形式

$$
\begin{equation}
\begin{aligned}
&\frac{\partial \sigma_x}{\partial x} + \frac{\partial \tau_{yx}}{\partial y} = 0, \\
&\frac{\partial \sigma_y}{\partial y} + \frac{\partial \tau_{xy}}{\partial x} = 0,
\end{aligned}
\end{equation}
$$

由于

$$
\begin{equation}
\begin{aligned}
\frac{\partial \sigma_x}{\partial x} = \frac{\partial }{\partial y} (-\tau_{yx}),\\
\frac{\partial \sigma_y}{\partial y} = \frac{\partial }{\partial x} (-\tau_{xy}),
\end{aligned}
\end{equation}
$$

所以存在 $A$ 和 $B$ 使得

$$
\begin{equation}
\begin{aligned}
\sigma_x = \frac{\partial A}{\partial y},\quad  -\tau_{yx} = \frac{\partial A}{\partial x},\\
\sigma_y = \frac{\partial B}{\partial x},\quad  -\tau_{xy} = \frac{\partial B}{\partial y},\\
\end{aligned}
\end{equation}
$$

进一步地，存在 $\Phi$ 满足

$$
A = \frac{\partial \Phi}{\partial y},\quad B = \frac{\partial \Phi}{\partial x},
$$

因此

$$
\sigma_x = \frac{\partial^2 \Phi}{\partial y^2}, \quad 
\sigma_y = \frac{\partial^2 \Phi}{\partial x^2}, \quad 
\tau_{xy} = -\frac{\partial^2 \Phi}{\partial x \partial y},
$$

其中 $\Phi$ 称为平面问题的**应力函数**，又称**艾里应力函数**，通过 $\Phi$ 可以表示出 $\sigma_x,\sigma_y,\tau_{xy}$。将上式代入到方程 {eq}`sec8-eq:solution-stress-2` 的第三式中，整理得到

$$
\frac{\partial^4 \Phi}{\partial x^4} 
+ 2 \frac{\partial^4 \Phi}{\partial x^2 \partial y^2} 
+ \frac{\partial^4 \Phi}{\partial y^4} = 0,
$$

这表明应力函数满足重调和方程，是**重调和函数**
```
