# Truesdell 应力率

Truesdell 应力率基于客观应力 [PK2](../chap4/sec2-2ndPiolaKirchhoff.md) 定义

$$
\overset{\circ}{\boldsymbol{\sigma}} = 
J^{-1}F\dot{\mathbf{S}}F^{T} = \dot{\boldsymbol{\sigma}} - \mathbf{L}\boldsymbol{\sigma} - \boldsymbol{\sigma}\mathbf{L}^{T} + \text{tr}(\mathbf{L})\boldsymbol{\sigma}.
$$

Truesdell 应力率严格满足客观性，适用于需要高精度和严格框架不变性的有限变形分析。然而，其表达复杂、计算量大，数值实现较为繁琐，在各向同性塑性等某些情形下可能引入不必要的复杂性，甚至导致不理想的分析结果。因此，Truesdell 应力率更适合对客观性和理论严谨性要求较高的场合，而在一般工程应用中可根据实际需求选用更为简便的应力率形式

## 推导

根据 PK2 应力，有

$$
J\boldsymbol{\sigma} = F\mathbf{S}F^{T},
$$

上式两端对时间 $t$ 求导，左端得

$$
\frac{\mathrm{d}}{\mathrm{d}t}(J\boldsymbol{\sigma}) = \dot{J}\boldsymbol{\sigma} + J\dot{\boldsymbol{\sigma}},
$$ (sec3-eq:truesdell-1)

右端得

$$
\frac{\mathrm{d}}{\mathrm{d}t}(F\mathbf{S}F^{T}) = \dot{F}\mathbf{S}F^{T} + F\dot{\mathbf{S}}F^{T} + F\mathbf{S}\dot{F}^{T},
$$

由于

$$
\mathbf{L} = \dot{F}F^{-1}\quad\Longrightarrow\quad \dot{F} = \mathbf{L}F,
$$

于是

$$
\begin{equation}
\begin{aligned}
\frac{\mathrm{d}}{\mathrm{d}t}(F\mathbf{S}F^{T})&=\mathbf{L}F\mathbf{S}F^{T}+F\dot{\mathbf{S}}F^{T}+F\mathbf{S}F^{T}\mathbf{L}^{T}\\
&=J\mathbf{L}\boldsymbol{\sigma}+F\dot{\mathbf{S}}F^{T}+J\boldsymbol{\sigma}\mathbf{L}^{T},
\end{aligned}
\end{equation}
$$ (sec3-eq:truesdell-2)

综合式 {eq}`sec3-eq:truesdell-1` 和 {eq}`sec3-eq:truesdell-2`，得

$$
\dot{J}\boldsymbol{\sigma} + J\dot{\boldsymbol{\sigma}} = J\mathbf{L}\boldsymbol{\sigma}+F\dot{\mathbf{S}}F^{T}+J\boldsymbol{\sigma}\mathbf{L}^{T},
$$

代入[局部体积变化速率](../chap3/sec1-velocity-gradient.md)

$$
\dot{J} = J\text{tr}(\mathbf{L}),
$$

两边除以 $J$，整理得到

$$
J^{-1}F\dot{\mathbf{S}}F^{T} = \dot{\boldsymbol{\sigma}} - \mathbf{L}\boldsymbol{\sigma} - \boldsymbol{\sigma}\mathbf{L}^{T} + \text{tr}(\mathbf{L})\boldsymbol{\sigma}.
$$


## 客观性

由于在刚体旋转阶段

$$
\mathbf{L} = \mathbf{W},
$$

此时也有 $\text{tr}(\mathbf{L}) = \text{tr}(\mathbf{W}) = 0$，因此，Truesdell 应力率的客观性也同 Jaumann 应力率得到满足

## 协变性

即，若存在坐标旋转变换

$$
\mathbf{x}'(t) = Q_{r}(t)\mathbf{x}(t),
$$

则

$$
\overset{\circ}{\boldsymbol{\sigma}'} := \dot{\boldsymbol{\sigma}}' - \mathbf{L}'\boldsymbol{\sigma}' - \boldsymbol{\sigma}'\mathbf{L}'^{T} + \text{tr}(\mathbf{L}')\boldsymbol{\sigma}' = Q_{r}\overset{\circ}{\boldsymbol{\sigma}}Q_{r}^{T}.
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

且

$$
\boldsymbol{\sigma}' = Q_{r}\boldsymbol{\sigma}Q_{r}^T,
$$

于是

$$
\begin{equation}
\begin{aligned}
\dot{\boldsymbol{\sigma}}' &= \dot{Q}_{r}\boldsymbol{\sigma}Q_{r}^T+Q_{r}\dot{\boldsymbol{\sigma}}Q_{r}^T+Q_{r}\boldsymbol{\sigma}\dot{Q}_{r}^T,\\
-\mathbf{L}'\boldsymbol{\sigma}' &= -\dot{Q}_{r}\boldsymbol{\sigma}Q_{r}^T - Q_{r}\mathbf{L}\boldsymbol{\sigma}Q_{r}^T,\\
- \boldsymbol{\sigma}'\mathbf{L}'^{T}&=-Q_{r}\boldsymbol{\sigma}\dot{Q}_{r}^T - Q_{r}\boldsymbol{\sigma}\mathbf{L}Q_{r}^{T}，\\
\text{tr}(\mathbf{L}')\boldsymbol{\sigma}'&=(\text{tr}(\dot{Q}_{r}Q_{r}^{T})+\text{tr}(Q_{r}\mathbf{L}Q_{r}^{T}))\boldsymbol{\sigma}',
\end{aligned}
\end{equation}
$$

由于 $\dot{Q}_{r}Q_{r}^{T}$ 是反对称矩阵，且正交变换保迹，因此

$$
\text{tr}(\dot{Q}_{r}Q_{r}^{T})+\text{tr}(Q_{r}\mathbf{L}Q_{r}^{T}) = \text{tr}(\mathbf{L}),
$$

代入并将上述四式相加，得到

$$
\begin{equation}
\begin{aligned}
\overset{\circ}{\boldsymbol{\sigma}'} &:= \dot{\boldsymbol{\sigma}}' - \mathbf{L}'\boldsymbol{\sigma}' - \boldsymbol{\sigma}'\mathbf{L}'^{T} + \text{tr}(\mathbf{L}')\boldsymbol{\sigma}'\\
&=Q_{r}(\dot{\boldsymbol{\sigma}} - \mathbf{L}\boldsymbol{\sigma} - \boldsymbol{\sigma}\mathbf{L}^{T} + \text{tr}(\mathbf{L})\boldsymbol{\sigma})Q_{r}^{T}\\
&=Q_{r}\overset{\circ}{\boldsymbol{\sigma}}Q_{r}^{T}.
\end{aligned}
\end{equation}
$$