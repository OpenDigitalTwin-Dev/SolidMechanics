# 显式动力学

当结构或材料在短时间内受到快速变化的载荷、冲击、爆炸、碰撞、振动或地震等作用，**惯性效应显著、加速度不可忽略时，必须采用动力学求解方法**，以准确分析其在时间历程中的响应和动态行为

## 动力学求解

与静力学求解相比，动力学求解的最大不同在于方程中保留了时间项，动力学分析中的时间通常是真实的物理时间，能够直接反映结构或材料在每一时刻的实际响应过程。因此，在有限元分析时，除了需要对空间进行离散，还必须对**时间离散**，此时每一个时间步都对应具体的物理时间长度，而不像静力学分析中那样仅作为载荷分步的数值过程

## 求解方程

与静力学求解不同，平衡方程中的速度项和加速度项均不可忽略

$$
\begin{equation}
\nabla\cdot \boldsymbol{\sigma} + \mathbf{f}= \rho\ddot{\mathbf{u}} + c\dot{\mathbf{u}} ,
\end{equation}
$$

其中，$\rho$ 是密度，$c$ 是阻尼系数；除此之外，还需要给出初始条件

$$
\mathbf{u}(\mathbf{x},0) = \mathbf{u}_{0}(\mathbf{x}),\quad \dot{\mathbf{u}}(\mathbf{x},0) = \dot{\mathbf{u}_{0}}(\mathbf{x}).
$$

其余方程均保持不变

## 弱形式

有限元弱形式为

$$
\begin{equation}
\begin{aligned}
\int_{\Omega}\rho\ddot{\mathbf{u}}\cdot\mathbf{v} \, \mathrm{d}V + 
\int_{\Omega}c\dot{\mathbf{u}}\cdot\mathbf{v} \, \mathrm{d}V +
\int_{\Omega} \boldsymbol{\varepsilon}(\mathbf{v}) : \boldsymbol{\sigma} \, \mathrm{d}V + \int_{\Gamma_{R}} \alpha\mathbf{u} \cdot \mathbf{v} \, \mathrm{d}S\\
= \int_{\Omega}\mathbf{f}\cdot \mathbf{v}\,\mathrm{d}V + \int_{\Gamma_{N}} \tilde{\mathbf{p}} \cdot \mathbf{v} \, \mathrm{d}S + \int_{\Gamma_{R}} \mathbf{f}_{R} \cdot \mathbf{v} \, \mathrm{d}S,\quad \forall \, \mathbf{v} \in \, \mathcal{V},
\end{aligned}
\end{equation}
$$

其中，$\mathbf{v}\in\mathcal{V}$ 是试验函数，$\mathbf{u} = \mathbf{\tilde{u}},\, \text{on}\, \Gamma_{D}$

## 离散形式

由于时间项的引入，此时不仅要进行空间离散，也要进行时间离散

### 空间离散


类似地，得到共计 $3N$ 个位移自由度 

$$
u_{x,1},u_{y,1},u_{z,1},u_{x,2},u_{y,2},u_{z,2},\cdots,u_{x,N},u_{y,N},u_{z,N},
$$

和 $3N$ 个求解方程

$$
\begin{equation}
\begin{aligned}
&\int_{\Omega}\rho\ddot{\mathbf{u}}\cdot\mathbf{v}_{*,i} \, \mathrm{d}V +
\int_{\Omega}c\dot{\mathbf{u}}\cdot\mathbf{v}_{*,i} \, \mathrm{d}V +
\int_{\Omega} \boldsymbol{\varepsilon}(\mathbf{v}_{*,i}) : \boldsymbol{\sigma} \, \mathrm{d}V + \int_{\Gamma_{R}} \alpha\mathbf{u} \cdot \mathbf{v}_{*,i} \, \mathrm{d}S \\
=& \int_{\Omega}\mathbf{f}\cdot \mathbf{v}_{*,i}\,\mathrm{d}V + \int_{\Gamma_{N}} \tilde{\mathbf{p}} \cdot \mathbf{v}_{*,i}\ \mathrm{d}S + \int_{\Gamma_{R}} \mathbf{f}_{R} \cdot \mathbf{v}_{*,i} \, \mathrm{d}S,\quad \forall \, \mathbf{v}_{*,i} \in \, \mathcal{V},\quad *=x,y,z;\ i=1:N.
\end{aligned}
\end{equation}
$$

