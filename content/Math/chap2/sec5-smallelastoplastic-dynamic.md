# 小变形弹塑性问题（动力学）

当结构或材料在短时间内受到快速变化的载荷、冲击、爆炸、碰撞、振动或地震等作用，**惯性效应显著、加速度不可忽略时，必须采用动力学求解方法**，以准确分析其在时间历程中的响应和动态行为

## 求解方程

与静力学求解不同，平衡方程中的加速度项不可忽略

$$
\begin{equation}
\nabla\cdot \boldsymbol{\sigma} + \mathbf{f} = \rho\ddot{\mathbf{u}},
\end{equation}
$$

除此之外，还需要给出初始条件

$$
\mathbf{u}(\mathbf{x},0) = \mathbf{u}_{0}(\mathbf{x}),\quad \dot{\mathbf{u}}(\mathbf{x},0) = \dot{\mathbf{u}_{0}}(\mathbf{x}).
$$

其余方程均保持不变


## 动力学求解

与静力学求解相比，动力学求解的最大不同在于方程中保留了时间项，动力学分析中的时间通常是真实的物理时间，能够直接反映结构或材料在每一时刻的实际响应过程。因此，在有限元分析时，除了需要对空间进行离散，还必须对**时间离散**，此时每一个时间步都对应具体的物理时间长度，而不像静力学分析中那样仅作为载荷分步的数值过程

## 有限元弱形式

类似地，弱形式为

$$
\int_{\Omega}\rho\ddot{\mathbf{u}}\cdot\mathbf{v} \, \mathrm{d}\Omega + 
\int_{\Omega} \boldsymbol{\varepsilon}(\mathbf{v}) : \boldsymbol{\sigma} \, \mathrm{d}\Omega + \int_{\Gamma_{R}} \alpha\mathbf{u} \cdot \mathbf{v} \, \mathrm{d}S
= \int_{\Omega}\mathbf{f}\cdot \mathbf{v}\,\mathrm{d}\Omega + \int_{\Gamma_{N}} \tilde{\mathbf{p}} \cdot \mathbf{v} \, \mathrm{d}S + \int_{\Gamma_{R}} \mathbf{f}_{R} \cdot \mathbf{v} \, \mathrm{d}S,\quad \forall \, \mathbf{v} \in \, \mathcal{V},
$$

其中，$\mathbf{v}\in\mathcal{V}$ 是试验函数，$\mathbf{u} = \mathbf{\tilde{u}},\, \text{on}\, \Gamma_{D}$

## 有限元离散形式

由于时间项的引入，此时不仅要进行空间离散，也要进行时间离散

### 空间离散

设有限元解空间 $\mathcal{U}_{h}$ 的基函数为

$$
\boldsymbol{\phi}_{1},\boldsymbol{\phi}_{2},\cdots,\boldsymbol{\phi}_{N},
$$

$\boldsymbol{\phi}_{i} = \left[\phi_{x,i},\phi_{y,i},\phi_{z,i}\right]$，其中，$\phi_{x,i},\phi_{y,i},\phi_{z,i}$ 表示位移在 $x,y,z$ 方向的插值基函数，通常 $\phi_{x,i}=\phi_{y,i}=\phi_{z,i}=:\phi_{i}$，于是位移分布函数为

$$
\mathbf{u} = \sum_{i=1}^{N}\mathbf{u}_{i}\phi_{i},
$$

其中，$\mathbf{u}_{i} = \left[u_{x,i},u_{y,i},u_{z,i}\right]^{T}$. 测试函数空间 $\mathcal{V}_{h} = \mathcal{U}_{h}$，在节点 $i$ 上，测试函数选为

$$
\begin{bmatrix}
\phi_{i} \\ 0 \\ 0
\end{bmatrix},\quad 
\begin{bmatrix}
 0  \\ \phi_{i} \\ 0
\end{bmatrix},\quad
\begin{bmatrix}
 0 \\ 0 \\ \phi_{i} 
\end{bmatrix}，
$$

分别记为 $\mathbf{v}_{x,i},\mathbf{v}_{y,i},\mathbf{v}_{z,i}$

共计 $3N$ 个位移自由度 

$$
u_{x,1},u_{y,1},u_{z,1},u_{x,2},u_{y,2},u_{z,2},\cdots,u_{x,N},u_{y,N},u_{z,N},
$$

和 $3N$ 个求解方程

$$
\begin{equation}
\begin{aligned}
&\int_{\Omega}\rho\ddot{\mathbf{u}}\cdot\mathbf{v}_{*,i} \, \mathrm{d}\Omega +\int_{\Omega} \boldsymbol{\varepsilon}(\mathbf{v}_{*,i}) : \boldsymbol{\sigma} \, \mathrm{d}\Omega + \int_{\Gamma_{R}} \alpha\mathbf{u} \cdot \mathbf{v}_{*,i} \, \mathrm{d}S \\
=& \int_{\Omega}\mathbf{f}\cdot \mathbf{v}_{*,i}\,\mathrm{d}\Omega + \int_{\Gamma_{N}} \tilde{\mathbf{p}} \cdot \mathbf{v}_{*,i}\ \mathrm{d}S + \int_{\Gamma_{R}} \mathbf{f}_{R} \cdot \mathbf{v}_{*,i} \, \mathrm{d}S,\quad \forall \, \mathbf{v}_{*,i} \in \, \mathcal{V},\quad *=x,y,z;\ i=1:N.
\end{aligned}
\end{equation}
$$

