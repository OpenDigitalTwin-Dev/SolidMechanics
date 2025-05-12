# 速度梯度场

<span class="gray-text">
速度梯度场描述了材料内部速度场的空间变化，反映了各部分之间的相对运动，是研究材料变形和流动的基础
</span>

速度向量表示为

$$
\mathbf{v} = \dot{\mathbf{u}}(t) = \dot{\mathbf{x}}(t) = \frac{\partial \mathbf{x}}{\partial t} \in \mathbb{R}^{3},
$$

速度梯度场定义为

$$
L = \nabla\mathbf{v} = \frac{\partial \mathbf{v}}{\partial \mathbf{x}} = \begin{bmatrix}
\frac{\partial v_{1}}{\partial x_{1}} & \frac{\partial v_{1}}{\partial x_{2}} & \frac{\partial v_{1}}{\partial x_{3}} \\
\frac{\partial v_{2}}{\partial x_{1}} & \frac{\partial v_{2}}{\partial x_{2}} & \frac{\partial v_{2}}{\partial x_{3}} \\
\frac{\partial v_{3}}{\partial x_{1}} & \frac{\partial v_{3}}{\partial x_{2}} & \frac{\partial v_{3}}{\partial x_{3}}
\end{bmatrix},
$$

显然有

$$
\text{tr}(\nabla\mathbf{v}) = \nabla\cdot\mathbf{v}.
$$

根据定义，速度梯度场还可以表示为

$$
L = \nabla\mathbf{v} = \frac{\partial \mathbf{v}}{\partial \mathbf{x}} = \frac{\partial \mathbf{v}}{\partial \mathbf{X}}\frac{\partial \mathbf{X}}{\partial \mathbf{x}} = \frac{\partial^2 \mathbf{u}}{\partial \mathbf{X}\partial t}\frac{\partial \mathbf{X}}{\partial \mathbf{x}} = \dot{F}F^{-1}.
$$

## 速度梯度场分解

<span class="gray-text">
速度梯度场的分解将真实形变与刚体旋转有效区分，为客观描述奠定基础
</span>

将速度梯度分解为对称部分和反对称部分

$$
L = D + W,
$$

- $D = \frac{1}{2}(L+L^{T})$：应变率张量，描述材料的拉伸、压缩和剪切等变形速率

$$
D_{ij} = \frac{1}{2}\left(\frac{\partial v_{i}}{\partial x_{j}} + \frac{\partial v_{j}}{\partial x_{i}}\right)
$$

- $W = \frac{1}{2}(L-L^{T})$：旋转率张量，描述材料的刚体旋转速率

$$
W_{ij} = \frac{1}{2}\left(\frac{\partial v_{i}}{\partial x_{j}} - \frac{\partial v_{j}}{\partial x_{i}}\right)
$$


### 几何解释

在 [几何方程](../../Elasticity/chap1/sec4-geometry-equa.md) 中可以看到，位移梯度决定了应变，因此速度梯度场决定了物体的变形速率。以微元在 $xOy$ 平面上的剪切应变为例，考虑两种特殊情况：

$$
2\varepsilon_{xy} = \frac{\partial u_{x}}{\partial y} + \frac{\partial u_{y}}{\partial x},
$$

**1.** $\frac{\partial u_{x}}{\partial y} = \frac{\partial u_{y}}{\partial x}$

```{figure} ../../../images/Tensor/chap1/sym-shear-1.png
---
width: 300px
name: sec1-fig:sym-shear
---
对称剪切
```

如图，沿 $x$ 方向与沿 $y$ 方向的剪切应变等大反向，表现为**对称剪切变形**。此时，对称轴保持不动，剪切应变完全描述了物体的形变，无冗余信息

$$
L = D \neq 0,\quad W = 0.
$$

**2.** $\frac{\partial u_{x}}{\partial y} = - \frac{\partial u_{y}}{\partial x}$

```{figure} ../../../images/Tensor/chap1/rotation.png
---
width: 300px
name: sec1-fig:rotation
---
刚体旋转
```

如图，沿 $x$ 方向和 $y$ 方向的剪切应变等大同向，表现为**刚体旋转**。此时，剪切应变包含了刚体旋转的分量，不能准确反映物体的真实形变

$$
L = W, D = 0.
$$

综上，速度梯度（或位移梯度）场既包含形变（对称部分），也包含刚体旋转（反对称部分）。对于一般的速度（或位移）梯度，可以将其分解为对称剪切变形与刚体旋转的叠加

```{figure} ../../../images/Tensor/chap1/general.png
---
width: 600px
name: sec1-fig:general-shear
---
一般形变的分解
```

于是，$D$（对称部分-对称剪切）描述了微元的真实形变，包括剪切和体积变化；$W$ （反对称部分-垂直方向的剪切差异）描述了微元的局部刚体旋转

