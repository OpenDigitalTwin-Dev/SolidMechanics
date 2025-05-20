# Green-Naghdi 应力率

<span class="gray-text">
Green-Naghdi 应力率的核心思想是：在随材料点极体旋转的参考系中，描述应力的变化，从而消除刚体旋转对应力率的影响
</span>

Green-Naghdi 应力率同样基于共旋导数，区别在于，Jaumann 应力率使用局部瞬时旋转

$$
\dot{\mathbf{e}}_{i} = \mathbf{W}\mathbf{e}_{i},
$$

**Green-Naghdi 应力率使用的是材料基于初始状态的的整体旋转**

## Green-Naghdi 应力率

设初始基底为 $\{\tilde{\mathbf{e}}_{i}\}_{i=1,2,3}$（不妨选为标准正交基），满足

$$
\begin{bmatrix}\mathbf{e}_{1}&\mathbf{e}_{2}&\mathbf{e}_{3}\end{bmatrix} = \begin{bmatrix}\tilde{\mathbf{e}}_{1}&\tilde{\mathbf{e}}_{2}&\tilde{\mathbf{e}}_{3}\end{bmatrix}Q(t) = Q,
$$

其中，$Q$ 来源于变形梯度矩阵的极分解 $F = QU$，是旋转矩阵

则

$$
\mathbf{e}_{i}  = \mathbf{q}_{i}\quad\Longrightarrow\quad \dot{\mathbf{e}}_{i} = \dot{\mathbf{q}}_{i},
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

记 $\boldsymbol{\Omega} = \dot{Q}Q^{T}$，得到 Green-Naghdi 应力率

$$
\overset{\circ}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} + \boldsymbol{\sigma} \boldsymbol{\Omega} - \boldsymbol{\Omega} \boldsymbol{\sigma}.
$$

**Green-Naghdi 应力率通过跟踪材料元的累计旋转 $\dot{\mathbf{e}}_{i} = \dot{\mathbf{q}}_{i}$，能够准确反映大旋转过程中的应力变化，适用于以刚体旋转为主的大旋转问题。相比 Jaumann 应力率，它能有效避免因旋转描述不准确而产生的“伪应力”。但在涉及显著剪切、拉伸等复杂大变形时，其物理描述仍有限，且实现复杂、计算量大**

### 客观性

由于在刚体旋转阶段

$$
\mathbf{W} = \dot{Q}Q^{T} = -Q\dot{Q}^{T} = \boldsymbol{\Omega},
$$

因此，Green-Naghdi 应力率的客观性也同 Jaumann 应力率得到满足

### 协变性

即，若存在坐标旋转变换

$$
\mathbf{x}'(t) = Q_{r}(t)\mathbf{x}(t),
$$

则

$$
\overset{\circ}{\boldsymbol{\sigma}'} := \dot{\boldsymbol{\sigma}}' + \boldsymbol{\sigma}' \boldsymbol{\Omega}' - \boldsymbol{\Omega}' \boldsymbol{\sigma}' = Q_{r}\overset{\circ}{\boldsymbol{\sigma}}Q_{r}^{T}.
$$


由于

$$
\begin{equation}
\begin{aligned}
\boldsymbol{\Omega}'= \dot{Q}'Q'^{T},
\end{aligned}
\end{equation}
$$

其中，$Q'$ 来自变形梯度矩阵 $F' = Q'U'$ 的极分解，由于

$$
F' = Q_{r}F = Q_{r}QU
$$

根据极分解的唯一性，有

$$
Q' = Q_{r}Q,
$$

故

$$
\boldsymbol{\Omega}'=\dot{Q}'Q'^{T}= \dot{Q}_{r}Q_{r}^{T} + Q_{r}\dot{Q}Q^{T}Q_{r}^{T} = \dot{Q}_{r}Q_{r}^{T} + Q_{r}\boldsymbol{\Omega}Q_{r}^{T}.
$$

由于

$$
\begin{equation}
\begin{aligned}
\dot{\boldsymbol{\sigma}}' &= \dot{Q}_{r}\boldsymbol{\sigma}Q_{r}^T+Q_{r}\dot{\boldsymbol{\sigma}}Q_{r}^T+Q_{r}\boldsymbol{\sigma}\dot{Q}_{r}^T,\\
\boldsymbol{\sigma}' \boldsymbol{\Omega}' &= Q_{r}\boldsymbol{\sigma}\boldsymbol{\Omega}Q_{r}^{T} + Q_{r}\boldsymbol{\sigma}Q_{r}^{T}\dot{Q}_{r}Q_{r}^{T},\\
-\boldsymbol{\Omega}'\boldsymbol{\sigma}'&=-Q_{r}\boldsymbol{\Omega}\boldsymbol{\sigma}Q_{r}^{T} - \dot{Q}_{r}\boldsymbol{\sigma}Q_{r}^{T}，
\end{aligned}
\end{equation}
$$

代入 $\dot{Q}_{r}Q_{r}^{T} = -Q_{r}\dot{Q}_{r}^{T}$ 到 $\boldsymbol{\sigma}' \boldsymbol{\Omega}'$，三式相加得到

$$
\begin{equation}
\begin{aligned}
\overset{\circ}{\boldsymbol{\sigma}'} &= \dot{\boldsymbol{\sigma}}' + \boldsymbol{\sigma}' \boldsymbol{\Omega}' -\boldsymbol{\Omega}'\boldsymbol{\sigma}' \\
&= Q_{r}(\dot{\boldsymbol{\sigma}}+\boldsymbol{\sigma}\boldsymbol{\Omega}-\boldsymbol{\Omega}\boldsymbol{\sigma})Q_{r}^{T} \\
&= Q_{r}\overset{\circ}{\boldsymbol{\sigma}}Q_{r}^{T}.
\end{aligned}
\end{equation}
$$

