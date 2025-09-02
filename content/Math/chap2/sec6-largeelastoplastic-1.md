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
\mathbf{n}\mathrm{d}S = J\mathbf{F}^{-T}\mathbf{N}\mathrm{d}S_{0}\quad \Longrightarrow\quad \mathrm{d}S = J\|\mathbf{F}^{-T}\mathbf{N}\|\mathrm{d}S_{0}
$$

**物理量变换**

将相关物理量转换到初始构型上

$$
\begin{equation}
\begin{aligned}
&\rho J = \rho_{0},\quad cJ=c_{0},\quad \mathbf{f}J = \mathbf{f}_{0},\\
&\alpha J\|\mathbf{F}^{-T}\mathbf{N}\|=\alpha_{0},\\
&\tilde{\mathbf{p}} J\|\mathbf{F}^{-T}\mathbf{N}\|=\tilde{\mathbf{p}}_{0},\\
&\mathbf{F}_{R} J\|\mathbf{F}^{-T}\mathbf{N}\|=\mathbf{F}_{R_{0}},
\end{aligned}
\end{equation}
$$

于是

$$
\begin{equation}
\begin{aligned}
&\int_{\Omega}\rho\ddot{\mathbf{u}}\cdot\mathbf{v}\mathrm{d}V  = \int_{\Omega_{0}}\rho_{0}\ddot{\mathbf{u}}\cdot\mathbf{v}\mathrm{d}V_{0},\\
&\int_{\Omega}c\dot{\mathbf{u}}\cdot\mathbf{v} \, \mathrm{d}V=\int_{\Omega_{0}}c_{0}\dot{\mathbf{u}}\cdot\mathbf{v} \, \mathrm{d}V_{0},\\
&\int_{\Omega}\mathbf{f}\cdot\mathbf{v} \, \mathrm{d}V=\int_{\Omega_{0}}\mathbf{f}_{0}\cdot\mathbf{v} \, \mathrm{d}V_{0},\\
&\int_{\Gamma_{R}} \alpha\mathbf{u} \cdot \mathbf{v} \, \mathrm{d}S=\int_{\Gamma_{R_{0}}} \alpha_{0}\mathbf{u} \cdot \mathbf{v} \, \,\mathrm{d}S_{0},\\
&\int_{\Gamma_{N}} \tilde{\mathbf{p}} \cdot \mathbf{v} \, \mathrm{d}S=\int_{\Gamma_{N_{0}}} \tilde{\mathbf{p}}_{0} \cdot \mathbf{v} \, \,\mathrm{d}S_{0},\\
&\int_{\Gamma_{R}} \mathbf{f}_{R} \cdot \mathbf{v} \, \mathrm{d}S=\int_{\Gamma_{R_{0}}} \mathbf{f}_{R_{0}} \cdot \mathbf{v}\,\mathrm{d}S_{0},\\
&\int_{\Omega} \boldsymbol{\varepsilon}(\mathbf{v}) : \boldsymbol{\sigma} \, \mathrm{d}V = \int_{\Omega_{0}} \delta\mathbf{E}:\mathbf{S} \, \mathrm{d}V_{0}.
\end{aligned}
\end{equation}
$$

:::{admonition} $\int_{\Omega} \boldsymbol{\varepsilon}(\mathbf{v}) : \boldsymbol{\sigma} \, \mathrm{d}V = \int_{\Omega_{0}} \delta\mathbf{E}:\mathbf{S} \, \mathrm{d}V_{0}$
:class: tip, dropdown

由于 

$$
\begin{equation}
\begin{aligned}
\boldsymbol{\varepsilon}(\mathbf{v}) &= \frac{1}{2}\left(\nabla_{x}\mathbf{v} + \nabla_{x}\mathbf{v}^{T}\right)\\
&=\frac{1}{2}\left(\nabla_{X}\mathbf{v}\mathbf{F}^{-1} + \mathbf{F}^{-T}\nabla_{X}\mathbf{v}^{T}\right)
\end{aligned}
\end{equation}
$$

故

$$
\boldsymbol{\varepsilon}(\mathbf{v}) : \boldsymbol{\sigma} = \frac{1}{2}\left(\nabla_{X}\mathbf{v}\mathbf{F}^{-1} + \mathbf{F}^{-T}\nabla_{X}\mathbf{v}^{T}\right) : J^{-1}\mathbf{F}\mathbf{S}\mathbf{F}^{T},
$$

由于 $A:B = \text{tr}(A^{T}B)$，第一项

$$
\begin{equation}
\begin{aligned}
\nabla_{X}\mathbf{v}\mathbf{F}^{-1}:(\mathbf{F}\mathbf{S}\mathbf{F}^{T})
&=\text{tr}(F^{-T}\nabla_{X}\mathbf{v}^{T}\mathbf{F}\mathbf{S}\mathbf{F}^{T})\\
&=\text{tr}(\nabla_{X}\mathbf{v}^{T}\mathbf{F}\mathbf{S})\\
&=\text{tr}((\mathbf{F}^{T}\nabla_{X}\mathbf{v})^{T}\mathbf{S})\\
&=\mathbf{F}^{T}\nabla_{X}\mathbf{v}:\mathbf{S},
\end{aligned}
\end{equation}
$$

类似地，第二项

