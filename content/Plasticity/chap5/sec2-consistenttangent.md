# 一致性切线模量

<span class="gray-text">
一致性切线模量与算法匹配，若使用非算法相关（直接从本构方程计算）的理论弹塑性模量，则牛顿迭代可能收敛缓慢甚至发散
</span>


## 连续切线模量

[连续切线模量](../chap3/sec1-tangent.md)是从材料的本构关系直接推导出的数学上的切线刚度，它描述了在无限小的应变增量下，应力增量和应变增量之间的瞬时关系，代表了材料应力-应变曲线在某个点的真实斜率

$$
\begin{equation}
\frac{\partial \dot{\boldsymbol{\sigma}}}{\partial \dot{\boldsymbol{\varepsilon}}}
\end{equation}
$$

然而，在有限元求解非线性问题的 Newton-Raphson 迭代过程中，应力更新通常采用**本构积分算法**，使得实际使用的本构方程成为理想本构关系在时间上的离散形式。因此，如果仍然使用连续切线模量来计算 Jacobian 矩阵，会导致其与实际数值算法不一致，进而影响收敛性，表现为收敛速度降低甚至出现发散现象

## 一致性切线模量

一致性切线模量（也称为**算法切线模量**）反映了数值算法中应力对总应变的线性化增量关系，**用于非线性有限元分析 Jacobian 矩阵的计算中，以显著提高全局非线性迭代的收敛速度和数值稳定性**。因此，在本构积分后，计算并返回一致性切线模量是实现高效、稳健的有限元求解的关键步骤

一致性切线模量定义为

```{margin}
区别于 $\mathbf{D}_{ep}^{\text{theo}}=\frac{\partial \boldsymbol{\sigma}}{\partial \boldsymbol{\varepsilon}}$
```

$$
\mathbf{D}_{ep}^{\text{alg}}=\frac{\partial \boldsymbol{\sigma}_{n+1}}{\partial \boldsymbol{\varepsilon}_{n+1}}.
$$

下简记为 $\mathbf{D}$

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

### 各向同性硬化的 Mises 屈服准则

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
$$ (sec2-eq:tar-der)

其中，$\boldsymbol{\varepsilon}^{e, \text{trial}}_{d} = \text{dev}(\boldsymbol{\varepsilon}^{e, \text{trial}}) = \mathbf{I}_{d}:\boldsymbol{\varepsilon}^{e, \text{trial}}$

由于

$$
q^{\text{trial}} = \sqrt{\frac{3}{2}}\|\mathbf{s}^{\text{trial}}\| = 2G\sqrt{\frac{3}{2}}\|\mathbf{I}_{d}:\boldsymbol{\varepsilon}^{e,\text{trial}}\|=2G\sqrt{\frac{3}{2}}\|\boldsymbol{\varepsilon}^{e, \text{trial}}_{d}\|,
$$ (sec2-eq:q)

故

$$
\begin{equation}
\frac{\partial q^{\text{trial}}}{\partial \boldsymbol{\varepsilon}^{e, \text{trial}}}=2G\sqrt{\frac{3}{2}}\frac{\mathbf{s}^{\text{trial}}}{\|\mathbf{s}^{\text{trial}}\|}=2G\sqrt{\frac{3}{2}}\frac{\boldsymbol{\varepsilon}^{e, \text{trial}}_{d}}{\|\boldsymbol{\varepsilon}^{e, \text{trial}}_{d}\|}.
\end{equation}
$$ (sec2-eq:q-der)

此外，根据式 {eq}`sec2-eq:yield`，有

$$
\frac{\partial q^{\text{trial}}}{\partial \boldsymbol{\varepsilon}^{e, \text{trial}}}-3G\frac{\partial \Delta\gamma}{\partial \boldsymbol{\varepsilon}^{e, \text{trial}}}-\frac{\partial \sigma_{y}(\bar{\varepsilon}_n^p + \Delta \gamma)}{\partial \boldsymbol{\varepsilon}^{e, \text{trial}}}=0,
$$ (sec2-eq:hardening-der)

一般地，可从上式求解出 $\frac{\partial \Delta\gamma}{\partial \boldsymbol{\varepsilon}^{e, \text{trial}}}$，对于线性硬化模型，有

$$
\sigma_{y}(\bar{\varepsilon}_n^p + \Delta \gamma) = \sigma_{0} + H\cdot(\bar{\varepsilon}_n^p + \Delta \gamma),
$$

得到

$$
\frac{\partial \sigma_{y}(\bar{\varepsilon}_n^p + \Delta \gamma)}{\partial \boldsymbol{\varepsilon}^{e, \text{trial}}} = H\frac{\partial \Delta\gamma}{\partial \boldsymbol{\varepsilon}^{e, \text{trial}}},
$$

故，代入式 {eq}`sec2-eq:hardening-der` 中，得到

$$
\begin{equation}
\frac{\partial \Delta\gamma}{\partial \boldsymbol{\varepsilon}^{e, \text{trial}}} = \frac{1}{3G+H}\frac{\partial q^{\text{trial}}}{\partial \boldsymbol{\varepsilon}^{e, \text{trial}}} = \frac{2G}{3G+H}\sqrt{\frac{3}{2}}\frac{\mathbf{s}^{\text{trial}}}{\|\mathbf{s}^{\text{trial}}\|}.
\end{equation}
$$ (sec2-eq:gamma-der)

