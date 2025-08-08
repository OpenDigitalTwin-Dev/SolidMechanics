# 小变形弹塑性问题

在涉及塑性变形的问题中，除了需要考虑基本的力学方程外，还需引入屈服准则、流动法则和硬化法则，因此其数学模型更加复杂。此处考虑**小变形、小旋转**的弹塑性问题

## 求解方程

**平衡方程（动量守恒方程）：**

$$
\begin{equation}
\nabla\cdot \boldsymbol{\sigma} + \mathbf{f} = \rho\mathbf{a},
\end{equation}
$$

在静力学求解中，假定加速度 $\mathbf{a} = \mathbf{0}$

**几何方程**

$$
\begin{equation}
\boldsymbol{\varepsilon} = \frac{1}{2}(\nabla \mathbf{u} + \nabla\mathbf{u}^{T}),
\end{equation}
$$

**应变分解**

$$
\begin{equation}
\boldsymbol{\varepsilon} = \boldsymbol{\varepsilon}^e + \boldsymbol{\varepsilon}^p，
\end{equation}
$$

**弹塑性本构关系**

$$
\begin{equation}
\boldsymbol{\sigma} = \mathbf{D} : \boldsymbol{\varepsilon}^e = \mathbf{D} : (\boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}^p)，
\end{equation}
$$

**屈服函数**

以经典的 [Mises 准则](../../Plasticity/chap2/sec2-mises.md) 为例

$$
\begin{equation}
f(\boldsymbol{\sigma}, \bar{\varepsilon}^p) = \sqrt{\frac{3}{2} \mathbf{s} : \mathbf{s}} - \sigma_y(\bar{\varepsilon}^p)，
\end{equation}
$$

其中，$\sigma_y(\bar{\varepsilon}^p)$ 是屈服应力，$\bar{\varepsilon}^p$ 是[等效塑性应变](../../Plasticity/chap1/sec2-uniaxial.md)，基于各向同性的 Mises 准则，其通常定义为

$$
\begin{equation}
\dot{\bar{\varepsilon}}^{p} = \sqrt{\frac{2}{3} \dot{\boldsymbol{\varepsilon}}^p : \dot{\boldsymbol{\varepsilon}}^p}.
\end{equation}
$$


**流动法则**

$$
\begin{equation}
\dot{\boldsymbol{\varepsilon}}^p = \dot{\gamma} \frac{\partial f}{\partial \boldsymbol{\sigma}}，
\end{equation}
$$

其中，$\dot{\gamma}$ 是[塑性乘子](../../Plasticity/chap3/intro.md)

**硬化法则**

若初始屈服应力为 $\sigma_{y}^{0}$，对于线性硬化，则有

$$
\begin{equation}
\sigma_y(\bar{\varepsilon}^p) = \sigma_{y}^{0} + H\bar{\varepsilon}^p,
\end{equation}
$$

其中，$H$ 是硬化模量

**塑性加载/卸载条件**

也称 Kuhn-Tucker 条件

$$
\begin{equation}
f \leq 0, \quad \dot{\gamma} \geq 0, \quad \dot{\gamma} f = 0,
\end{equation}
$$

当

- $f<0$，则处于弹性状态，此时 $\dot{\gamma} = 0$
- $f=0$，则材料可能屈服，此时 $\dot{\gamma} \geq 0$

当 $\dot{\gamma} > 0$ 时，有 $f\equiv0$，因此

$$
\begin{equation}
  \dot{f} = \frac{\partial f}{\partial \boldsymbol{\sigma}} : \dot{\boldsymbol{\sigma}} + \frac{\partial f}{\partial \bar{\varepsilon}^p} \dot{\bar{\varepsilon}}^p = 0,
\end{equation}
$$

即塑性流动始终发生在屈服面上，这也是塑性流动的**一致性条件**

**边界条件**

以及用来描述边界载荷的三类边界条件

$$
\begin{equation}
\begin{aligned}
\mathbf{u} &= \tilde{\mathbf{u}},\quad &\text{on}\,\, \Gamma_{D},\\
\boldsymbol{\sigma}\mathbf{n} &= \tilde{\mathbf{p}},\quad &\text{on}\,\, \Gamma_{N},\\
\boldsymbol{\sigma}\mathbf{n} + \alpha\mathbf{u} &= \mathbf{f}_{R},\quad &\text{on}\,\, \Gamma_{R}.
\end{aligned}
\end{equation}
$$

## 有限元求解