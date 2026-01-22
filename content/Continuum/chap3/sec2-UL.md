# Updated Lagrangian 格式

<span class="gray-text">
在 Updated Lagrangian 格式中，以上一为参考构型，所有量都在上一构型中度量
</span>

根据虚功原理 {eq}`sec2-eq:vw-u`，第 $t^{n+1}$ 时满足

```{margin}
$\mathbf{\hat{f}}$ 和 $\mathbf{\hat{t}}$ 表示相应构型的度量
```

$$
\int_{\Omega_{n}} \mathbf{S}^{n+1}:\delta\mathbf{E}^{n+1}\ \mathrm{d}V - \left(\int_{\Omega_{n}}\mathbf{\hat{f}}^{n+1}\cdot\delta\mathbf{u}\ \mathrm{d}V+\oint_{\Gamma_{n}}\mathbf{\hat{t}}^{n+1}\cdot\delta\mathbf{u}\ \mathrm{d}S\right) = 0
$$ (sec2-eq:UL0)

## 增量分解

**由于参考构型为上一构型 $\Omega_{n}$**，故

$$
\mathbf{u}^{n} = \mathbf{0},\quad \mathbf{u}^{n+1} = \mathbf{u}^{n} + \Delta\mathbf{u} = \Delta\mathbf{u}
$$

于是 $\mathbf{E}^{n}=\mathbf{0}$，且

$$
\begin{aligned}
\Delta\mathbf{E}&=\mathbf{E}^{n+1} - \mathbf{E}^{n} = \mathbf{E}(\mathbf{u}^{n+1}) = \mathbf{E}(\Delta\mathbf{u}) \\ &= \frac{1}{2}[\nabla_{0}\Delta\mathbf{u}+(\nabla_{0}\Delta\mathbf{u})^{T}+(\nabla_{0}\Delta\mathbf{u})^{T}\cdot(\nabla_{0}\Delta\mathbf{u})]\\
&:=\Delta\mathbf{E}^{\text{L}}+\Delta\mathbf{E}^{\text{NL}}
\end{aligned}
$$

其中

$$
\begin{aligned}
\Delta\mathbf{E}^{\text{L}}&=\frac{1}{2}[\nabla_{0}\Delta\mathbf{u}+(\nabla_{0}\Delta\mathbf{u})^{T}]\\
\Delta\mathbf{E}^{\text{NL}}&=\frac{1}{2}[(\nabla_{0}\Delta\mathbf{u})^{T}\cdot(\nabla_{0}\Delta\mathbf{u})]
\end{aligned}
$$

分别是增量的线性部分和非线性部分

**注意：参考构型是上一构型 $\Omega_{n}$，故 $\nabla_{0}$ 也是针对 $\Omega_{n}$ 的梯度**

对于 PK2 应力张量，有

$$
\mathbf{S}^{n+1} = \boldsymbol{\sigma}^{n} + \Delta\mathbf{S}
$$

其中，$\mathbf{S}^{n+1}$ 是 $t^{n+1}$ 时刻的 PK2 在构型 $\Omega_{n}$ 上的度量，$\boldsymbol{\sigma}^{n}$ 是 $t^{n}$ 时刻的 Cauchy 应力张量在构型 $\Omega_{n}$ 上的度量，$\Delta\mathbf{S}$ 被称为 Updated Kirchhoff 应力张量增量，在 $\Omega_{n}$ 上度量，是计算的中间量

由于

$$
\delta\mathbf{E}^{n+1}=\delta(\Delta\mathbf{E}) = \delta\Delta\mathbf{E}
$$

于是

$$
\begin{aligned}
\int_{\Omega_{n}} \mathbf{S}^{n+1}:\delta\mathbf{E}^{n+1}\ \mathrm{d}V &= \int_{\Omega_{n}}(\boldsymbol{\sigma}^{n} + \Delta\mathbf{S}):\delta\Delta\mathbf{E}\ \mathrm{d}V\\
&=\int_{\Omega_{n}}(\sigma^{n}_{ij} + \Delta S_{ij})(\delta\Delta E_{ij})\ \mathrm{d}V\\
&=\int_{\Omega_{n}}(\sigma^{n}_{ij}(\delta\Delta E^{\text{L}}_{ij}+\delta\Delta E^{\text{NL}}_{ij}) + \Delta S_{ij}(\delta\Delta E_{ij}))\ \mathrm{d}V
\end{aligned}
$$

