# 一致性切线模量

<span class="gray-text">
一致性切线模量与算法匹配，若使用非算法相关（直接从本构方程计算）的理论弹塑性模量，则牛顿迭代可能收敛缓慢甚至发散
</span>

一致性切线模量（也称为**算法切线模量**）反映了应力对总应变的线性化增量关系，能够准确描述材料在弹塑性等非线性行为下的刚度变化。**在非线性有限元分析中，Jacobian 矩阵的计算采用一致性切线模量，可以显著提高全局非线性迭代的收敛速度和数值稳定性**。因此，在本构积分后，计算并返回一致性切线模量是实现高效、稳健的有限元求解的关键步骤

一致性切线模量定义为

```{margin}
区别于 $\mathbf{D}_{ep}^{\text{theo}}=\frac{\partial \boldsymbol{\sigma}}{\partial \boldsymbol{\varepsilon}}$
```

$$
\mathbf{D}_{ep}^{\text{alg}}=\frac{\partial \boldsymbol{\sigma}_{n+1}}{\partial \boldsymbol{\varepsilon}_{n+1}}.
$$

下简记为 $\mathbf{D}$


## 弹塑性材料

对于弹塑性材料，在已知前一步内变量 $\boldsymbol{\alpha}_{n}$ 和当前步总应变 $\boldsymbol{\varepsilon}_{n+1}$ 的情况下，通常通过本构积分算法来更新应力。这个过程自然定义了一个算子形式的增量本构函数 $\hat{\boldsymbol{\sigma}}$，即

$$
\boldsymbol{\sigma}_{n+1}=\hat{\boldsymbol{\sigma}}(\boldsymbol{\alpha}_{n},\boldsymbol{\varepsilon}_{n+1})
$$

有限应变塑性理论中，常常使用乘子应变分解，即

$$
\mathbf{F} = \mathbf{F}^{e}\cdot\mathbf{F}^{p},
$$

其中
- $\mathbf{F}$ 是总变形梯度
- $\mathbf{F}^{e}$ 是弹性变形梯度
- $\mathbf{F}^{p}$ 是塑性变形梯度

因此在有限应变塑性中，不定义总非线性应变 $\boldsymbol{\varepsilon}_{n+1}$，但弹性试应变 $\boldsymbol{\varepsilon}_{n+1}^{e,\text{trail}}$ 仍自然出现在弹性预测-塑性校正算法中。由于 

$$
\boldsymbol{\varepsilon}_{n+1}^{e,\text{trail}} = \boldsymbol{\varepsilon}_{n}^{e} + \Delta\boldsymbol{\varepsilon}_{n+1} = \boldsymbol{\varepsilon}_{n} - \boldsymbol{\varepsilon}_{n}^{p} + \Delta\boldsymbol{\varepsilon}_{n+1} = \boldsymbol{\varepsilon}_{n+1} - \boldsymbol{\varepsilon}_{n}^{p},
$$

因此，将 $\boldsymbol{\sigma}_{n+1}$ 表示为 $\boldsymbol{\varepsilon}_{n+1}^{e,\text{trail}}$ 的函数

$$
\boldsymbol{\sigma}_{n+1}=\bar{\boldsymbol{\sigma}}(\boldsymbol{\alpha}_{n},\boldsymbol{\varepsilon}_{n+1}^{e,\text{trail}})=\hat{\boldsymbol{\sigma}}(\boldsymbol{\alpha}_{n},\boldsymbol{\varepsilon}_{n+1}^{e,\text{trail}}+\boldsymbol{\varepsilon}_{n}^{p})=\hat{\boldsymbol{\sigma}}(\boldsymbol{\alpha}_{n},\boldsymbol{\varepsilon}_{n+1}),
$$

此时有

$$
\mathbf{D} = \frac{\partial \hat{\boldsymbol{\sigma}}}{\partial \boldsymbol{\varepsilon}_{n+1}} = \frac{\partial \hat{\boldsymbol{\sigma}}}{\partial \boldsymbol{\varepsilon}_{n+1}^{e,\text{trail}}} = \frac{\partial \bar{\boldsymbol{\sigma}}}{\partial \boldsymbol{\varepsilon}_{n+1}^{e,\text{trail}}}.
$$

为了使小应变塑性模型和有限应变塑性模型拥有形式一致的一致性切线模量，我们采用如下形式

$$
\mathbf{D} = \frac{\partial \hat{\boldsymbol{\sigma}}}{\partial \boldsymbol{\varepsilon}_{n+1}^{e,\text{trail}}} = \frac{\partial \bar{\boldsymbol{\sigma}}}{\partial \boldsymbol{\varepsilon}_{n+1}^{e,\text{trail}}}.
$$

