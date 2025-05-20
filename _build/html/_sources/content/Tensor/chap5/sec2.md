# temp




## 协变

$$

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
\mathbf{L}' = \dot{F}'F'^{-1} &= (\dot{Q}F+Q\dot{F})F^{-1}Q^{T}\\
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
\boldsymbol{\sigma}'\mathbf{L}' &=Q\boldsymbol{\sigma}Q^{T}\dot{Q}Q^{T}+Q\boldsymbol{\sigma}LQ^{T},\\
\mathbf{L}'^{T} \boldsymbol{\sigma}' &=Q\dot{Q}^{T}Q\boldsymbol{\sigma}Q^{T}+QL^{T}\boldsymbol{\sigma}Q^{T}.
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
\overset{\circ}{\boldsymbol{\sigma}'} &= \dot{\boldsymbol{\sigma}}' + \mathbf{L}'^{T} \boldsymbol{\sigma}' + \boldsymbol{\sigma}'\mathbf{L}' \\
&=Q\dot{\boldsymbol{\sigma}}Q^{T} + Q\boldsymbol{\sigma}LQ^{T}-QL\boldsymbol{\sigma}Q^{T}\\
&=Q(\dot{\boldsymbol{\sigma}} + \boldsymbol{\sigma}\mathbf{L} + \mathbf{L}^{T}\boldsymbol{\sigma})Q^{T}\\
&=Q\overset{\circ}{\boldsymbol{\sigma}}Q^{T}.
\end{aligned}
\end{equation}
$$