在静力学求解中，空间离散完得到的是非线性的代数方程，而在动力学求解中，上述方程是一个非线性的**微分方程**

将上述方程记为

$$
\ddot{\mathbf{F}}^{\text{a}}(t)+\dot{\mathbf{F}}^{\text{v}}(t)+\mathbf{F}^{\text{int}} (t)+ \mathbf{F}^{r}(t) = \mathbf{F}^{\text{ext}}(t),
$$ (sec5-eq:fea-space)

其中
- 加速度项（二阶导）：$\ddot{\mathbf{F}}^{\text{a}}(t):=\int_{\Omega}\rho\ddot{\mathbf{u}}\cdot\mathbf{v}_{*,i} \, \mathrm{d}V$
- 速度项（一阶导）：$\dot{\mathbf{F}}^{\text{v}}(t):=\int_{\Omega}c\dot{\mathbf{u}}\cdot\mathbf{v}_{*,i} \, \mathrm{d}V$
- 内力项向量：$\mathbf{F}^{\text{int}}(t):=\int_{\Omega} \boldsymbol{\varepsilon}(\mathbf{v}_{*,i}) : \boldsymbol{\sigma} \, \mathrm{d}V$
- Robin 边界条件贡献向量：$\mathbf{F}^{\text{r}}(t):=\int_{\Gamma_{R}} \alpha\mathbf{u} \cdot \mathbf{v}_{*,i} \, \mathrm{d}S$
- 外力向量：$\mathbf{F}^{\text{ext}}(t):=\int_{\Omega}\mathbf{f}\cdot \mathbf{v}_{*,i}\,\mathrm{d}V + \int_{\Gamma_{N}} \tilde{\mathbf{p}} \cdot \mathbf{v}_{*,i}\ \mathrm{d}S + \int_{\Gamma_{R}} \mathbf{f}_{R} \cdot \mathbf{v}_{*,i} \, \mathrm{d}S$

为表示方便，这里使用 Vogit 形式，计算推导过程与前文类似，在每个单元上（等式最右端为 $\mathbf{u}_{E}$，仍记为 $\mathbf{u}$）

$$
\begin{equation}
\begin{aligned}
&\ddot{\mathbf{F}}^{\text{a}} = \int_{E} \rho\ddot{\mathbf{u}}\cdot\mathbf{v}_{*,i} \, \mathrm{d}E = \int_{E}\rho\mathbf{N}^{T}\ddot{\mathbf{u}}\ \mathbf{d}E= \int_{E}\rho\mathbf{N}^{T}\mathbf{N}\ \mathbf{d}E\cdot\ddot{\mathbf{u}},\\
&\dot{\mathbf{F}}^{\text{v}} = \int_{E} c\dot{\mathbf{u}}\cdot\mathbf{v}_{*,i} \, \mathrm{d}E = \int_{E}\rho\mathbf{N}^{T}\dot{\mathbf{u}}\ \mathbf{d}E= \int_{E}c\mathbf{N}^{T}\mathbf{N}\ \mathbf{d}E\cdot\dot{\mathbf{u}},\\
&\mathbf{F}^{\text{int}} = \int_{E} \boldsymbol{\varepsilon}(\mathbf{v}_{*,i}) : \boldsymbol{\sigma} \, \mathrm{d}E = \int_{E}\mathbf{B}^{T}\boldsymbol{\sigma}\, \mathrm{d}E,\\
&\mathbf{F}^{r}=\int_{\Gamma_{R,E}} \alpha\mathbf{u} \cdot \mathbf{v}_{*,i} \, \mathrm{d}S=\int_{\Gamma_{R,E}} \alpha\mathbf{N}^{T}\mathbf{u}\, \mathrm{d}S=\int_{\Gamma_{R,E}} \alpha\mathbf{N}^{T}\mathbf{N}\, \mathrm{d}S\cdot\mathbf{u},\\
&\mathbf{F}^{\text{ext}}=\int_{E}\mathbf{N}^{T}\mathbf{f}\,\mathrm{d}E + \int_{\Gamma_{N,E}} \mathbf{N}^{T}\tilde{\mathbf{p}}\ \mathrm{d}S + \int_{\Gamma_{R,E}} \mathbf{N}^{T}\mathbf{f}_{R}\, \mathrm{d}S,
\end{aligned}
\end{equation}
$$

