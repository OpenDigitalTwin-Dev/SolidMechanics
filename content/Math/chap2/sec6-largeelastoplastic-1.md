# 大变形弹塑性问题-参考构型法

参考构型法是一种以材料初始状态为基准进行力学分析的方法，常用于大变形问题。该方法通过建立初始构型与当前构型之间的映射关系，利用变形梯度、格林-拉格朗日应变和第二类 Piola-Kirchhoff 应力等张量，在参考构型下描述材料的应力和应变，能够有效处理大变形过程中的力学行为，保证理论的物理一致性

## 求解方程

**运动关系**

变形梯度矩阵

$$
\mathbf{F} = \frac{\partial \mathbf{x}}{\partial \mathbf{X}} = \mathbf{I} + \nabla_{X}\mathbf{u},
$$

**平衡方程（动量守恒方程）：**

$$
\begin{equation}
\nabla_{x}\cdot \boldsymbol{\sigma} + \mathbf{f} = \rho\ddot{\mathbf{u}} + c\dot{\mathbf{u}},
\end{equation}
$$

其中

$$
\boldsymbol{\sigma} = J^{-1}\mathbf{F}\mathbf{S}\mathbf{F}^{T},
$$

$\mathbf{S}$ 是 PK2 应力

**几何方程**

$$
\mathbf{E} = \frac{1}{2}(\mathbf{F}^{T}\mathbf{F}-\mathbf{I}), 
$$

**应变分解**

$$
\mathbf{F}=\mathbf{F}^{e}\mathbf{F}^{p},
$$

**弹塑性本构关系**

$$
\mathbf{S} = \frac{\partial \Psi(\mathbf{E}^{e})}{\partial \mathbf{E}^{e}} = \mathbb{C} : \mathbf{E}^{e},
$$

其中，$\mathbf{E}^{e} = \frac{1}{2}(\mathbf{F}^{eT}\mathbf{F}^{e}-\mathbf{I})$

**屈服准则**

例如，对于经典的 [Mises 准则](../../Plasticity/chap2/sec2-mises.md)

$$
\begin{equation}
f(\mathbf{S}, \bar{\varepsilon}^p) = \sqrt{\frac{3}{2} \mathbf{S}' : \mathbf{S}'} - \sigma_y(\bar{\varepsilon}^p)，
\end{equation}
$$

等效塑性应变通常定义为

$$
\begin{equation}
\dot{\bar{\varepsilon}}^{p} = \sqrt{\frac{2}{3} \dot{\mathbf{E}}^p : \dot{\mathbf{E}}^p}=\dot{\gamma}.
\end{equation}
$$

**塑性流动法则**

例如，考虑关联性流动法则

$$
\dot{\mathbf{E}}^{p}=\dot{\gamma}\frac{\partial f}{\partial \mathbf{S}},
$$

**硬化规律**

例如，对于线性硬化

$$
\begin{equation}
\sigma_y(\bar{\varepsilon}^p) = \sigma_{y0} + H\bar{\varepsilon}^{p},
\end{equation}
$$

其中，$\sigma_{y0}$ 是初始屈服强度，$H$ 是硬化模量

**Kuhn-Tucker 条件**

$$
\begin{equation}
f(\mathbf{S}) \leq 0, \quad \dot{\gamma} \geq 0, \quad \dot{\gamma} f(\mathbf{S}) = 0,
\end{equation}
$$

**边界条件**

描述边界载荷的三类边界条件，它们定义在当前构型上

$$
\begin{equation}
\begin{aligned}
\mathbf{u} &= \tilde{\mathbf{u}},\quad &\text{on}\,\, \Gamma_{D},\\
\boldsymbol{\sigma}\mathbf{n} &= \tilde{\mathbf{p}},\quad &\text{on}\,\, \Gamma_{N},\\
\boldsymbol{\sigma}\mathbf{n} + \alpha\mathbf{u} &= \mathbf{f}_{R},\quad &\text{on}\,\, \Gamma_{R}.
\end{aligned}
\end{equation}
$$

**初始条件**

$$
\mathbf{u}(\mathbf{x},0) = \mathbf{u}_{0}(\mathbf{x}),\quad \dot{\mathbf{u}}(\mathbf{x},0) = \dot{\mathbf{u}_{0}}(\mathbf{x}).
$$

## 有限元弱形式

有限元弱形式为

$$
\begin{equation}
\begin{aligned}
\int_{\Omega}\rho\ddot{\mathbf{u}}\cdot\mathbf{v} \, \mathrm{d}V +\int_{\Omega}c\dot{\mathbf{u}}\cdot\mathbf{v} \, \mathrm{d}V 
+\int_{\Omega} \boldsymbol{\varepsilon}(\mathbf{v}) : \boldsymbol{\sigma} \, \mathrm{d}V 
+\int_{\Gamma_{R}} \alpha\mathbf{u} \cdot \mathbf{v} \, \mathrm{d}S\\
= \int_{\Omega}\mathbf{f}\cdot \mathbf{v}\,\mathrm{d}V + \int_{\Gamma_{N}} \tilde{\mathbf{p}} \cdot \mathbf{v} \, \mathrm{d}S + \int_{\Gamma_{R}} \mathbf{f}_{R} \cdot \mathbf{v} \, \mathrm{d}S,\quad \forall \, \mathbf{v} \in \, \mathcal{V},
\end{aligned}
\end{equation}
$$

其中，$\mathbf{v}\in\mathcal{V}$ 是试验函数，$\mathbf{u} = \mathbf{\tilde{u}},\, \text{on}\, \Gamma_{D}$

上式中，积分在当前构型 $\Omega$（未知）中进行，将其转换到初始构型 $\Omega_{0}$

**体元转换**

$$
\mathrm{d}V = J\mathrm{d}V_{0},
$$

**面元转换**

$$
\mathbf{n}\mathrm{d}A = J\mathbf{F}^{-T}\mathbf{N}\mathrm{d}A_{0},
$$

于是

$$
\begin{equation}
\begin{aligned}
&\int_{\Omega}\rho\ddot{\mathbf{u}}\cdot\mathbf{v}\mathrm{d}V  = \int_{\Omega_{0}}\rho\ddot{\mathbf{u}}\cdot\mathbf{v}J\mathrm{d}V_{0},\\
&\int_{\Omega}c\dot{\mathbf{u}}\cdot\mathbf{v} \, \mathrm{d}V=\int_{\Omega_{0}}c\dot{\mathbf{u}}\cdot\mathbf{v}J \, \mathrm{d}V_{0},
\end{aligned}
\end{equation}
$$

由于

$$

$$

$$
\int_{\Omega} \boldsymbol{\varepsilon}(\mathbf{v}) : \boldsymbol{\sigma} \, \mathrm{d}V = \int_{\Omega_{0}} \boldsymbol{\varepsilon}(\mathbf{v}) : J^{-1}\mathbf{F}\mathbf{S}\mathbf{F}^{T}J \, \mathrm{d}V_{0} = \int_{\Omega_{0}} \boldsymbol{\varepsilon}(\mathbf{v}) : \mathbf{F}\mathbf{S}\mathbf{F}^{T} \, \mathrm{d}V_{0}
$$