记

$$
\delta R^{n+1}=\int_{\Omega_{n}}\mathbf{\hat{f}}^{n+1}\cdot\delta\mathbf{u}\ \mathrm{d}V+\oint_{\Gamma_{n}}\mathbf{\hat{t}}^{n+1}\cdot\delta\mathbf{u}\ \mathrm{d}S
$$

于是 {eq}`sec2-eq:UL0` 可以写为

$$
\int_{\Omega_{n}} \Delta S_{ij}(\delta\Delta E_{ij})+\sigma^{n}_{ij}(\delta\Delta E^{\text{L}}_{ij})+\sigma^{n}_{ij}(\delta\Delta E^{\text{NL}}_{ij})\ \mathrm{d}V - \delta R^{n+1} = 0
$$ (sec2-eq:UL1)

这是关于 $\Delta \mathbf{u}$ 的非线性方程

## 线性化

增量形式的本构方程写为

$$
\Delta S_{ij} \approx C_{ijkl}\Delta E_{kl}
$$

其中 $\Delta E$ 仍为 Green-Lagrange 应变增量

代入到方程 {eq}`sec2-eq:UL1` 得到

$$
\int_{\Omega_{n}} C_{ijkl}\Delta E_{kl}(\delta\Delta E_{ij})+\sigma^{n}_{ij}(\delta\Delta E^{\text{L}}_{ij})+\sigma^{n}_{ij}(\delta\Delta E^{\text{NL}}_{ij})\ \mathrm{d}V - \delta R^{n+1} = 0
$$ (sec2-eq:UL2)

由于 $\Delta\mathbf{E}^{\text{NL}}$ 是 $\Delta\mathbf{u}$ 的高阶无穷小量，因此

$$
\Delta E_{kl} \rightarrow \Delta E^{\text{L}}_{kl}
$$

于是方程 {eq}`sec2-eq:UL2` 写为

$$
\int_{\Omega_{n}} C_{ijkl}\Delta E_{kl}^{\text{L}}(\delta\Delta E_{ij}^{\text{L}})+\sigma^{n}_{ij}(\delta\Delta E^{\text{L}}_{ij})+\sigma^{n}_{ij}(\delta\Delta E^{\text{NL}}_{ij})\ \mathrm{d}V - \delta R^{n+1} = 0
$$ (sec2-eq:UL3)

### 变分计算

$$
\begin{aligned}
\delta\Delta\mathbf{E}^{\text{L}}&=\frac{1}{2}\delta[\nabla_{0}\Delta\mathbf{u}+(\nabla_{0}\Delta\mathbf{u})^{T}]\\
&=\frac{1}{2}[\nabla_{0}\delta\Delta\mathbf{u}+(\nabla_{0}\delta\Delta\mathbf{u})^{T}]\\
\delta\Delta\mathbf{E}^{\text{NL}}&=\frac{1}{2}\delta[(\nabla_{0}\Delta\mathbf{u})^{T}\cdot(\nabla_{0}\Delta\mathbf{u})]\\
&=\frac{1}{2}[(\nabla_{0}\delta\Delta\mathbf{u})^{T}\cdot(\nabla_{0}\Delta\mathbf{u}) + (\nabla_{0}\Delta\mathbf{u})^{T}\cdot(\nabla_{0}\delta\Delta\mathbf{u})]
\end{aligned}
$$

由于 $\Delta \mathbf{E}^{\text{L}}$ 是关于 $\mathbf{u}$ 的线性函数，因此 $\delta\Delta \mathbf{E}^{\text{L}}$ 中仅包含 $\delta\Delta\mathbf{u}$ 而不包含 $\Delta\mathbf{u}$，将自由度项置于左端，最终得到

$$
\int_{\Omega_{0}} C_{ijkl}\Delta E_{kl}^{\text{L}}(\delta\Delta E_{ij}^{\text{L}})+\sigma^{n}_{ij}(\delta\Delta E^{\text{NL}}_{ij})\ \mathrm{d}V = \delta R^{n+1} - \int_{\Omega_{0}}\sigma^{n}_{ij}(\delta\Delta E^{\text{L}}_{ij})\ \mathrm{d}V
$$ (sec1-eq:TL4)