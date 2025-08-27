# 大变形弹塑性问题（静力学）

相较于小变形弹塑性问题，大变形弹塑性问题通常伴随着显著的刚体转动。旋转会破坏应力和应变的物理客观性，因此在理论和数值分析中，必须将变形与旋转进行有效解耦，才能准确描述材料的力学行为。目前主要存在两种主流求解思路：

- **参考构型法（拉格朗日描述）**：  
  在小变形分析中，通常假定初始构型与当前构型几乎一致，可采用线性应变和 Cauchy 应力进行描述；而在大变形分析中，需建立初始构型与当前构型之间的映射关系，采用**变形梯度**、**格林-拉格朗日应变**以及**第二类 Piola-Kirchhoff 应力**等张量来刻画材料的力学状态。该方法所有变量均以**参考构型**为基础，便于处理大变形下的物理量，广泛用在**隐式求解**中

- **客观应力率法（欧拉描述）**：  
  在大变形分析中，由于可能存在显著的刚体转动，需引入**客观应力率**（如 Jaumann 应力率等），以确保应力率的物理合理性和客观性；而在小变形分析中，刚体转动影响甚微，通常无需考虑应力率的客观性修正。该方法所有变量均以**当前构型**为基础，适用于处理涉及大变形和复杂运动的力学问题，常用在**显式动力学**计算中

---

如需进一步扩展或补充，也可以随时告诉我！


## 求解方程

**运动关系**

$$
\mathbf{F} = \mathbf{I} + \nabla_{X}\mathbf{u},
$$

**平衡方程（动量守恒方程）：**

$$
\begin{equation}
\nabla_{x}\cdot \boldsymbol{\sigma} + \mathbf{f} = \mathbf{0},
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
\mathbf{S} = \frac{\partial \Psi(\mathbf{E}^{e})}{\partial \mathbf{E}^{e}} = \mathbf{D} : \mathbf{E}^{e},
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