**通过对速度梯度场的分解，可以有效剔除刚体旋转的影响，使应力率等物理量在不同参考系下保持客观性，从而为大变形下本构关系的建立提供理论基础**

### 极分解

对 $F$ 进行极分解

$$
F = QU,
$$

其中，$Q$ 是正交矩阵（旋转变换矩阵），$U$ 是对称正定矩阵，于是

$$
L = (\dot{Q}U+Q\dot{U})U^{-1}Q^{T} = \dot{Q}Q^{T} + Q\dot{U}U^{-1}Q^{T}
$$

由于 $\dot{Q}Q^{T} + Q\dot{Q}^{T} = 0$，故

$$
\begin{equation}
\begin{aligned}
D = \frac{1}{2}(L+L^{T})&=\frac{1}{2}(Q\dot{U}U^{-1}Q^{T} + QU^{-1}\dot{U}Q^{T})\\
&=\frac{1}{2}Q(\dot{U}U^{-1}Q^{T} + QU^{-1}\dot{U})Q^{T},
\end{aligned}
\end{equation}
$$

以及

$$
\begin{equation}
\begin{aligned}
W = L - D = \frac{1}{2}Q(\dot{U}U^{-1}Q^{T} - QU^{-1}\dot{U})Q^{T} + \dot{Q}Q^{T}.
\end{aligned}
\end{equation}
$$

### 刚体旋转

对于刚体旋转变换，有

$$
U = I,
$$

此时

$$
D = 0,
$$

以及

$$
W = L = \dot{Q}Q^{T} = -Q\dot{Q}^{T}.
$$

### 局部体积变化速率

记 $J= \det(F)$，则

$$
\dot{J} = J\ \text{tr}(\dot{F}F^{-1}) = J\ \text{tr}(\nabla\mathbf{v}) = J\ (\nabla\cdot\mathbf{v}),
$$

该公式表明，**单位体积的变化速率 $\dot{J}$，等于体积本身 $J$ 乘以速度梯度场张量的迹（速度场的散度）**

对于等容行为，有

$$
J = 1 \Rightarrow \dot{J} = 1 \Rightarrow \text{tr}(\nabla\mathbf{v}) = \nabla\cdot\mathbf{v} = 0.
$$

:::{admonition} 证明一
:class: tip, dropdown


$$
J = \det(F) = \sum_{i,j,k=1}^{3}\varepsilon_{ijk}\frac{\partial x_{1}}{\partial X_{i}}\frac{\partial x_{2}}{\partial X_{j}}\frac{\partial x_{3}}{\partial X_{k}},
$$

对 $t$ 求导

$$
\dot{J} =  \sum_{i,j,k=1}^{3}\varepsilon_{ijk}\left(\frac{\partial \dot{x}_{1}}{\partial X_{i}}\frac{\partial x_{2}}{\partial X_{j}}\frac{\partial x_{3}}{\partial X_{k}} + \frac{\partial x_{1}}{\partial X_{i}}\frac{\partial \dot{x}_{2}}{\partial X_{j}}\frac{\partial x_{3}}{\partial X_{k}} + \frac{\partial x_{1}}{\partial X_{i}}\frac{\partial x_{2}}{\partial X_{j}}\frac{\partial \dot{x}_{3}}{\partial X_{k}}\right),
$$

代入

$$
\frac{\partial \dot{x}_{k}}{\partial X_{l}} = \sum_{i=1}^{3}\frac{\partial \dot{x}_{k}}{\partial x_{i}}\frac{\partial x_{i}}{\partial X_{l}},
$$

由于

$$
\sum_{i,j,k=1}^{3} \varepsilon_{ijk} 
\frac{\partial x_a}{\partial X_i}
\frac{\partial x_a}{\partial X_j}
\frac{\partial x_b}{\partial X_k}
=
\sum_{i,j,k=1}^{3} \varepsilon_{ijk} 
\frac{\partial x_b}{\partial X_i}
\frac{\partial x_b}{\partial X_j}
\frac{\partial x_a}{\partial X_k}
=
\sum_{i,j,k=1}^{3} \varepsilon_{ijk} 
\frac{\partial x_a}{\partial X_i}
\frac{\partial x_b}{\partial X_j}
\frac{\partial x_a}{\partial X_k}
=0,
$$

于是

$$
\dot{J} = \sum_{i,j,k=1}^{3} \varepsilon_{ijk} \left(
\frac{\partial \dot{x}_1}{\partial x_1} \frac{\partial x_1}{\partial X_i} \frac{\partial x_2}{\partial X_j} \frac{\partial x_3}{\partial X_k}
+
\frac{\partial \dot{x}_2}{\partial x_2} \frac{\partial x_1}{\partial X_i} \frac{\partial x_2}{\partial X_j} \frac{\partial x_3}{\partial X_k}
+
\frac{\partial \dot{x}_3}{\partial x_3} \frac{\partial x_1}{\partial X_i} \frac{\partial x_2}{\partial X_j} \frac{\partial x_3}{\partial X_k}
\right),
$$

