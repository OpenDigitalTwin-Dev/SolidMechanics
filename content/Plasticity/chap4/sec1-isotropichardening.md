# 各向同性硬化模型

<span class="gray-text">
各向同性硬化模型假设屈服函数是应力的各向同性函数，即在整个塑性变形过程中，屈服面以其中心为原点（位置不变），保持形状不变地向外均匀膨胀，反映了材料在各个方向上的屈服行为一致
</span>

在整个变形过程中，屈服面是应力的各向同性函数，并假设屈服函数的数学形式保持不变，同时通过引入与变形历史相关的标量参数 $K$ 来定义当前屈服面的大小，即

$$
f(\boldsymbol{\sigma},K) = 0,
$$

其中

$$
K = K(\vartheta),
$$

$\vartheta$ 是历史变形参数，通常取为一般化的塑性应变

$$
\vartheta = \int_0^t \left( 2 \mathbf{D}^p : \mathbf{D}^p \right)^{1/2} dt.
$$

根据持续塑性变形的一致性条件，应力状态应始终在屈服面上

$$
\dot{f} = \frac{\partial f}{\partial \boldsymbol{\sigma}} : \overset{\nabla}{\boldsymbol{\tau}} + \frac{\partial f}{\partial K} \frac{\partial K}{\partial \vartheta} \dot{\vartheta} = 0,
$$

由于

$$
\dot{\vartheta} = \left( 2 \mathbf{D}^p : \mathbf{D}^p \right)^{1/2} = \frac{1}{H} \left( 2 \frac{\partial f}{\partial \boldsymbol{\sigma}} : \frac{\partial f}{\partial \boldsymbol{\sigma}} \right)^{1/2} \left( \frac{\partial f}{\partial \boldsymbol{\sigma}} : \overset{\nabla}{\boldsymbol{\tau}} \right),
$$

代入到上式，得到

$$
H = -\frac{\partial f}{\partial K} \frac{dK}{d\vartheta} \left( 2 \frac{\partial f}{\partial \boldsymbol{\sigma}} : \frac{\partial f}{\partial \boldsymbol{\sigma}} \right)^{1/2}.
$$

## $J_{2}$ 塑性流动理论

使用 [von Mises 类屈服准则](../chap2/sec2-mises.md)

$$
f = J_{2} - k^2(\vartheta) = 0,\quad J_{2} = \frac{1}{2}\mathbf{s}:\mathbf{s},
$$

由于

$$
\frac{\partial f}{\partial \boldsymbol{\sigma}} = \frac{\partial J_{2}}{\partial\boldsymbol{\sigma}} = \mathbf{s},
$$

```{admonition} 证明
:class: tip, dropdown

$$
J_{2} = \frac{1}{2}s_{ij}^{2},
$$

其中

$$
s_{ij} = \sigma_{ij} - \frac{1}{3}\text{tr}(\boldsymbol{\sigma})\delta_{ij},
$$

故

$$
\frac{\partial J_{2}}{\partial \sigma_{kl}} = s_{ij}\frac{\partial s_{ij}}{\partial \sigma_{kl}} = s_{ij}(\delta_{ik}\delta_{jl} - \frac{1}{3}\delta_{ij}\delta_{kl}),
$$

由于

$$
\begin{equation}
\begin{aligned}
s_{ij}\delta_{ik}\delta_{jl} &= s_{kl},\\
s_{ij}\delta_{ij}\delta_{kl} &= s_{ii}\delta_{kl} = 0,
\end{aligned}
\end{equation}
$$

因此

$$
\frac{\partial J_{2}}{\partial \sigma_{kl}} = s_{kl},
$$

即

$$
\frac{\partial J_{2}}{\partial\boldsymbol{\sigma}} = \mathbf{s}.
$$

```

因此

$$
H=2k\frac{\mathrm{d}k}{\mathrm{d} \vartheta}(2\mathbf{s}:\mathbf{s}) = 4k\frac{\mathrm{d}k}{\mathrm{d} \vartheta}\sqrt{J_{2}},
$$

由于材料在屈服面上，有 $J_{2} = k^2(\vartheta)$，故

$$
H=4k^2\frac{\mathrm{d}k}{\mathrm{d} \vartheta},
$$

其中，$h_{\text{t}}^{\text{p}}=\frac{\mathrm{d}k}{\mathrm{d} \vartheta}$ 是**纯剪切变形中的塑性切线模量**

根据式 {eq}`(intro-eq:strain-p)`，得到

$$
\mathbf{D}^{\text{p}} = \frac{1}{H} \left( \frac{\partial f}{\partial \boldsymbol{\sigma}} : \overset{\nabla}{\boldsymbol{\tau}} \right) \frac{\partial f}{\partial \boldsymbol{\sigma}} = \frac{1}{H} \left( \mathbf{s} : \overset{\nabla}{\boldsymbol{\tau}} \right) \mathbf{s},
$$

因此，$\text{tr}(\mathbf{D}^{\text{p}}) = 0$，这表明塑性部分的体积应变率为零

由于

