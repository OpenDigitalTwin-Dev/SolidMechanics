# Jaumann 应力率

<span class="gray-text">
Jaumann 应力率的核心思想是：在随材料局部旋转的共旋坐标系中描述应力的变化，从而消除刚体旋转对应力率的影响
</span>

## Jaumann 应力率

### 共旋导数

共旋导数是“去除了参考系旋转影响”的时间导数，反映了物理量在随体坐标系下的真实变化率

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

**在 Jaumann 应力率中，使用**

$$
\dot{\mathbf{e}}_{i} = \mathbf{W}\mathbf{e}_{i},
$$

因此

$$
\dot{\sigma_{ij}}\mathbf{e}_{i}\mathbf{e}_{j}^{T} = \dot{\boldsymbol{\sigma}} - \sigma_{ij}\mathbf{W}\mathbf{e}_{i}\mathbf{e}_{j}^{T} + \sigma_{ij}\mathbf{e}_{i}\mathbf{e}_{j}^{T}\mathbf{W},
$$

故

$$
\dot{\sigma_{ij}}\mathbf{e}_{i}\mathbf{e}_{j}^{T} = \dot{\boldsymbol{\sigma}} + \boldsymbol{\sigma}\mathbf{W} - \mathbf{W}\boldsymbol{\sigma}.
$$

于是得到 Jaumann 应力率

$$
\overset{\circ}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} + \boldsymbol{\sigma} \mathbf{W} - \mathbf{W} \boldsymbol{\sigma}.
$$

Jaumann 应力率通过引入旋转修正项，有效剔除了由刚体旋转引起的虚假应力变化，且具有形式简单、计算高效的优点

**Jaumann 应力率在有限变形中较小变形或纯旋转的弹塑性问题中，能够较好地反映材料的实际物理行为，因此被广泛应用于常规工程分析。然而，由于其假设基底的旋转速率为 $\dot{\mathbf{e}}_{i} = \mathbf{W}\mathbf{e}_{i}$，而 $\mathbf{W}$ 在大变形条件下难以准确描述材料元的实际旋转，容易引入非物理的“伪应力”，导致数值结果失真。因此，Jaumann应力率并不适用于大变形的问题**

### 客观性

<span class="gray-text">
参考系独立性或刚体旋转不变性
</span>

设存在**刚体旋转变换**（$\mathbf{x}_{0}$ 为当前状态）

$$
\mathbf{x}(t) = Q(t)\mathbf{x}_{0},
$$

其中，$Q(t)$ 表示同一次刚体旋转过程中，在时刻 $t$ 的正交旋转矩阵，因此，在旋转过程中

$$
\boldsymbol{\sigma}(t) = Q(t)\boldsymbol{\sigma}_{0}Q^{T}(t),\quad
\boldsymbol{\sigma}(0) = \boldsymbol{\sigma}_{0},
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

由于在[刚体旋转阶段](../chap3/sec1-velocity-gradient.md)

$$
\mathbf{W} = \dot{Q}Q^{T} = -Q\dot{Q}^{T},
$$

故

$$
\dot{\boldsymbol{\sigma}} = \mathbf{W}\boldsymbol{\sigma}-\boldsymbol{\sigma}\mathbf{W},
$$

因此，Jaumann 应力率在纯刚体旋转下，满足客观性要求

$$
\overset{\circ}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} + \boldsymbol{\sigma} \mathbf{W} - \mathbf{W} \boldsymbol{\sigma} = 0.
$$

### 协变性

<span class="gray-text">
随坐标系变换正交相似变换
</span>

即，若存在坐标旋转变换

$$
\mathbf{x}'(t) = Q_{r}(t)\mathbf{x}(t),
$$

则

