# Total Lagrangian 格式

<span class="gray-text">
在 Total Lagrangian 格式中，所有量都在初始构型中度量
</span>


根据虚功原理 {eq}`sec2-eq:vw-u`，第 $t^{n+1}$ 时满足

$$
\int_{\Omega_{0}} \mathbf{S}^{n+1}:\delta\mathbf{E}^{n+1}\ \mathrm{d}V - \left(\int_{\Omega_{0}}\mathbf{f}_{0}^{n+1}\cdot\delta\mathbf{u}\ \mathrm{d}V+\oint_{\Gamma_{0}}\mathbf{t}_{0}^{n+1}\cdot\delta\mathbf{u}\ \mathrm{d}S\right) = 0
$$ (sec1-eq:TL0)

## 增量分解

对于 Green-Lagrange 应变张量，有

$$
\begin{aligned}
\Delta\mathbf{E}&=\mathbf{E}^{n+1} - \mathbf{E}^{n}\\
&=\frac{1}{2}[\nabla_{0}\mathbf{u}^{n+1}+(\nabla_{0}\mathbf{u}^{n+1})^{T}+(\nabla_{0}\mathbf{u}^{n+1})^{T}\cdot(\nabla_{0}\mathbf{u}^{n+1})]\\
&-\frac{1}{2}[\nabla_{0}\mathbf{u}^{n}+(\nabla_{0}\mathbf{u}^{n})^{T}+(\nabla_{0}\mathbf{u}^{n})^{T}\cdot(\nabla_{0}\mathbf{u}^{n})]
\end{aligned}
$$

代入 $\mathbf{u}^{n+1} = \mathbf{u}^{n} + \Delta\mathbf{u}$，得到

$$
\begin{aligned}
\Delta\mathbf{E} &= \frac{1}{2}[\nabla_{0}\Delta\mathbf{u}+(\nabla_{0}\Delta\mathbf{u})^{T}+(\nabla_{0}\mathbf{u}^{n})^{T}\cdot(\nabla_{0}\Delta\mathbf{u})\\
&+(\nabla_{0}\Delta\mathbf{u})^{T}\cdot(\nabla_{0}\mathbf{u}^{n})+(\nabla_{0}\Delta\mathbf{u})^{T}\cdot(\nabla_{0}\Delta\mathbf{u})]\\
&:=\Delta\mathbf{E}^{\text{L}}+\Delta\mathbf{E}^{\text{NL}}
\end{aligned}
$$

其中

$$
\begin{aligned}
\Delta\mathbf{E}^{\text{L}}&=\nabla_{0}\Delta\mathbf{u}+(\nabla_{0}\Delta\mathbf{u})^{T}+(\nabla_{0}\mathbf{u}^{n})^{T}\cdot(\nabla_{0}\Delta\mathbf{u})
+(\nabla_{0}\Delta\mathbf{u})^{T}\cdot(\nabla_{0}\mathbf{u}^{n})\\
\Delta\mathbf{E}^{\text{NL}}&=(\nabla_{0}\Delta\mathbf{u})^{T}\cdot(\nabla_{0}\Delta\mathbf{u})
\end{aligned}
$$

分别是增量的**线性部分**和**非线性部分**

$\Delta\mathbf{E}^{\text{L}}$ 也可以表示为

$$
\begin{aligned}
\Delta\mathbf{E}^{\text{L}}&=\nabla_{0}\Delta\mathbf{u}+(\nabla_{0}\Delta\mathbf{u})^{T}+(\nabla_{0}\mathbf{u}^{n})^{T}\cdot(\nabla_{0}\Delta\mathbf{u})
+(\nabla_{0}\Delta\mathbf{u})^{T}\cdot(\nabla_{0}\mathbf{u}^{n})\\
&=(\mathbf{I}+(\nabla_{0}\mathbf{u}^{n})^{T})(\nabla_{0}\Delta\mathbf{u})+(\nabla_{0}\Delta\mathbf{u})^{T}(\mathbf{I}+\nabla_{0}\mathbf{u}^{n})\\
&=(\mathbf{F}^{n})^{T}(\nabla_{0}\Delta\mathbf{u})+(\nabla_{0}\Delta\mathbf{u})^{T}\mathbf{F}^{n}
\end{aligned}
$$