在静力学求解中，空间离散完得到的是非线性的代数方程，而在动力学求解中，上述方程是一个非线性的**微分方程**

将上述方程记为

$$
\ddot{\mathbf{F}}^{\text{u}}(t)+\mathbf{F}^{\text{int}} (t)+ \mathbf{F}^{r}(t)-\mathbf{F}^{\text{ext}}(t) = \mathbf{0},
$$ (sec5-eq:fea-space)

其中
- 时间微分项向量：$\ddot{\mathbf{F}}^{\text{u}}(t):=\int_{\Omega}\rho\ddot{\mathbf{u}}\cdot\mathbf{v}_{*,i} \, \mathrm{d}\Omega$
- 内力项向量：$\mathbf{F}^{\text{int}}(t):=\int_{\Omega} \boldsymbol{\varepsilon}(\mathbf{v}_{*,i}) : \boldsymbol{\sigma} \, \mathrm{d}\Omega$
- Robin 边界条件贡献向量：$\mathbf{F}^{\text{r}}(t):=\int_{\Gamma_{R}} \alpha\mathbf{u} \cdot \mathbf{v}_{*,i} \, \mathrm{d}S$
- 外力向量：$\mathbf{F}^{\text{ext}}(t):=\int_{\Omega}\mathbf{f}\cdot \mathbf{v}_{*,i}\,\mathrm{d}\Omega + \int_{\Gamma_{N}} \tilde{\mathbf{p}} \cdot \mathbf{v}_{*,i}\ \mathrm{d}S + \int_{\Gamma_{R}} \mathbf{f}_{R} \cdot \mathbf{v}_{*,i} \, \mathrm{d}S$

类似地，在每个单元上

$$
\begin{equation}
\begin{aligned}
&\ddot{\mathbf{F}}^{\text{u}} = \int_{E} \rho\ddot{\mathbf{u}}\cdot\mathbf{v}_{*,i} \, \mathrm{d}E = \int_{E}\rho\mathbf{N}^{T}\ddot{\mathbf{u}}\ \mathbf{d}E,\\
&\mathbf{F}^{\text{int}} = \int_{E} \boldsymbol{\varepsilon}(\mathbf{v}_{*,i}) : \boldsymbol{\sigma} \, \mathrm{d}E = \int_{E}\mathbf{B}^{T}\boldsymbol{\sigma}\ \mathbf{d}E,\\
&\mathbf{F}^{r}=\int_{\Gamma_{R,E}} \alpha\mathbf{u} \cdot \mathbf{v}_{*,i} \, \mathrm{d}S=\int_{\Gamma_{R,E}} \alpha\mathbf{N}^{T}\mathbf{u}\, \mathrm{d}S,\\
&\mathbf{F}^{\text{ext}}=\int_{E}\mathbf{N}^{T}\mathbf{f}\,\mathrm{d}E + \int_{\Gamma_{N,E}} \mathbf{N}^{T}\tilde{\mathbf{p}}\ \mathrm{d}S + \int_{\Gamma_{R,E}} \mathbf{N}^{T}\mathbf{f}_{R}\, \mathrm{d}S
\end{aligned}
\end{equation}
$$

### 时间离散

接下来对方程 {eq}`sec5-eq:fea-space` 进行时间离散，对 $\ddot{\mathbf{F}}_{\text{u}}(t)$ 通常使用中心差分

$$
\ddot{\mathbf{F}}^{\text{u}}(t) \approx \frac{\mathbf{F}^{\text{u}}(t+\Delta t)-2\mathbf{F}^{\text{u}}(t)+\mathbf{F}^{\text{u}}(t-\Delta t)}{\Delta t^2},
$$

于是，方程 {eq}`sec5-eq:fea-space` 变为

$$
\frac{\mathbf{F}^{\text{u}}(t+\Delta t)-2\mathbf{F}^{\text{u}}(t)+\mathbf{F}^{\text{u}}(t-\Delta t)}{\Delta t^2}+\mathbf{F}^{\text{int}} (t)+ \mathbf{F}^{r}(t)-\mathbf{F}^{\text{ext}}(t) = \mathbf{0}.
$$

#### 显式步求解

$$
\frac{\mathbf{F}^{\text{u}}_{n+1}-2\mathbf{F}^{\text{u}}_{n}+\mathbf{F}^{\text{u}}_{n-1}}{\Delta t^2}+\mathbf{F}^{\text{int}}_{n}+ \mathbf{F}^{r}_{n}-\mathbf{F}^{\text{ext}}_{n} = \mathbf{0}.
$$

#### 隐式步求解

$$
\frac{\mathbf{F}^{\text{u}}_{n+1}-2\mathbf{F}^{\text{u}}_{n}+\mathbf{F}^{\text{u}}_{n-1}}{\Delta t^2}+\mathbf{F}^{\text{int}}_{n+1}+ \mathbf{F}^{r}_{n+1}-\mathbf{F}^{\text{ext}}_{n+1} = \mathbf{0}.
$$

通常，在求解过程中，$\Delta t$ 不是均匀分布的，此时需要使用变步长的中心差分公式