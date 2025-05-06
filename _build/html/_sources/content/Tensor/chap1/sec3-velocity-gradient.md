# 速度梯度

<span class="gray-text">
速度梯度描述了材料内部速度场的空间变化，反映了各部分之间的相对运动，是研究材料变形和流动的基础
</span>

速度向量表示为

$$
\mathbf{v} = \dot{\mathbf{u}} = \dot{\mathbf{x}} = \frac{\partial \mathbf{x}}{\partial t} \in \mathbb{R}^{3},
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

### 刚体旋转

对于刚体旋转变换，有

$$
\mathbf{x} = Q\mathbf{X},
$$

其中，$Q$ 是正交矩阵，于是

$$
L = \dot{Q}Q^{T},
$$

此时

$$
D = \frac{1}{2}\left(\dot{Q}Q^{T} + Q\dot{Q}^{T}\right) = \frac{1}{2}\dot{I} = 0,
$$

故

$$
W = L = \frac{1}{2}\left(\dot{Q}Q^{T} - Q\dot{Q}^{T}\right).
$$

### 局部体积变化速率

记 $J= \det(F)$，则

$$
\dot{J} = J\ \text{tr}(\dot{F}F^{-1}) = J\ \text{tr}(\nabla\mathbf{v})
$$

该公式表明，**单位体积的变化速率 $\dot{J}$，等于体积本身 $J$ 乘以速度场的散度（速度梯度场张量的迹）**

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

设 $a,b,c\in\mathbb{R}^{3}$ 是三个线性无关的向量，则

$$
J = \det(F) = \frac{Fa\cdot(Fb\times Fc)}{a\cdot(b\times c)}
=
\frac{\det\left(\begin{bmatrix}
Fa&Fb&Fc
\end{bmatrix}\right)}{
\det\left(\begin{bmatrix}
a&b&c
\end{bmatrix}\right)
},
$$

于是

$$
\begin{equation}
\begin{aligned}
\dot{J} &= \frac{\dot{F}a \cdot (Fb \times Fc) + Fa \cdot (\dot{F}b \times Fc) + Fa \cdot (Fb \times \dot{F}c)}{a \cdot (b \times c)}\\
&=\frac{\dot{F}F^{-1}Fa \cdot (Fb \times Fc) + Fa \cdot (\dot{F}F^{-1}Fb \times Fc) + Fa \cdot (Fb \times \dot{F}F^{-1}Fc)}{a \cdot (b \times c)}\\
&=\frac{\dot{F}F^{-1}Fa \cdot (Fb \times Fc) + Fa \cdot (\dot{F}F^{-1}Fb \times Fc) + Fa \cdot (Fb \times \dot{F}F^{-1}Fc)}{Fa \cdot (Fb \times Fc)}\frac{Fa \cdot (Fb \times Fc)}{a \cdot (b \times c)}\\
&=J\ \text{tr}(\dot{F}F^{-1})\\
&= J\ \text{tr}(L)
\end{aligned}
\end{equation}
$$

**注：**

$$
\frac{Aa \cdot (b \times c) + a \cdot (Ab \times c) + a \cdot (b \times Ac)}{a \cdot (b \times c)} = \text{tr}(A)
$$

证明：

由于

$$
\begin{equation}
\begin{aligned}
Aa \cdot (b \times c) &= \det(\begin{bmatrix}Aa & b & c\end{bmatrix}),\\
a \cdot (Ab \times c) &= \det(\begin{bmatrix}a & Ab & c\end{bmatrix}),\\
a \cdot (b \times Ac) &= \det(\begin{bmatrix}a & b & Ac\end{bmatrix}),
\end{aligned}
\end{equation}
$$

故分母为

$$
\det(\begin{bmatrix}Aa & b & c\end{bmatrix}) + \det(\begin{bmatrix}a & Ab & c\end{bmatrix}) + \det(\begin{bmatrix}a & b & Ac\end{bmatrix})
$$

:::