# 速度梯度

<span class="gray-text">
速度梯度描述了材料内部速度场的空间变化，反映了各部分之间的相对运动，是研究材料变形和流动的基础
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
W = L = \frac{1}{2}\left(\dot{Q}Q^{T} - Q\dot{Q}^{T}\right) = \dot{Q}Q^{T} = -Q\dot{Q}^{T}.
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