故

$$
\dot{J} = J\ \left(\frac{\partial \dot{x}_1}{\partial x_1} + \frac{\partial \dot{x}_2}{\partial x_2} + \frac{\partial \dot{x}_3}{\partial x_3}\right) = J\ \text{tr}(L).
$$

:::

:::{admonition} 证明二
:class: tip, dropdown

设 $\mathbf{a},\mathbf{b},\mathbf{c}\in\mathbb{R}^{3}$ 是三个线性无关的向量，则

$$
J = \det(F) = \frac{F\mathbf{a}\cdot(F\mathbf{b}\times F\mathbf{c})}{\mathbf{a}\cdot(\mathbf{b}\times \mathbf{c})}
=
\frac{\det\left(\begin{bmatrix}
F\mathbf{a}&F\mathbf{b}&F\mathbf{c}
\end{bmatrix}\right)}{
\det\left(\begin{bmatrix}
\mathbf{a}&\mathbf{b}&\mathbf{c}
\end{bmatrix}\right)
},
$$

于是

$$
\begin{equation}
\begin{aligned}
\dot{J} &= \frac{\dot{F}\mathbf{a} \cdot (F\mathbf{b} \times F\mathbf{c}) + F\mathbf{a} \cdot (\dot{F}\mathbf{b} \times F\mathbf{c}) + F\mathbf{a} \cdot (F\mathbf{b} \times \dot{F}\mathbf{c})}{\mathbf{a} \cdot (\mathbf{b} \times \mathbf{c})}\\
&=\frac{\dot{F}F^{-1}F\mathbf{a} \cdot (F\mathbf{b} \times F\mathbf{c}) + F\mathbf{a} \cdot (\dot{F}F^{-1}F\mathbf{b} \times F\mathbf{c}) + F\mathbf{a} \cdot (F\mathbf{b} \times \dot{F}F^{-1}F\mathbf{c})}{\mathbf{a} \cdot (\mathbf{b} \times \mathbf{c})}\\
&=\frac{\dot{F}F^{-1}F\mathbf{a} \cdot (F\mathbf{b} \times F\mathbf{c}) + F\mathbf{a} \cdot (\dot{F}F^{-1}F\mathbf{b} \times F\mathbf{c}) + F\mathbf{a} \cdot (F\mathbf{b} \times \dot{F}F^{-1}F\mathbf{c})}{F\mathbf{a} \cdot (F\mathbf{b} \times F\mathbf{c})}\frac{F\mathbf{a} \cdot (F\mathbf{b} \times F\mathbf{c})}{a \cdot (\mathbf{b} \times \mathbf{c})}\\
&=J\ \text{tr}(\dot{F}F^{-1})\\
&= J\ \text{tr}(L).
\end{aligned}
\end{equation}
$$

**注：**

$$
\frac{M\mathbf{a} \cdot (\mathbf{b} \times \mathbf{c}) + \mathbf{a} \cdot (M\mathbf{b} \times \mathbf{c}) + \mathbf{a} \cdot (\mathbf{b} \times M\mathbf{c})}{\mathbf{a} \cdot (\mathbf{b} \times \mathbf{c})} = \text{tr}(M)
$$

证明：

由于

$$
\begin{equation}
\begin{aligned}
M\mathbf{a} \cdot (\mathbf{b} \times \mathbf{c}) &= \det(\begin{bmatrix}M\mathbf{a} & \mathbf{b} & \mathbf{c}\end{bmatrix}),\\
\mathbf{a} \cdot (M\mathbf{b} \times \mathbf{c}) &= \det(\begin{bmatrix}a & M\mathbf{b} & \mathbf{c}\end{bmatrix}),\\
\mathbf{a} \cdot (\mathbf{b} \times M\mathbf{c}) &= \det(\begin{bmatrix}a & \mathbf{b} & M\mathbf{c}\end{bmatrix}),
\end{aligned}
\end{equation}
$$

记 $M = \begin{bmatrix}\mathbf{m}_{1} & \mathbf{m}_{2} & \mathbf{m}_{3}\end{bmatrix}$，于是

