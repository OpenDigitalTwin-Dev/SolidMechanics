# Treusdell 应力率

由于

$$
\dot{\boldsymbol{\sigma}} = \frac{\mathrm{d} \boldsymbol{\sigma}}{\mathrm{d} t} = \frac{\partial \boldsymbol{\sigma}}{\partial t} + (\mathbf{v}\cdot\nabla)\boldsymbol{\sigma}，
$$

根据 [PK2 应力](../chap4/sec2-2ndPiolaKirchhoff.md)，有

$$
J\boldsymbol{\sigma} = F\mathbf{S}F^{T},
$$

上式两端对时间 $t$ 求导，左端得

$$
\frac{\mathrm{d}}{\mathrm{d}t}(J\boldsymbol{\sigma}) = \dot{J}\boldsymbol{\sigma} + J\dot{\boldsymbol{\sigma}},
$$ (sec3-eq:truesdell-1)

右端得

$$
\frac{\mathrm{d}}{\mathrm{d}t}(F\mathbf{S}F^{T}) = \dot{F}\mathbf{S}F^{T} + F\dot{\mathbf{S}}F^{T} + F\mathbf{S}\dot{F}^{T}
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

两边除以 $J$，得到

$$
\text{tr}(\mathbf{L})\boldsymbol{\sigma} + \dot{\boldsymbol{\sigma}} =  \mathbf{L}\boldsymbol{\sigma} + J^{-1}F\dot{\mathbf{S}}F^{T} + \boldsymbol{\sigma}\mathbf{L}^{T}.
$$

Truesdell 应力率定义为

$$
\overset{\circ}{\boldsymbol{\sigma}} = 
J^{-1}F\dot{\mathbf{S}}F^{T} = \dot{\boldsymbol{\sigma}} - \mathbf{L}\boldsymbol{\sigma} - \boldsymbol{\sigma}\mathbf{L}^{T} + \text{tr}(\mathbf{L})\boldsymbol{\sigma}.
$$