记

$$
\mathbf{\bar{N}} = \frac{\mathbf{s}^{\text{trial}}}{\|\mathbf{s}^{\text{trial}}\|} = \frac{\boldsymbol{\varepsilon}^{e, \text{trial}}_{d}}{\|\boldsymbol{\varepsilon}^{e, \text{trial}}_{d}\|},
$$

将式 {eq}`sec2-eq:q-der` 和式 {eq}`sec2-eq:gamma-der` 代入到 {eq}`sec2-eq:tar-der`，并结合式 {eq}`sec2-eq:q` 得到

$$
\begin{equation}
\begin{aligned}
\mathbf{D}=
\frac{\partial \boldsymbol{\sigma}_{n+1}}{\partial \boldsymbol{\varepsilon}^{e, \text{trial}}}
&=
\mathbf{D}^e
-
\frac{\Delta \gamma \, 6 G^2}{q^{\text{trial}}} \mathbf{I}_d
+
6G^2\left(\frac{\Delta\gamma}{q^{\text{trial}}}-\frac{1}{3G+H}\right)\mathbf{\bar{N}}\otimes\mathbf{\bar{N}},
\end{aligned}
\end{equation}
$$

此处，$\mathbf{D}$ 是对称的

#### 连续切线模量

对于各向同性硬化

$$
\sigma_{y}(\bar{\varepsilon}^p) = \sigma_{0} + \kappa(\bar{\varepsilon}^p),
$$

有

$$
\boldsymbol{\alpha} = \{\bar{\varepsilon}_{n}^{p}\},\quad \mathbf{A} = \{\kappa\},
$$

故

$$
\begin{equation}
\frac{\partial^2 \psi^p}{\partial \boldsymbol{\alpha}^2}=\frac{\partial \psi^p}{\partial {\bar{\varepsilon}^{p}}^{2}}=\frac{\partial \kappa}{\partial \bar{\varepsilon}^{p}} = H(\bar{\varepsilon}^{p}),
\end{equation}
$$

对于线性硬化，有 $H(\bar{\varepsilon}^{p}) \equiv H$. 此外，对于 Mises 屈服准则，有

$$
\mathbf{H} = -\frac{\partial \Phi}{\partial \mathbf{A}} = -\frac{\partial \Phi}{\partial \kappa} = 1
$$

且对于关联塑性流动，有

$$
\mathbf{N} = \frac{\partial \Phi}{\partial \boldsymbol{\sigma}},
$$

于是

$$
\begin{equation}
\begin{aligned}
\mathbf{D}^{ep}_{c} &= \mathbf{D}^{e} - \frac{(\mathbf{D}^{e}:\mathbf{N})\otimes(\mathbf{D}^{e}:\frac{\partial \Phi}{\partial \boldsymbol{\sigma}})}{\frac{\partial \Phi}{\partial \boldsymbol{\sigma}}:\mathbf{D}^{e}:\mathbf{N}-\frac{\partial \Phi}{\partial \mathbf{A}}\frac{\partial^2 \psi^p}{\partial \boldsymbol{\alpha}^2}\mathbf{H}}\\
&=\mathbf{D}^{e} - \frac{(\mathbf{D}^{e}:\mathbf{N})\otimes(\mathbf{D}^{e}:\mathbf{N})}{\mathbf{N}:\mathbf{D}^{e}:\mathbf{N}+H}
\end{aligned}
\end{equation}
$$

由于 $\mathbf{N}$ 是偏张量，故

$$
\mathbf{D}^{e}:\mathbf{N} = 2G\mathbf{N}\quad \Longrightarrow\quad \mathbf{N}:\mathbf{D}^{e}:\mathbf{N} = 3G,
$$

最终，连续切线模量化简为

```{margin}
$\bar{\mathbf{N}}=\sqrt{\frac{2}{3}}\mathbf{N}$
```

$$
\mathbf{D}^{ep}_{c} =\mathbf{D}^{e} - \frac{6G^2}{3G+H}\bar{\mathbf{N}}\otimes\bar{\mathbf{N}}.
$$

连续切线模量与一致性切线模量关系如下

$$
\mathbf{D}=\mathbf{D}_{c}^{ep}-\frac{\Delta \gamma \, 6 G^2}{q^{\text{trial}}}\left[\mathbf{I}_d-\bar{\mathbf{N}}\otimes\bar{\mathbf{N}}\right],
$$

当 $\Delta\gamma\rightarrow0$ 时，$\mathbf{D}_{c}^{ep}\rightarrow\mathbf{D}$；然而，当 $\Delta\gamma$ 较大（例如时间步长较大时），$\mathbf{D}{c}^{ep}$ 将逐渐偏离 $\mathbf{D}$。如果此时仍继续采用 $\mathbf{D}_{c}^{ep}$，可能会导致明显的数值不一致性，从而影响牛顿迭代的收敛性，甚至导致收敛速度显著降低

### 一般情形