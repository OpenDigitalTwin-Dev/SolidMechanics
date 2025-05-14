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

## 几何解释

应力张量在随体基底 $\{\mathbf{e}_{i}\}_{i=1,2,3}$ 下可以写为

$$
\boldsymbol{\sigma}(t)= \sigma_{ij}(t)\mathbf{e}_{i}(t)\mathbf{e}_{j}^{T}(t),
$$

这得到

$$
\dot{\boldsymbol{\sigma}} = \frac{\mathrm{d} \boldsymbol{\sigma}}{\mathrm{d} t}  = \dot{\sigma}_{ij}\mathbf{e}_{i}\mathbf{e}_{j}^{T} + \sigma_{ij}\dot{\mathbf{e}}_{i}\mathbf{e}_{j}^{T} + \sigma_{ij}\mathbf{e}_{i}\dot{\mathbf{e}}_{j}^{T},
$$

从上式可以看到，应力张量的真实变化包括

- 应力分量本身的变化：材料真实的应力变化
- 基底变化引起的变化：旋转带来的伪变化

在材料本构分析中，通常只关注应力分量本身的真实变化

$$
\dot{\sigma_{ij}}\mathbf{e}_{i}\mathbf{e}_{j}^{T} = \dot{\boldsymbol{\sigma}} - \sigma_{ij}\dot{\mathbf{e}}_{i}\mathbf{e}_{j}^{T} - \sigma_{ij}\mathbf{e}_{i}\dot{\mathbf{e}}_{j}^{T},
$$ (sec1-eq:Jaumann-0)

设随体基底与初始基底 $\{\tilde{\mathbf{e}}_{i}\}_{i=1,2,3}$（不妨选为标准正交基）满足

$$
\begin{bmatrix}\mathbf{e}_{1}&\mathbf{e}_{2}&\mathbf{e}_{3}\end{bmatrix} = \begin{bmatrix}\tilde{\mathbf{e}}_{1}&\tilde{\mathbf{e}}_{2}&\tilde{\mathbf{e}}_{3}\end{bmatrix}Q(t) = Q,
$$

则

$$
\mathbf{e}_{i}  = \mathbf{q}_{i},
$$

其中，$\mathbf{q}_{i}$ 是过度矩阵 $Q$ 的第 $i$ 列，于是

$$
\dot{\mathbf{e}}_{i} = \dot{\mathbf{q}}_{i},
$$

代入到式 {eq}`sec1-eq:Jaumann-0` 中，得到

$$
\begin{equation}
\begin{aligned}
\dot{\sigma}_{ij}\mathbf{q}_{i}\mathbf{q}_{j}^{T} &= \dot{\boldsymbol{\sigma}} - \sigma_{ij}\dot{\mathbf{q}}_{i}\mathbf{q}_{j}^{T} - \sigma_{ij}\mathbf{q}_{i}\dot{\mathbf{q}}_{j}^{T}\\
\end{aligned}
\end{equation}
$$

由于

$$
\begin{equation}
\begin{aligned}
\dot{Q}Q^{T} = (\dot{\mathbf{q}}_{k}\tilde{\mathbf{e}}_{k}^{T})(\mathbf{q}_{l}\tilde{\mathbf{e}}_{l}^{T})^{T} = \dot{\mathbf{q}}_{k}\tilde{\mathbf{e}}_{k}^{T}\tilde{\mathbf{e}}_{l}\mathbf{q}_{l} = \dot{\mathbf{q}}_{k}\mathbf{q}_{k}^{T},
\end{aligned}
\end{equation}
$$

故

$$
\dot{Q}Q^{T}\boldsymbol{\sigma} = (\dot{\mathbf{q}}_{k}\mathbf{q}_{k}^{T})(\sigma_{ij}\mathbf{q}_{i}\mathbf{q}_{j}^{T}) = \sigma_{ij}\dot{\mathbf{q}}_{k}\mathbf{q}_{k}^{T}\mathbf{q}_{i}\mathbf{q}_{j}^{T} = \sigma_{ij}\dot{\mathbf{q}}_{i}\mathbf{q}_{j}^{T} ,
$$

于是

$$
\boldsymbol{\sigma}Q\dot{Q}^{T} = (\dot{Q}Q^{T}\boldsymbol{\sigma})^{T} = (\sigma_{ij}\dot{\mathbf{q}}_{i}\mathbf{q}_{j}^{T})^{T} = \sigma_{ij}\mathbf{q}_{j}\dot{\mathbf{q}}_{i}^{T}= \sigma_{ji}\mathbf{q}_{i}\dot{\mathbf{q}}_{j}^{T} = \sigma_{ij}\mathbf{q}_{i}\dot{\mathbf{q}}_{j}^{T},
$$