$$
\begin{equation}
\begin{aligned}
\det(\begin{bmatrix}M\mathbf{a} & \mathbf{b} & \mathbf{c}\end{bmatrix}) & =a_{1}\det(\begin{bmatrix}\mathbf{m}_{1} & \mathbf{b} & \mathbf{c}\end{bmatrix}) + a_{2}\det(\begin{bmatrix}\mathbf{m}_{2} & \mathbf{b} & \mathbf{c}\end{bmatrix}) + a_{3}\det(\begin{bmatrix}\mathbf{m}_{3} & \mathbf{b} & \mathbf{c}\end{bmatrix}),\\
\det(\begin{bmatrix}\mathbf{a} & M\mathbf{b} & \mathbf{c}\end{bmatrix}) & =b_{1}\det(\begin{bmatrix}\mathbf{a} & \mathbf{m}_{1} & \mathbf{c}\end{bmatrix}) + b_{2}\det(\begin{bmatrix}\mathbf{a} & \mathbf{m}_{2} & \mathbf{c}\end{bmatrix}) + b_{3}\det(\begin{bmatrix}\mathbf{a} & \mathbf{m}_{3} & \mathbf{c}\end{bmatrix}),\\
\det(\begin{bmatrix}\mathbf{a} & \mathbf{b} & M\mathbf{c}\end{bmatrix}) & =c_{1}\det(\begin{bmatrix}\mathbf{a} & \mathbf{b} & \mathbf{m}_{1}\end{bmatrix}) + c_{2}\det(\begin{bmatrix}\mathbf{a} & \mathbf{b} & \mathbf{m}_{2}\end{bmatrix}) + c_{3}\det(\begin{bmatrix}\mathbf{a} & \mathbf{b} & \mathbf{m}_{3}\end{bmatrix}),
\end{aligned}
\end{equation}
$$

其中，根据克拉默法则，式

$$
\det(\begin{bmatrix}\mathbf{m}_{1} & \mathbf{b} & \mathbf{c}\end{bmatrix}), \quad \det(\begin{bmatrix}\mathbf{a} & \mathbf{m}_{1} & \mathbf{c}\end{bmatrix}), \quad  \det(\begin{bmatrix}\mathbf{a} & \mathbf{b} & \mathbf{m}_{1}\end{bmatrix})
$$

是线性方程组

$$
\begin{bmatrix}\mathbf{a} & \mathbf{b} & \mathbf{c}\end{bmatrix}\mathbf{x} = \det(\begin{bmatrix}\mathbf{a} & \mathbf{b} & \mathbf{c}\end{bmatrix}) \cdot \mathbf{m}_{1}
$$

的解，即

$$
\begin{equation}
\begin{aligned}
&\det(\begin{bmatrix}\mathbf{m}_{1} & \mathbf{b} & \mathbf{c}\end{bmatrix})\cdot\mathbf{a} + \det(\begin{bmatrix}\mathbf{a} & \mathbf{m}_{1} & \mathbf{c}\end{bmatrix})\cdot \mathbf{b} + \det(\begin{bmatrix}\mathbf{a} & \mathbf{b} & \mathbf{m}_{1}\end{bmatrix})\cdot\mathbf{c}
=\mathbf{m}_{1} \cdot \det(\begin{bmatrix}\mathbf{a} & \mathbf{b} & \mathbf{c}\end{bmatrix}),
\end{aligned}
\end{equation}
$$

于是，根据向量第一项的等式，得到

$$
a_{1}\det(\begin{bmatrix}\mathbf{m}_{1} & \mathbf{b} & \mathbf{c}\end{bmatrix}) + b_{1}\det(\begin{bmatrix}\mathbf{a} & \mathbf{m}_{1} & \mathbf{c}\end{bmatrix}) + c_{1}\det(\begin{bmatrix}\mathbf{a} & \mathbf{b} & \mathbf{m}_{1}\end{bmatrix}) = m_{11}\det(\begin{bmatrix}\mathbf{a} & \mathbf{b} & \mathbf{c}\end{bmatrix}).
$$

类似地，对于第二列和第三列，有

$$
\begin{equation}
\begin{aligned}
a_{2}\det(\begin{bmatrix}\mathbf{m}_{2} & \mathbf{b} & \mathbf{c}\end{bmatrix}) + b_{2}\det(\begin{bmatrix}\mathbf{a} & \mathbf{m}_{2} & \mathbf{c}\end{bmatrix}) + c_{2}\det(\begin{bmatrix}\mathbf{a} & \mathbf{b} & \mathbf{m}_{2}\end{bmatrix}) = m_{22}\det(\begin{bmatrix}\mathbf{a} & \mathbf{b} & \mathbf{c}\end{bmatrix}),\\
a_{3}\det(\begin{bmatrix}\mathbf{m}_{3} & \mathbf{b} & \mathbf{c}\end{bmatrix}) + b_{3}\det(\begin{bmatrix}\mathbf{a} & \mathbf{m}_{3} & \mathbf{c}\end{bmatrix}) + c_{3}\det(\begin{bmatrix}\mathbf{a} & \mathbf{b} & \mathbf{m}_{3}\end{bmatrix}) = m_{33}\det(\begin{bmatrix}\mathbf{a} & \mathbf{b} & \mathbf{c}\end{bmatrix}),
\end{aligned}
\end{equation}
$$

代入即可

:::