对于 PK2 应力张量，有

$$
\mathbf{S}^{n+1} = \mathbf{S}^{n} + \Delta\mathbf{S}
$$

由于

$$
\delta\mathbf{E}^{n+1}=\delta(\mathbf{E}^{n}+\Delta\mathbf{E}) = \delta\Delta\mathbf{E}
$$

于是

$$
\begin{aligned}
\int_{\Omega_{0}} \mathbf{S}^{n+1}:\delta\mathbf{E}^{n+1}\ \mathrm{d}V &= \int_{\Omega_{0}}(\mathbf{S}^{n} + \Delta\mathbf{S}):\delta\Delta\mathbf{E}\ \mathrm{d}V\\
&=\int_{\Omega_{0}}(S^{n}_{ij} + \Delta S_{ij})(\delta\Delta E_{ij})\ \mathrm{d}V\\
&=\int_{\Omega_{0}}(S^{n}_{ij}(\delta\Delta E^{\text{L}}_{ij}+\delta\Delta E^{\text{NL}}_{ij}) + \Delta S_{ij}(\delta\Delta E_{ij}))\ \mathrm{d}V
\end{aligned}
$$

记

$$
\delta R^{n+1}=\int_{\Omega_{0}}\mathbf{f}_{0}^{n+1}\cdot\delta\mathbf{u}\ \mathrm{d}V+\oint_{\Gamma_{0}}\mathbf{t}_{0}^{n+1}\cdot\delta\mathbf{u}\ \mathrm{d}S
$$

于是 {eq}`sec1-eq:TL0` 可以写为

$$
\int_{\Omega_{0}} \Delta S_{ij}(\delta\Delta E_{ij})+S^{n}_{ij}(\delta\Delta E^{\text{L}}_{ij})+S^{n}_{ij}(\delta\Delta E^{\text{NL}}_{ij})\ \mathrm{d}V - \delta R^{n+1} = 0
$$ (sec1-eq:TL1)

## 线性化

**假设从 $\Omega^{n}$ 到 $\Omega^{n+1}$ 的载荷增量很小，于是 $\Delta\mathbf{u}$ 也很小**，故

$$
\Delta\mathbf{S}\approx\mathbb{C}:\Delta\mathbf{E}\quad \text{or}\quad \Delta S_{ij} \approx C_{ijkl}\Delta E_{kl}
$$


其中，$\mathbb{C}$ 是材料模型的瞬时刚度模量，对于线弹性模型，退化为 Hooke 定律

代入本构关系得到

$$
\int_{\Omega_{0}} C_{ijkl}\Delta E_{kl}(\delta\Delta E_{ij})+S^{n}_{ij}(\delta\Delta E^{\text{L}}_{ij})+S^{n}_{ij}(\delta\Delta E^{\text{NL}}_{ij})\ \mathrm{d}V - \delta R^{n+1} = 0
$$ (sec1-eq:TL2)

由于 $\Delta\mathbf{E}^{\text{NL}}$ 是 $\Delta\mathbf{u}$ 的高阶无穷小量，因此

$$
\Delta E_{kl} \approx \Delta E^{\text{L}}_{kl}
$$

于是方程 {eq}`sec1-eq:TL2` 写为

$$
\int_{\Omega_{0}} C_{ijkl}\Delta E_{kl}^{\text{L}}(\delta\Delta E_{ij}^{\text{L}})+S^{n}_{ij}(\delta\Delta E^{\text{L}}_{ij})+S^{n}_{ij}(\delta\Delta E^{\text{NL}}_{ij})\ \mathrm{d}V - \delta R^{n+1} = 0
$$ (sec1-eq:TL3)