代入上面两式到式 {eq}`sec1-eq:Jaumann-0` 得到

$$
\begin{equation}
\begin{aligned}
\dot{\sigma}_{ij}\mathbf{q}_{i}\mathbf{q}_{j}^{T} &= \dot{\boldsymbol{\sigma}} - \dot{Q}Q^{T}\boldsymbol{\sigma} - \boldsymbol{\sigma}Q\dot{Q}^{T}\\
&=\dot{\boldsymbol{\sigma}} + \boldsymbol{\sigma}(\dot{Q}Q^{T}) - (\dot{Q}Q^{T})\boldsymbol{\sigma}.
\end{aligned}
\end{equation}
$$


## 客观性

假设物体**只进行刚体旋转变换**（$\mathbf{x}_{0}$ 为初始状态）

$$
\mathbf{x}(t) = Q(t)\mathbf{x}_{0},
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

是协变的，即若存在实时的坐标旋转变换

$$
\mathbf{x}'(t) = Q(t)\mathbf{x}(t),
$$

则

$$
\overset{\circ}{\boldsymbol{\sigma}'} = Q\overset{\circ}{\boldsymbol{\sigma}}Q^{T}.
$$

由于

$$
F'=\frac{\partial \mathbf{x}'}{\partial \mathbf{X}} = \frac{\partial \mathbf{x}'}{\partial \mathbf{x}}\frac{\partial \mathbf{x}}{\partial \mathbf{X}} = QF,
$$

于是

$$
\begin{equation}
\begin{aligned}
L' = \dot{F}'F'^{-1} &= (\dot{Q}F+Q\dot{F})F^{-1}Q^{T}\\
&=\dot{Q}Q^{T}+Q\dot{F}F^{-1}Q^{T}\\
&=\dot{Q}Q^{T} + QLQ^{T}
\end{aligned}
\end{equation}
$$

此外，根据坐标变换有

$$
\boldsymbol{\sigma}' = Q\boldsymbol{\sigma}Q^{T},
$$

于是

$$
\begin{equation}
\begin{aligned}
\dot{\boldsymbol{\sigma}}' &= \dot{Q}\boldsymbol{\sigma}Q^{T} + Q\dot{\boldsymbol{\sigma}}Q^{T} + Q\boldsymbol{\sigma}\dot{Q^{T}},\\
\boldsymbol{\sigma}'L' &=Q\boldsymbol{\sigma}Q^{T}\dot{Q}Q^{T}+Q\boldsymbol{\sigma}LQ^{T},\\
L'^{T} \boldsymbol{\sigma}' &=Q\dot{Q}^{T}Q\boldsymbol{\sigma}Q^{T}+QL^{T}\boldsymbol{\sigma}Q^{T}.
\end{aligned}
\end{equation}
$$ (sec1-eq:Jaumann-2)

由于 

$$
\dot{Q}Q^{T} = -Q\dot{Q}^{T}
$$

故

$$
\begin{equation}
\begin{aligned}
Q\boldsymbol{\sigma}Q^{T}\dot{Q}Q^{T}&=-Q\boldsymbol{\sigma}\dot{Q}^{T}\\
Q\dot{Q}^{T}Q\boldsymbol{\sigma}Q^{T}&=-\dot{Q}\boldsymbol{\sigma}Q^{T}
\end{aligned}
\end{equation}
$$

代入到式 {eq}`sec1-eq:Jaumann-2` 并三式相加得到

$$
\begin{equation}
\begin{aligned}
\overset{\circ}{\boldsymbol{\sigma}'} &= \dot{\boldsymbol{\sigma}}' + L'^{T} \boldsymbol{\sigma}' + \boldsymbol{\sigma}'L' \\
&=Q\dot{\boldsymbol{\sigma}}Q^{T} + Q\boldsymbol{\sigma}LQ^{T}-QL\boldsymbol{\sigma}Q^{T}\\
&=Q(\dot{\boldsymbol{\sigma}} + \boldsymbol{\sigma}L + L^{T}\boldsymbol{\sigma})Q^{T}\\
&=Q\overset{\circ}{\boldsymbol{\sigma}}Q^{T}.
\end{aligned}
\end{equation}
$$

对于刚体旋转变换

$$
\mathbf{x}(t) = \mathbf{Q}(t)\mathbf{X},
$$


有 $L=W,L^{T} = -W$，故式 {eq}`sec1-eq:Jaumann-1` 退化为

$$
\overset{\circ}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} + \boldsymbol{\sigma} W - W \boldsymbol{\sigma}.
$$