上式通常写为

$$
\mathbf{M}\ddot{\mathbf{u}}+\mathbf{C}\dot{\mathbf{u}}+\mathbf{F}^{\text{int}}+\mathbf{K}_{r}\mathbf{u}-\mathbf{F}^{\text{ext}} = \mathbf{0},
$$

其中

$$
\begin{equation}
\begin{aligned}
&\mathbf{M} = \int_{E}\rho\mathbf{N}^{T}\mathbf{N}\ \mathbf{d}E,\quad \mathbf{C} = \int_{E}c\mathbf{N}^{T}\mathbf{N}\ \mathbf{d}E,\quad \mathbf{K}_{r}=\int_{\Gamma_{R}^{E}} \alpha\mathbf{N}^{T}\mathbf{N}\, \mathrm{d}S.
\end{aligned}
\end{equation}
$$

对于线弹性本构，有

$$
\mathbf{F}^{\text{int}} =\int_{E}\mathbf{B}^{T}\mathbb{C}\mathbf{B}\ \mathbf{d}E\cdot\mathbf{u}=\mathbf{K}\mathbf{u},
$$

### 分量计算

#### 矩阵分量

$$
\begin{equation}
\begin{aligned}
&\ddot{\mathbf{F}}^{\text{a}}_{ij*+} = \int_{E} \rho\mathbf{v}_{+,j}\cdot\mathbf{v}_{*,i} \, \mathrm{d}E\ \ddot{\mathbf{u}}_{j+} = \delta_{*,+}\int_{E} \rho v_{j}v_{i} \, \mathrm{d}E\ \ddot{\mathbf{u}}_{j+},\\
&\dot{\mathbf{F}}^{\text{v}}_{ij*+} = \int_{E} c\mathbf{v}_{+,j}\cdot\mathbf{v}_{*,i} \, \mathrm{d}E\ \dot{\mathbf{u}}_{j+} = \delta_{*,+}\int_{E} c v_{j}v_{i} \, \mathrm{d}E\ \dot{\mathbf{u}}_{j+},\\
\end{aligned}
\end{equation}
$$

#### 右端项分量

$$
\begin{equation}
\begin{aligned}
&\ddot{\mathbf{F}}^{\text{a}}_{i*} = \int_{E} \rho\mathbf{v}_{*,i}\sum_{+,j}\mathbf{v}_{+,j}\ddot{\mathbf{u}}_{j+}\, \mathrm{d}E = \delta_{*,+}\int_{E} \rho v_{i}\sum_{j}v_{j} \ddot{\mathbf{u}}_{j*} \, \mathrm{d}E = \delta_{*,+}\sum_{j}\int_{E} \rho v_{i}v_{j} \ddot{\mathbf{u}}_{j*} \, \mathrm{d}E,\\
&\dot{\mathbf{F}}^{\text{v}}_{i*} = \int_{E} c\mathbf{v}_{*,i}\sum_{+,j}\mathbf{v}_{+,j}\dot{\mathbf{u}}_{j+} \mathrm{d}E = \delta_{*,+}\int_{E} c v_{i}\sum_{j}v_{j} \dot{\mathbf{u}}_{j*} \, \mathrm{d}E = \delta_{*,+}\sum_{j}\int_{E} c v_{i}v_{j} \dot{\mathbf{u}}_{j*} \, \mathrm{d}E,\\
\end{aligned}
\end{equation}
$$