### 分段性

$\hat{\boldsymbol{\sigma}}$ 是一个分段函数，当

- $\Phi^{\text{trial}} < 0$，则 $\hat{\boldsymbol{\sigma}}$ 随着弹性曲线演化，此时 $\mathbf{D} = \mathbf{D}^{e}$
- $\Phi^{\text{trial}} > 0$，则 $\hat{\boldsymbol{\sigma}}$ 随着塑性曲线演化，此时 $\mathbf{D} = \mathbf{D}^{ep}$
- $\Phi^{\text{trial}} = 0$，则可能发生弹性卸载，或发生塑性演化，在切换点处，$\hat{\boldsymbol{\sigma}}$ 不可微

## Mises 屈服准则和各向同性硬化准则

接下来以 Mises 屈服准则和各向同性硬化准则为例，介绍一致性切线模量 $\mathbf{D}$ 的计算过程，根据 [return mapping 算法](./sec1-returnmapping.md)，有

$$
\begin{equation}
\begin{aligned}
\boldsymbol{\sigma}_{n+1}=\left(\mathbf{D}^e - \frac{6G^{2}\Delta\gamma}{q^{\text{trial}}}\mathbf{I}_{d}\right) : \boldsymbol{\varepsilon}^{e, \text{trial}},
\end{aligned}
\end{equation}
$$

其中，$q^{\text{trial}}=\sqrt{3J_{2}(\mathbf{s}^{\text{trial}})} = \sqrt{\frac{3}{2}}\|\mathbf{s}^{\text{trial}}\|$，$\Delta\gamma$ 是方程

$$
\begin{equation}
q^{\text{trial}}-3G\Delta\gamma-\sigma_{y}(\bar{\varepsilon}_n^p + \Delta \gamma)=0
\end{equation}
$$ (sec2-eq:yield)

的解，于是

$$
\begin{equation}
\begin{aligned}
\frac{\partial \boldsymbol{\sigma}_{n+1}}{\partial \boldsymbol{\varepsilon}^{e, \text{trial}}}
=
\mathbf{D}^e
-
\frac{\Delta \gamma \, 6 G^2}{q^{\text{trial}}} \mathbf{I}_d
-
\frac{6 G^2}{q^{\text{trial}}} \boldsymbol{\varepsilon}^{e, \text{trial}}_{d}
\otimes
\frac{\partial \Delta \gamma}{\partial \boldsymbol{\varepsilon}^{e, \text{trial}}}
\\
+
\frac{\Delta \gamma \, 6 G^2}{(q^{\text{trial}})^2} \boldsymbol{\varepsilon}^{e, \text{trial}}_{d}
\otimes
\frac{\partial q^{\text{trial}}}{\partial \boldsymbol{\varepsilon}^{e, \text{trial}}},
\end{aligned}
\end{equation}
$$

其中，$\boldsymbol{\varepsilon}^{e, \text{trial}}_{d} = \text{dev}(\boldsymbol{\varepsilon}^{e, \text{trial}}) = \mathbf{I}_{d}:\boldsymbol{\varepsilon}^{e, \text{trial}}$

由于

$$
q^{\text{trial}} = \sqrt{\frac{3}{2}}\|\mathbf{s}^{\text{trial}}\| = 2G\sqrt{\frac{3}{2}}\|\mathbf{I}_{d}:\boldsymbol{\varepsilon}^{e,\text{trial}}\|,
$$

故

$$
\begin{equation}
\frac{\partial q^{\text{trial}}}{\partial \boldsymbol{\varepsilon}^{e, \text{trial}}}=2G\sqrt{\frac{3}{2}}\frac{\mathbf{s}^{\text{trial}}}{\|\mathbf{s}^{\text{trial}}\|}=2G\sqrt{\frac{3}{2}}\frac{\boldsymbol{\varepsilon}^{e, \text{trial}}_{d}}{\|\boldsymbol{\varepsilon}^{e, \text{trial}}_{d}\|}.
\end{equation}
$$

此外，根据式 {eq}`sec2-eq:yield`，有

$$
\frac{\partial q^{\text{trial}}}{\partial \boldsymbol{\varepsilon}^{e, \text{trial}}}-3G\frac{\partial \Delta\gamma}{\partial \boldsymbol{\varepsilon}^{e, \text{trial}}}-\frac{\partial \sigma_{y}(\bar{\varepsilon}_n^p + \Delta \gamma)}{\partial \boldsymbol{\varepsilon}^{e, \text{trial}}}=0,
$$

可从上式求解出 $\frac{\partial \Delta\gamma}{\partial \boldsymbol{\varepsilon}^{e, \text{trial}}}$，