$$
\begin{equation}
\begin{aligned}
\mathbf{D}^{\text{p}} &= \frac{1}{4k^2h_{\text{t}}^{\text{p}}}(\mathbf{s}\otimes\mathbf{s}):\overset{\nabla}{\boldsymbol{\tau}}\\
&=\frac{1}{2h_{\text{t}}^{\text{p}}}\frac{\mathbf{s}\otimes\mathbf{s}}{\mathbf{s}:\mathbf{s}}:\overset{\nabla}{\boldsymbol{\tau}},
\end{aligned}
\end{equation}
$$

因此，总应变率张量为

$$
\mathbf{D} = \left(\mathbf{M}^{\text{e}} + \frac{1}{2h_{\text{t}}^{\text{p}}}\frac{\mathbf{s}\otimes\mathbf{s}}{\mathbf{s}:\mathbf{s}}\right):\overset{\nabla}{\boldsymbol{\tau}}.
$$

其逆形式为

$$
\overset{\nabla}{\boldsymbol{\tau}} = \left( \boldsymbol{\Lambda}^{\text{e}} - \frac{2\mu}{1 + h_{\text{t}}^{\text{p}}/\mu} \frac{\mathbf{s}\otimes\mathbf{s}}{\mathbf{s} : \mathbf{s}} \right) : \mathbf{D}.
$$

$\mathbf{D}^{\text{p}}$ 可以写为

$$
\\
\mathbf{D}^{\text{p}}=\frac{1}{2h_{\text{t}}^{\text{p}}}\frac{\mathbf{s}\otimes\mathbf{s}}{\mathbf{s}:\mathbf{s}}:\overset{\nabla}{\boldsymbol{\tau}}=\frac{1}{2h_{\text{t}}^{\text{p}}}\frac{\mathbf{s}:\overset{\nabla}{\boldsymbol{\tau}}}{\mathbf{s}:\mathbf{s}}\ \mathbf{s},
$$ 

由于

$$
\mathbf{s}:\overset{\nabla}{\boldsymbol{\tau}} =\frac{2h_{\text{t}}^{\text{p}}}{1+h_{\text{t}}^{\text{p}}/\mu}\ \mathbf{s}:\mathbf{D},
$$

故

$$
\mathbf{D}^{\text{p}}=\frac{1}{1+h_{\text{t}}^{\text{p}}/\mu}\ \frac{\mathbf{s}:\mathbf{D}}{\mathbf{s}:\mathbf{s}}\ \mathbf{s}.
$$

```{admonition} 证明
:class: tip, dropdown

由于

$$
\mathbf{s}:\overset{\nabla}{\boldsymbol{\tau}} = \mathbf{s}:\left( \boldsymbol{\Lambda}^{\text{e}} : \mathbf{D} - \frac{2\mu}{1 + h_{\text{t}}^{\text{p}}/\mu} \frac{\mathbf{s}\otimes\mathbf{s}}{\mathbf{s} : \mathbf{s}} : \mathbf{D} \right),
$$ (sec1-eq:eq1)

由于

$$
\left(\mathbf{I}^{s}:\mathbf{D}\right)_{ij} =  \frac{1}{2} (\delta_{ik}\delta_{jl} + \delta_{il}\delta_{jk})D_{kl} = \frac{1}{2}(D_{ij} + D_{ji}) = D_{ij},
$$

且

$$
\left(\mathbf{I}\otimes\mathbf{I}\right):\mathbf{D} = \text{tr}(\mathbf{D})\mathbf{I},
$$

因此，式{eq}`sec1-eq:eq1`中的第一项

$$
\begin{equation}
\begin{aligned}
\mathbf{s}:\left( \boldsymbol{\Lambda}^{\text{e}} : \mathbf{D}\right) &= \mathbf{s}:\left(2\mu \mathbf{I}^{s}: \mathbf{D}+\lambda \mathbf{I}\otimes\mathbf{I}: \mathbf{D}\right)\\
&=\mathbf{s}:\left(2\mu\mathbf{D} + \lambda\text{tr}(\mathbf{D})\mathbf{I}\right)\\
&=2\mu(\mathbf{s}:\mathbf{D}).
\end{aligned}
\end{equation}
$$

对于第二项

$$
\mathbf{s}:\frac{\mathbf{s}\otimes\mathbf{s}}{\mathbf{s} : \mathbf{s}} : \mathbf{D} = \mathbf{s}:\frac{\mathbf{s}:\mathbf{D}}{\mathbf{s} : \mathbf{s}}:\mathbf{s} = \mathbf{s}:\mathbf{D},
$$

因此

$$
\begin{equation}
\begin{aligned}
\mathbf{s}:\overset{\nabla}{\boldsymbol{\tau}} &= 2\mu(1 - \frac{1}{1 + h_{\text{t}}^{\text{p}}/\mu})\ \mathbf{s}:\mathbf{D}\\
&=\frac{2h_{\text{t}}^{\text{p}}}{1+h_{\text{t}}^{\text{p}}/\mu}\ \mathbf{s}:\mathbf{D}.
\end{aligned}
\end{equation}
$$


```

在硬化范围的塑性加载阶段，有

$$
\frac{\partial f}{\partial \boldsymbol{\sigma}} : \overset{\nabla}{\boldsymbol{\tau}} = \mathbf{s}:\overset{\nabla}{\boldsymbol{\tau}} > 0,
$$

因此，在 $\mu>0$ 和 $h_{\text{t}}^{\text{p}}>0$ 时

$$
\mathbf{s}:\mathbf{D}>0.
$$