$$
\begin{equation}
\begin{aligned}
\mathbf{F}^{-T}\nabla_{X}\mathbf{v}^{T}:(\mathbf{F}\mathbf{S}\mathbf{F}^{T})
&=\text{tr}(\nabla_{X}\mathbf{v}\mathbf{F}^{-1}\mathbf{F}\mathbf{S}\mathbf{F}^{T})\\
&=\text{tr}(\nabla_{X}\mathbf{v}\mathbf{S}\mathbf{F}^{T})\\
&=\text{tr}(\mathbf{F}^{T}\nabla_{X}\mathbf{v}\mathbf{S})\\
&=(\mathbf{F}^{T}\nabla_{X}\mathbf{v})^{T}:\mathbf{S},
\end{aligned}
\end{equation}
$$

于是

$$
\boldsymbol{\varepsilon}(\mathbf{v}) : \boldsymbol{\sigma} = \frac{J^{-1}}{2}\left(\mathbf{F}^{T}\nabla_{X}\mathbf{v}+(\mathbf{F}^{T}\nabla_{X}\mathbf{v})^{T}\right):\mathbf{S},
$$


$\delta(\cdot)$ 是变分算子，是一种“广义微分”，描述对象在某种扰动下的一阶变化，例如：对于泛函 $J[u]$，其在函数 $u(x)$ 沿方向 $\eta(x)$ 的变分定义为 $\delta J[u;\eta]=\frac{\mathrm{d}}{\mathrm{d}\epsilon}J[u+\epsilon\eta]\big|_{\epsilon=0}$，变分类似于“函数空间中的方向导数”，是泛函对函数变化的敏感性描述

另一方面，由于

$$
\delta\mathbf{F} = \delta\frac{\partial \mathbf{x}}{\partial \mathbf{X}} =  \frac{\mathrm{d}}{\mathrm{d}\epsilon}\frac{\partial(\mathbf{x}+\epsilon\mathbf{v})}{\partial \mathbf{X}} = \nabla_{X}\mathbf{v},
$$

故

$$
\begin{equation}
\begin{aligned}
\mathbf{E} = \frac{1}{2}\left(\mathbf{F}^{T}\mathbf{F}-\mathbf{I}\right)\quad\Longrightarrow\quad
\delta\mathbf{E}&=\frac{1}{2}\left((\delta\mathbf{F}^{T})\mathbf{F} + \mathbf{F}^{T}(\delta\mathbf{F})\right)\\
&=\frac{1}{2}\left(\nabla_{X}\mathbf{v}^{T}\mathbf{F}+\mathbf{F}^{T}\nabla_{X}\mathbf{v}\right),
\end{aligned}
\end{equation}
$$

于是

$$
\int_{\Omega} \boldsymbol{\varepsilon}(\mathbf{v}) : \boldsymbol{\sigma} \, \mathrm{d}V = \int_{\Omega_{0}} \delta\mathbf{E}:\mathbf{S} \, \mathrm{d}V_{0}.
$$
:::

最终，合并所有的式子，得到初始构型上的弱形式

$$
\begin{equation}
\begin{aligned}
&\int_{\Omega_{0}}\rho_{0}\ddot{\mathbf{u}}\cdot\mathbf{v}\mathrm{d}V_{0}
+\int_{\Omega_{0}}c_{0}\dot{\mathbf{u}}\cdot\mathbf{v} \, \mathrm{d}V_{0}
+\int_{\Omega_{0}} \delta\mathbf{E}:\mathbf{S} \, \mathrm{d}V_{0}
+\int_{\Gamma_{R_{0}}} \alpha_{0}\mathbf{u} \cdot \mathbf{v} \, \,\mathrm{d}S_{0} \\
&=\int_{\Omega_{0}}\mathbf{f}_{0}\cdot\mathbf{v} \, \mathrm{d}V_{0}
+\int_{\Gamma_{N_{0}}} \tilde{\mathbf{p}}_{0} \cdot \mathbf{v} \, \,\mathrm{d}S_{0}+\int_{\Gamma_{R_{0}}} \mathbf{f}_{R_{0}} \cdot \mathbf{v} \,\mathrm{d}S_{0},\quad \forall \, \mathbf{v} \in \, \mathcal{V},
\end{aligned}
\end{equation}
$$

## 有限元离散形式

### 空间离散

由于

$$
\mathbf{F} = \frac{\partial (\mathbf{X} + \mathbf{u})}{\partial \mathbf{X}} = \mathbf{I} + \nabla_{X}\mathbf{u},
$$

故

$$
\begin{equation}
\begin{aligned}
\delta\mathbf{E}&=\frac{1}{2}\left(\nabla_{X}\mathbf{v}_{*,i}^{T}\mathbf{F}+\mathbf{F}^{T}\nabla_{X}\mathbf{v}_{*,i}\right),\\
&=\frac{1}{2}\left(\nabla_{X}\mathbf{v}_{*,i} + \nabla_{X}\mathbf{v}_{*,i}^{T}\right) + \frac{1}{2}\left(\nabla_{X}\mathbf{v}_{*,i}^{T}\nabla_{X}\mathbf{u} + \nabla_{X}\mathbf{u}^{T}\nabla_{X}\mathbf{v}_{*,i}\right),\\
&\qquad\qquad\qquad\qquad\qquad\qquad \forall \, \mathbf{v}_{*,i} \in \, \mathcal{V},\quad *=x,y,z;\ i=1:N.
\end{aligned}
\end{equation}
$$

由于

$$
\mathbf{u} = \mathbf{N}\mathbf{u}_{E},
$$

故

$$
\nabla_{X}\mathbf{u} =  \mathbf{B}_{L}\mathbf{u}_{E},
$$

对于全体 $\mathbf{v}_{*,i}$，写作矩阵形式，得到

$$
\nabla_{X}\mathbf{v}_{*,i} = \mathbf{B}_{L}
$$