$$
\overset{\circ}{\boldsymbol{\sigma}'} := \dot{\boldsymbol{\sigma}}' + \boldsymbol{\sigma}' \mathbf{W}' - \mathbf{W}' \boldsymbol{\sigma}' = Q_{r}\overset{\circ}{\boldsymbol{\sigma}}Q_{r}^{T}.
$$

由于

$$
\begin{equation}
\begin{aligned}
\mathbf{L}' = \dot{F}'F'^{-1} &= (\dot{Q}_{r}F+Q_{r}\dot{F})F^{-1}Q_{r}^{T}\\
&=\dot{Q}_{r}Q_{r}^{T}+Q_{r}\dot{F}F^{-1}Q_{r}^{T}\\
&=\dot{Q}_{r}Q_{r}^{T} + Q_{r}\mathbf{L}Q_{r}^{T},
\end{aligned}
\end{equation}
$$

故

$$
\begin{equation}
\begin{aligned}
\mathbf{W}' = \frac{1}{2}(\mathbf{L}' - \mathbf{L}'^{T}) = \dot{Q}_{r}Q_{r}^{T} + Q_{r}\mathbf{W}Q_{r}^{T}.
\end{aligned}
\end{equation}
$$

且

$$
\boldsymbol{\sigma}' = Q_{r}\boldsymbol{\sigma}Q_{r}^T,
$$

于是

$$
\begin{equation}
\begin{aligned}
\dot{\boldsymbol{\sigma}}' &= \dot{Q}_{r}\boldsymbol{\sigma}Q_{r}^T+Q_{r}\dot{\boldsymbol{\sigma}}Q_{r}^T+Q_{r}\boldsymbol{\sigma}\dot{Q}_{r}^T,\\
\boldsymbol{\sigma}' \mathbf{W}' &= Q_{r}\boldsymbol{\sigma}\mathbf{W}Q_{r}^{T} + Q_{r}\boldsymbol{\sigma}Q_{r}^{T}\dot{Q}_{r}Q_{r}^{T},\\
-\mathbf{W}'\boldsymbol{\sigma}'&=-Q_{r}\mathbf{W}\boldsymbol{\sigma}Q_{r}^{T} - \dot{Q}_{r}\boldsymbol{\sigma}Q_{r}^{T}，
\end{aligned}
\end{equation}
$$

代入 $\dot{Q}_{r}Q_{r}^{T} = -Q_{r}\dot{Q}_{r}^{T}$ 到 $\boldsymbol{\sigma}' \mathbf{W}'$，三式相加得到

$$
\begin{equation}
\begin{aligned}
\overset{\circ}{\boldsymbol{\sigma}'} &= \dot{\boldsymbol{\sigma}}' + \boldsymbol{\sigma}' \mathbf{W}' -\mathbf{W}'\boldsymbol{\sigma}' \\
&= Q_{r}(\dot{\boldsymbol{\sigma}}+\boldsymbol{\sigma}\mathbf{W}-\mathbf{W}\boldsymbol{\sigma})Q_{r}^{T} \\
&= Q_{r}\overset{\circ}{\boldsymbol{\sigma}}Q_{r}^{T}.
\end{aligned}
\end{equation}
$$

## Kirchhoff 应力的 Jaumann 应力率

对于 [Kirchhoff 应力](../chap4/sec3-Kirchhoff.md)，有

$$
\overset{\circ}{\boldsymbol{\tau}} = \dot{\boldsymbol{\tau}} + \boldsymbol{\tau} \mathbf{W} - \mathbf{W} \boldsymbol{\tau},
$$

根据[局部体积变化速率](../chap3/sec1-velocity-gradient.md)公式

$$
\dot{\boldsymbol{\tau}} = \dot{J}\boldsymbol{\sigma} + J\dot{\boldsymbol{\sigma}} = J\ \text{tr}(\mathbf{L})\boldsymbol{\sigma} + J\dot{\boldsymbol{\sigma}}  = J\ \text{tr}(\mathbf{D})\boldsymbol{\sigma} + J\dot{\boldsymbol{\sigma}} ,
$$

故

$$
\overset{\circ}{\boldsymbol{\tau}} = J(\dot{\boldsymbol{\sigma}} + \boldsymbol{\sigma}\text{tr}(\mathbf{D}) + \boldsymbol{\sigma} \mathbf{W} - \mathbf{W} \boldsymbol{\sigma}),
$$

记

$$
\overset{\nabla}{\boldsymbol{\tau}} = \dot{\boldsymbol{\sigma}} + \boldsymbol{\sigma}\text{tr}(\mathbf{D}) + \boldsymbol{\sigma} \mathbf{W} - \mathbf{W} \boldsymbol{\sigma}.
$$