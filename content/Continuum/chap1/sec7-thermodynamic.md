# 热力学原理

*热力学第一定律：系统总能量的变化率等于外力所做功的变化率与热量输入的变化率之和*

## 能量方程

### 空间描述

根据热力学第一定律，有

$$
\frac{\mathrm{d}}{\mathrm{d}t}\int_{\Omega}\rho\epsilon\mathrm{d}v=W_{\text{net}}+H_{\text{net}}
$$ (sec7-eq:thermo)

其中，$\epsilon$ 是存储在单位质量的总能量，$W_{\text{net}}$ 是输入到系统中的净功率，$H_{\text{net}}$ 是输入到系统中的净热传递速率

单位质量的总储存能量 $\epsilon$ 包含内能和动能

$$
\epsilon = e_{c} + \frac{1}{2}(\mathbf{v}\cdot\mathbf{v})
$$

$e_{c}$ 为单位质量的内能，是所有微观能量形式的总和，$\frac{1}{2}(\mathbf{v}\cdot\mathbf{v})$ 是动能

在连续体没有体偶的情况下，输入功率 $W_{\text{net}}$ 可以表示为

$$
\begin{aligned}
W_{\text{net}}&=\oint_{\Gamma}\mathbf{t}\cdot\mathbf{v}\mathrm{d}s+\int_{\Omega}\mathbf{f}\cdot\mathbf{v}\mathrm{d}v
\end{aligned}
$$

由于

$$
\nabla\cdot(\boldsymbol{\sigma}\mathbf{v})=\left(\nabla \cdot \boldsymbol{\sigma}\right) \cdot \mathbf{v}+\boldsymbol{\sigma}:\nabla\mathbf{v},
$$

故由 $\boldsymbol{\sigma}$ 的对称性，再结合散度定理，得到

$$
\begin{aligned}
\oint_{\Gamma}\mathbf{t}\cdot\mathbf{v}\mathrm{d}s &= \oint_{\Gamma}\boldsymbol{\sigma}\mathbf{n}\cdot\mathbf{v}\mathrm{d}s=\oint_{\Gamma}(\boldsymbol{\sigma}\mathbf{v})\cdot\mathbf{n}\mathrm{d}s\\
&=\int_{\Omega}\nabla\cdot(\boldsymbol{\sigma}\mathbf{v})\mathrm{d}s\\
&=\int_{\Omega}\left((\nabla \cdot \boldsymbol{\sigma}) \cdot \mathbf{v}+\boldsymbol{\sigma}:\nabla\mathbf{v}\right)\mathrm{d}s
\end{aligned}
$$

结合线动量守恒方程 {eq}`sec6-eq:linear-momentum-local`，有

$$
\begin{aligned}
W_{\text{net}}&=\int_{\Omega}[(\nabla \cdot \boldsymbol{\sigma}+\mathbf{f}) \cdot \mathbf{v}+\boldsymbol{\sigma}:\nabla\mathbf{v}]\mathrm{d}v\\
&=\int_{\Omega}[\rho\frac{\mathrm{d}\mathbf{v}}{\mathrm{d}t} \cdot \mathbf{v}+\boldsymbol{\sigma}:\nabla\mathbf{v}]\mathrm{d}v
\end{aligned}
$$

由于 $\boldsymbol{\sigma}$ 是对称的，故

$$
\boldsymbol{\sigma}:\nabla\mathbf{v}=\boldsymbol{\sigma}:\frac{1}{2}[\nabla\mathbf{v} + (\nabla\mathbf{v})^{T}] = \boldsymbol{\sigma}:\mathbf{d},
$$

再结合 Reynolds 输运定理 {eq}`sec6-eq:reynolds`

$$
\int_{\Omega}\rho\frac{\mathrm{d}\mathbf{v}}{\mathrm{d}t} \cdot \mathbf{v}\mathrm{d}v = \frac{1}{2}\int_{\Omega}\rho\frac{\mathrm{d}}{\mathrm{d}t} (\mathbf{v}\cdot \mathbf{v})\mathrm{d}v = \frac{1}{2}\frac{\mathrm{d}}{\mathrm{d}t}\int_{\Omega}\rho\mathbf{v}\cdot \mathbf{v}\mathrm{d}v
$$

最终，$W_{\text{net}}$ 可以写为

$$
W_{\text{net}}=\frac{1}{2}\frac{\mathrm{d}}{\mathrm{d}t}\int_{\Omega}\rho\mathbf{v}\cdot \mathbf{v}\mathrm{d}v+\int_{\Omega}\boldsymbol{\sigma}:\mathbf{d}\mathrm{d}v
$$

净热传递速率 $H_{\text{net}}$ 可以表示为

$$
H_{\text{net}}=-\oint_{\Gamma}\mathbf{q}\cdot\mathbf{n}\mathrm{d}s+\int_{\Omega}g\mathrm{d}v=\int_{\Omega}(-\nabla\cdot\mathbf{q}+g)\mathrm{d}v
$$

其中，$\mathbf{q}$ 是热流量，$g$ 是单位体积内的内部热源项

最终，热力学第一定律 {eq}`sec7-eq:thermo` 可以写为

$$
\frac{\mathrm{d}}{\mathrm{d}t}\int_{\Omega}\rho(e_{c} + \frac{1}{2}(\mathbf{v}\cdot\mathbf{v}))\mathrm{d}v=\frac{1}{2}\frac{\mathrm{d}}{\mathrm{d}t}\int_{\Omega}\rho\mathbf{v}\cdot \mathbf{v}\mathrm{d}v+\int_{\Omega}(\boldsymbol{\sigma}:\mathbf{d}-\nabla\cdot\mathbf{q}+g)\mathrm{d}v
$$

结合 Reynolds 输运定理 {eq}`sec6-eq:reynolds`，化简得到

$$
0=\int_{\Omega}(\rho\frac{\mathrm{d}e_{c}}{\mathrm{d}t}-\boldsymbol{\sigma}:\mathbf{d}+\nabla\cdot\mathbf{q}-g)\mathrm{d}v
$$

由于 $\Omega$ 的任意性，得到其局部形式

$$
\rho\frac{\mathrm{d}e_{c}}{\mathrm{d}t}=\boldsymbol{\sigma}:\mathbf{d}-\nabla\cdot\mathbf{q}+g
$$

也被称为热力学形式，其中 $\boldsymbol{\sigma}:\mathbf{d}$ 被称为应力功，$\mathbf{q}$ 可以写为

$$
\mathbf{q}=-\mathbf{k}\cdot\nabla T
$$

其中，$\mathbf{k}$ 是二阶热传导张量，$T$ 是温度

### 物质描述

将每一项分别使用物质描述表示

$$
\begin{aligned}
\int_{\Omega}\rho\epsilon\mathrm{d}v&=\int_{\Omega_{0}}\rho_{0}(e_{c}+ \frac{1}{2}(\mathbf{V}\cdot\mathbf{V}))\mathrm{d}V
\end{aligned}
$$

输入功率项

$$
\begin{aligned}
W_{\text{net}}&=\int_{\Omega}\left[\frac{1}{2}\rho\frac{\mathrm{d}}{\mathrm{d}t}(\mathbf{v}\cdot \mathbf{v})+\boldsymbol{\sigma}:\nabla\mathbf{v}\right]\mathrm{d}v\\
&=\int_{\Omega_{0}}\left[\frac{1}{2}\rho_{0}\frac{\partial}{\partial t}(\mathbf{V}\cdot \mathbf{V})+\mathbf{P}:\nabla_{0}\mathbf{V}\right]\mathrm{d}V
\end{aligned}
$$

## 焓不等式
