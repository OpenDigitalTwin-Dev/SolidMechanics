# Jaumann 应力率

<span class="gray-text">
Jaumann 应力率的核心思想是：在随材料局部旋转的共旋坐标系中描述应力的变化，从而消除刚体旋转对应力率的影响
</span>

Jaumann 应力率通过引入修正项，有效剔除了由刚体旋转引起的虚假应力变化

$$
\overset{\circ}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} + \boldsymbol{\sigma} W - W \boldsymbol{\sigma},
$$

其中，$W$ 是旋转率张量，是速度梯度 $L=\nabla\mathbf{v}$ 的反对称部分

$$
W = \frac{1}{2}(L - L^{T}).
$$

## 客观性

假设物体只进行旋转变换（$\mathbf{x}_{0}$ 为初始状态）

$$
\mathbf{x}(t) = Q(t)\mathbf{x}_{0}(t),
$$

其中，$Q(t)$ 是正交矩阵，于是

$$
\boldsymbol{\sigma} = Q(t)\boldsymbol{\sigma}_{0}Q^{T}(t),
$$

故

$$
\begin{equation}
\begin{aligned}
\dot{\boldsymbol{\sigma}} &= \dot{Q}\boldsymbol{\sigma}_{0}Q^{T} + Q\boldsymbol{\sigma}_{0}\dot{Q}^{T}\\
&=\dot{Q}Q^{T}Q\boldsymbol{\sigma}_{0}Q^{T}+Q\boldsymbol{\sigma}_{0}Q^{T}Q\dot{Q}^{T},
\end{aligned}
\end{equation}
$$

由于在刚体旋转中

$$
W = \dot{Q}Q^{T} = -Q\dot{Q}^{T},
$$

故

$$
\dot{\boldsymbol{\sigma}} = W\boldsymbol{\sigma}-\boldsymbol{\sigma}W,
$$

于是

$$
\overset{\circ}{\boldsymbol{\sigma}} = 0.
$$

## 协变性

此处证明

$$
\overset{\circ}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} + \boldsymbol{\sigma} L + L^{T} \boldsymbol{\sigma}
$$ (sec1-eq:Jaumann-1)

是协变的，即当发生刚体旋转（$\mathbf{x}_{0}$ 为初始状态）

$$
\mathbf{x}(t) = Q(t)\mathbf{x}_{0}(t)
$$

时，满足

$$
\overset{\circ}{\boldsymbol{\sigma}} = Q\overset{\circ}{\boldsymbol{\sigma}}_{0}Q^{T}.
$$