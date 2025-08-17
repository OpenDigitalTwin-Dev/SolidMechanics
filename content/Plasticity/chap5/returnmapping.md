# Return Mapping Algorithm

Return Mapping Algorithm（返回映射算法）是解决弹塑性材料本构积分问题的一种特定的、高效和鲁棒的数值积分策略，其核心思想是将复杂的弹塑性本构积分问题分解成两个更简单的步骤：

- **弹性预测**：假设在时间步长内，材料行为完全是弹性的，计算试应力
- **塑性修正**：检查试应力是否超出屈服面，若超出，则将应力拉回更新后的屈服面

## 弹性预测

假设整个步长是弹性的，则

```{margin}
**应力是由弹性形变产生的**
```

$$
\begin{equation}
\begin{aligned}
&\boldsymbol{\varepsilon}^{e, \text{trial}} = \boldsymbol{\varepsilon}_n^e + \Delta \boldsymbol{\varepsilon},\\
&\boldsymbol{\sigma}^{\text{trial}} = \mathbf{D}^e : \boldsymbol{\varepsilon}^{e, \text{trial}} = \boldsymbol{\sigma}_n + \mathbf{D}^e : \Delta \boldsymbol{\varepsilon}.
\end{aligned}
\end{equation}
$$

同时塑性应变和硬化模量不变

$$
\boldsymbol{\varepsilon}_{n+1}^{p, \text{trial}} = \boldsymbol{\varepsilon}_n^p, \quad \bar{\varepsilon}_{n+1}^{p, \text{trial}} = \bar{\varepsilon}_n^p,
$$

计算屈服函数$f^{\text{trial}}$，若 $f^{\text{trial}} \leq 0$：则步长内为弹性变形，接受预测值：

$$
\boldsymbol{\sigma}_{n+1} = \boldsymbol{\sigma}^{\text{trial}}, \quad
\boldsymbol{\varepsilon}_{n+1}^p = \boldsymbol{\varepsilon}_n^p, \quad
\bar{\varepsilon}_{n+1}^p = \bar{\varepsilon}_n^p.
$$

否则，进入塑性修正阶段

## 塑性修正

塑性修正的目标是将应力状态拉回到更新后的屈服面上，即找到 $t_{n+1}$ 时刻满足下述方程的应力状态

$$
\begin{equation}
\begin{aligned}
&\boldsymbol{\varepsilon}^{e}_{n+1} = \boldsymbol{\varepsilon}^{e, \text{trial}} - \Delta\gamma\mathbf{n}_{n+1},\\
&\boldsymbol{\alpha}_{n+1} = \boldsymbol{\alpha}_{n} + \Delta\gamma\mathbf{H}(\boldsymbol{\sigma}_{n+1},\mathbf{A}_{n+1}),\\
&\Phi(\boldsymbol{\sigma}_{n+1}, \mathbf{A}_{n+1}) = 0,\\
&\Delta\gamma\geq0,
\end{aligned}
\end{equation}
$$

上述方程组对于变量 $\boldsymbol{\varepsilon}^{e}_{n+1},\boldsymbol{\alpha}_{n+1},\Delta\gamma$ 封闭

接下来以 Mises 屈服准则和关联流动法则为例，考虑小变形假设的情形

**Mises 屈服函数**

$$
f(\boldsymbol{\sigma},\boldsymbol{\alpha},\bar{\varepsilon}^{p})=\sqrt{\frac{3}{2}}\|\mathbf{s} - \boldsymbol{\alpha}\|-\sigma_{y}(\bar{\varepsilon}^{p}),
$$

**关联流动法则**

$$
\dot{\boldsymbol{\varepsilon}}^{p} = \dot{\gamma}\mathbf{n}=\dot{\gamma}\frac{\partial f}{\partial \boldsymbol{\sigma}},
$$

### 各向同性硬化

Mises 屈服函数为

$$
f(\boldsymbol{\sigma},\bar{\varepsilon}^{p})=\sqrt{\frac{3}{2}}\|\mathbf{s}\|-\sigma_{y}(\bar{\varepsilon}^{p}),
$$

此时 $\mathbf{n} = \sqrt{\frac{3}{2}} \frac{\mathbf{s}}{\|\mathbf{s}\|}$，结合关联流动法则，有

$$
\dot{\bar{\varepsilon}}^{p}=\sqrt{\frac{2}{3}}\|\dot{\boldsymbol{\varepsilon}}^{p}\|=\sqrt{\frac{2}{3}}\|\dot{\gamma}\mathbf{n}\| =\dot{\gamma},
$$

其离散形式为

$$
\bar{\varepsilon}_{n+1}^p = \bar{\varepsilon}_n^p + \Delta \gamma,
$$

因此，求解方程组为

$$
\begin{equation}
\begin{aligned}
\boldsymbol{\sigma}_{n+1} &= \boldsymbol{\sigma}^{\text{trial}} - \Delta\gamma\mathbf{D}^e :\mathbf{n}_{n+1},\\
\bar{\varepsilon}_{n+1}^p &= \bar{\varepsilon}_n^p + \Delta \gamma,\\
f_{n+1}&=\sqrt{\frac{3}{2}}\|\mathbf{s}_{n+1}\|-\sigma_{y}(\bar{\varepsilon}^{p}_{n+1})=0,
\end{aligned}
\end{equation}
$$

求解变量为

$$
\boldsymbol{\sigma}_{n+1},\quad \bar{\varepsilon}_{n+1}^p,\quad \Delta \gamma
$$

#### 方程组求解

这一非线性方程组可使用 Newton-Raphson 方法进行求解：

记 $\mathbf{v} = \left[\boldsymbol{\sigma}=\boldsymbol{\sigma}_{n+1},\varepsilon=\bar{\varepsilon}_{n+1}^p,\Delta \gamma\right]^{T}$，

记 $\mathbf{r}=\left[\mathbf{r}_{\boldsymbol{\sigma}},r_{\varepsilon},r_{f}\right]^{T}$，其中

$$
\begin{equation}
\begin{aligned}
\mathbf{r}_{\boldsymbol{\sigma}} &= \boldsymbol{\sigma} - \boldsymbol{\sigma}^{\text{trial}} + \Delta\gamma\mathbf{D}^e : \mathbf{n}_{n+1},\\
r_{\varepsilon}&=\varepsilon - \bar{\varepsilon}_n^p - \Delta \gamma,\\
r_{f}&=\sqrt{\frac{3}{2}}\|\mathbf{s}_{n+1}\|-\sigma_{y}(\varepsilon),
\end{aligned}
\end{equation}
$$

于是，Jacobian 矩阵为

$$
\begin{equation}
\mathbf{J} = \frac{\partial \mathbf{r}}{\partial \mathbf{v}}=
\begin{bmatrix}
\frac{\partial \mathbf{r}_{\boldsymbol{\sigma}}}{\partial \boldsymbol{\sigma}} & \frac{\partial \mathbf{r}_{\boldsymbol{\sigma}}}{\partial \varepsilon} & \frac{\partial \mathbf{r}_{\boldsymbol{\sigma}}}{\partial \Delta \gamma} \\
\frac{\partial r_{\varepsilon}}{\partial \boldsymbol{\sigma}} & \frac{\partial r_{\varepsilon}}{\partial \varepsilon} & \frac{\partial r_{\varepsilon}}{\partial \Delta \gamma} \\
\frac{\partial r_{f}}{\partial \boldsymbol{\sigma}} & \frac{\partial r_{f}}{\partial \varepsilon} & \frac{\partial r_{f}}{\partial \Delta \gamma}
\end{bmatrix}.
\end{equation}
$$

初值可选为 $\mathbf{v}^{(0)}=\left[\boldsymbol{\sigma}^{\text{trial}},\bar{\varepsilon}_{n}^p,0\right]$. 注意，$\bar{\varepsilon}_{n}^p$ 使用的是当前时间步上一个外层非线性迭代的结果

#### 单方程简化

Newton-Raphson 方法可以用于求解一般的非线性方程组。然而，由于在每一个高斯积分点都需要对非线性方程组进行求解，尤其在三维情况下，方程的维数达到 8，非线性求解的难度也较大，因此计算代价非常高。在某些特定情况下，可以通过消元，将方程组简化为单个方程，从而降低求解的复杂度

由于塑性流动不可压，因此

$$
\text{tr}(\dot{\boldsymbol{\varepsilon}})=0\quad \Longrightarrow\quad \text{tr}(\Delta\boldsymbol{\varepsilon})=0，
$$

故

$$
\mathbf{D}^e:\Delta\boldsymbol{\varepsilon} = 2G\ \text{dev}(\Delta\boldsymbol{\varepsilon})+K\text{tr}(\Delta\boldsymbol{\varepsilon})\mathbf{I}=2G\ \text{dev}(\Delta\boldsymbol{\varepsilon}),
$$

其中，$\text{dev}(\cdot)$ 表示偏张量的部分，由于 $\text{dev}(\Delta\boldsymbol{\varepsilon}^{p})=\Delta\boldsymbol{\varepsilon}^{p}$，故

$$
\mathbf{D}^e:(\Delta\gamma\mathbf{n}_{n+1})=\mathbf{D}^e:(\Delta\boldsymbol{\varepsilon}^{p})=2G\text{dev}(\Delta\boldsymbol{\varepsilon}^{p})=2G\Delta\boldsymbol{\varepsilon}^{p}=2G\Delta\gamma\mathbf{n}_{n+1},
$$

于是

$$
\boldsymbol{\sigma}_{n+1} = \boldsymbol{\sigma}^{\text{trial}} - 2G\Delta\gamma\sqrt{\frac{3}{2}} \frac{\mathbf{s}_{n+1}}{\|\mathbf{s}_{n+1}\|},
$$

从而

$$
\mathbf{s}_{n+1} = \mathbf{s}^{\text{trial}} - 2G\Delta\gamma\sqrt{\frac{3}{2}} \frac{\mathbf{s}_{n+1}}{\|\mathbf{s}_{n+1}\|},
$$

这表明 $\mathbf{s}_{n+1}$ 和 $\mathbf{s}^{\text{trial}}$ 同向，因此

$$
\frac{\mathbf{s}_{n+1}}{\|\mathbf{s}_{n+1}\|}=\frac{\mathbf{s}^{\text{trial}}}{\|\mathbf{s}^{\text{trial}}\|},
$$

于是

```{margin}
由于 $\mathbf{s}^{\text{trial}}$ 是常值，因此 $\mathbf{s}_{n+1}$ 是关于 $\Delta\gamma$ 的线性函数
```

$$
\mathbf{s}_{n+1} = \left(1-\frac{\sqrt{6}G\Delta\gamma}{\|\mathbf{s}^{\text{trial}}\|}\right)\mathbf{s}^{\text{trial}},
$$


将上式和 $\bar{\varepsilon}_{n+1}^p = \bar{\varepsilon}_n^p + \Delta \gamma$ 代入到屈服面函数，得到关于 $\Delta\gamma$ 的方程

$$
\sqrt{\frac{3}{2}}\left(\|\mathbf{s}^{\text{trial}}\|-\sqrt{6}G\Delta\gamma\right)-\sigma_{y}(\bar{\varepsilon}_n^p + \Delta \gamma)=0,
$$

即

$$
\sqrt{\frac{3}{2}}\|\mathbf{s}^{\text{trial}}\|-3G\Delta\gamma-\sigma_{y}(\bar{\varepsilon}_n^p + \Delta \gamma)=0.
$$

对于线性硬化，该方程是线性的，对于非线性硬化，方程是非线性的，通常使用 Newton-Rapshon 求解

```{admonition} $\boldsymbol{\sigma}_{n+1} = \boldsymbol{\sigma}_{n+1}(\Delta\gamma)$
:class: tip, dropdown

$$
\begin{equation}
\begin{aligned}
\boldsymbol{\sigma}_{n+1} &= \boldsymbol{\sigma}^{\text{trial}} - 2G\Delta\gamma\sqrt{\frac{3}{2}} \frac{\mathbf{s}_{n+1}}{\|\mathbf{s}_{n+1}\|}\\
&=\mathbf{D}^e : \boldsymbol{\varepsilon}^{e, \text{trial}} - \sqrt{6}G\Delta\gamma\frac{\mathbf{s}^{\text{trial}}}{\|\mathbf{s}^{\text{trial}}\|}
\end{aligned}
\end{equation}
$$

由于

$$
\boldsymbol{\sigma}^{\text{trial}} = \mathbf{D}^{e}:\boldsymbol{\varepsilon}^{e,\text{trial}}
$$

因此

$$
\begin{equation}
\begin{aligned}
\text{dev}(\boldsymbol{\sigma}^{\text{trial}}) + \frac{1}{3}\text{tr}(\boldsymbol{\sigma}^{\text{trial}})\mathbf{I} &= \mathbf{D}^{e}:(\text{dev}(\boldsymbol{\varepsilon}^{e,\text{trial}}) + \frac{1}{3}\text{tr}(\boldsymbol{\varepsilon}^{e,\text{trial}})\mathbf{I})
\end{aligned}
\end{equation}
$$

又

$$
\begin{equation}
\begin{aligned}
\mathbf{D}^{e}:\text{tr}(\boldsymbol{\varepsilon}^{e,\text{trial}})\mathbf{I} = \text{tr}(\boldsymbol{\sigma}^{\text{trial}})\mathbf{I}
\end{aligned}
\end{equation}
$$

故

$$
\begin{equation}
\begin{aligned}
\mathbf{s}^{\text{trial}}&=\text{dev}(\boldsymbol{\sigma}^{\text{trial}}) = \mathbf{D}^{e}:\text{dev}(\boldsymbol{\varepsilon}^{e,\text{trial}})\\
&=2G\text{dev}(\boldsymbol{\varepsilon}^{e,\text{trial}}) = 2G\mathbf{I}_{d}:\boldsymbol{\varepsilon}^{e,\text{trial}}
\end{aligned}
\end{equation}
$$

其中，$\mathbf{I}_{d}$ 是因此**偏张量投影张量**，于是

$$
\begin{equation}
\begin{aligned}
\boldsymbol{\sigma}_{n+1}=\left(\mathbf{D}^e - \frac{2\sqrt{6}G^{2}\Delta\gamma}{\|\mathbf{s}^{\text{trial}}\|}\mathbf{I}_{d}\right) : \boldsymbol{\varepsilon}^{e, \text{trial}}
\end{aligned}
\end{equation}
$$

由于 $\|\mathbf{s}^{\text{trial}}\| = \sqrt{2J_{2}(\mathbf{s}^{\text{trial}})} = \sqrt{\frac{2}{3}}\cdot\sqrt{3J_{2}(\mathbf{s}^{\text{trial}})}$，代入上式最终得到

$$
\begin{equation}
\begin{aligned}
\boldsymbol{\sigma}_{n+1}=\left(\mathbf{D}^e - \frac{6G^{2}\Delta\gamma}{\sqrt{3J_{2}(\mathbf{s}^{\text{trial}})}}\mathbf{I}_{d}\right) : \boldsymbol{\varepsilon}^{e, \text{trial}}
\end{aligned}
\end{equation}
$$

其中，$\sqrt{3J_{2}(\mathbf{s}^{\text{trial}})}$ 是试验等效应力

```

### 运动硬化

Mises 屈服函数为

$$
f(\boldsymbol{\sigma},\boldsymbol{\alpha})=\sqrt{\frac{3}{2}}\|\mathbf{s}-\boldsymbol{\alpha}\|-\sigma_{y},
$$

此时 $\mathbf{n} = \sqrt{\frac{3}{2}} \frac{\mathbf{s}-\boldsymbol{\alpha}}{\|\mathbf{s}-\boldsymbol{\alpha}\|}$，根据 Prager 运动硬化公式

$$
\mathrm{d}\boldsymbol{\alpha}=C\mathrm{d}\gamma\mathbf{n}_{n+1},
$$

其中，$C$ 是运动硬化模量，其离散形式为

$$
\boldsymbol{\alpha}_{n+1}=\boldsymbol{\alpha}_{n} + C\Delta\gamma\mathbf{n}_{n+1},
$$

因此，求解方程组为

$$
\begin{equation}
\begin{aligned}
\boldsymbol{\sigma}_{n+1} &= \boldsymbol{\sigma}^{\text{trial}} - \Delta\gamma\mathbf{D}^e :\mathbf{n}_{n+1},\\
\boldsymbol{\alpha}_{n+1}&=\boldsymbol{\alpha}_{n} + C\Delta\gamma\mathbf{n}_{n+1},\\
f_{n+1}&=\sqrt{\frac{3}{2}}\|\mathbf{s}_{n+1}-\boldsymbol{\alpha}_{n+1}\|-\sigma_{y}=0,
\end{aligned}
\end{equation}
$$

求解变量为

$$
\boldsymbol{\sigma}_{n+1},\quad \boldsymbol{\alpha}_{n+1},\quad \Delta \gamma
$$

使用 Newton-Raphson 方法求解方程组，初值可选为 $\mathbf{v}^{(0)}=\left[\boldsymbol{\sigma}^{\text{trial}},\boldsymbol{\alpha}_{n},0\right]$. 注意，$\boldsymbol{\alpha}_{n}$ 使用的是当前时间步上一个外层非线性迭代的结果

### 混合硬化

此时，Mises 屈服函数为

$$
f(\boldsymbol{\sigma},\boldsymbol{\alpha},\bar{\varepsilon}^{p})=\sqrt{\frac{3}{2}}\|\mathbf{s} - \boldsymbol{\alpha}\|-\sigma_{y}(\bar{\varepsilon}^{p}),
$$

此时 $\mathbf{n} = \sqrt{\frac{3}{2}} \frac{\mathbf{s}-\boldsymbol{\alpha}}{\|\mathbf{s}-\boldsymbol{\alpha}\|}$，结合各向同性硬化和 Prager 运动硬化公式，得到求解方程组为

$$
\begin{equation}
\begin{aligned}
\boldsymbol{\sigma}_{n+1} &= \boldsymbol{\sigma}^{\text{trial}} - \Delta\gamma\mathbf{D}^e :\mathbf{n}_{n+1},\\
\bar{\varepsilon}_{n+1}^p &= \bar{\varepsilon}_n^p + \Delta \gamma,\\
\boldsymbol{\alpha}_{n+1}&=\boldsymbol{\alpha}_{n} + C\Delta\gamma\mathbf{n}_{n+1},\\
f_{n+1}&=\sqrt{\frac{3}{2}}\|\mathbf{s}_{n+1}-\boldsymbol{\alpha}_{n+1}\|-\sigma_y \left( \bar{\varepsilon}_{n+1}^p \right)=0,
\end{aligned}
\end{equation}
$$

求解变量为

$$
\boldsymbol{\sigma}_{n+1},\quad \bar{\varepsilon}_{n+1}^p,\quad \boldsymbol{\alpha}_{n+1},\quad \Delta \gamma
$$


使用 Newton-Raphson 方法求解方程组，初值可选为 $\mathbf{v}^{(0)}=\left[\boldsymbol{\sigma}^{\text{trial}},\bar{\varepsilon}_{n}^p,\boldsymbol{\alpha}_{n},0\right]$. 注意，$\bar{\varepsilon}_{n}^p,\boldsymbol{\alpha}_{n}$ 使用的是当前时间步上一个外层非线性迭代的结果

## 一致性切线模量 $\mathbf{C}_{ep}^{\text{alg}}$

```{margin}
一致性切线模量与算法匹配，若使用非算法相关的理论弹塑性模量 $\mathbf{C}_{ep}^{\text{theo}}$，则牛顿迭代肯能够收敛缓慢甚至发散
```

一致性切线模量（也称为**算法切线模量**）反映了应力对总应变的线性化增量关系，能够准确描述材料在弹塑性等非线性行为下的刚度变化。**在非线性有限元分析中，Jacobian 矩阵的计算采用一致性切线模量，可以显著提高全局非线性迭代的收敛速度和数值稳定性**。因此，在本构积分后，计算并返回一致性切线模量是实现高效、稳健的有限元求解的关键步骤

一致性切线模量定义为

$$
\mathbf{D}_{ep}^{\text{alg}}=\frac{\partial \boldsymbol{\sigma}_{n+1}}{\partial \boldsymbol{\varepsilon}_{n+1}}.
$$

### 弹性材料

对于弹性材料，有

$$
\mathbf{D}_{ep}^{\text{alg}} = \mathbf{D}^{e} = 2\mu \mathbf{I}^{s}+\lambda \mathbf{I}\otimes\mathbf{I}.
$$

### 弹塑性材料

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
\mathbf{D}_{ep}^{\text{alg}} = \frac{\partial \hat{\boldsymbol{\sigma}}}{\partial \boldsymbol{\varepsilon}_{n+1}} = \frac{\partial \hat{\boldsymbol{\sigma}}}{\partial \boldsymbol{\varepsilon}_{n+1}^{e,\text{trail}}} = \frac{\partial \bar{\boldsymbol{\sigma}}}{\partial \boldsymbol{\varepsilon}_{n+1}^{e,\text{trail}}}.
$$

为了使小应变塑性模型和有限应变塑性模型拥有形式一致的一致性切线模量，我们采用如下形式

$$
\mathbf{D}_{ep}^{\text{alg}} =\frac{\partial \bar{\boldsymbol{\sigma}}}{\partial \boldsymbol{\varepsilon}_{n+1}^{e,\text{trail}}}
$$

## 求解注记

### $\Delta\gamma$ 的正值

虽然方程要求满足 $\dot{\gamma}(t)>0$，但在求解过程中仍有可能出现收敛到 $\Delta\gamma<0$ 的情况，这在常规材料与基础塑性模型中不太可能出现，但在复杂本构中可能出现。这样的解在物理上没有意义，必须舍弃，且需通过一定的策略进行修正

### 非线性求解

对于一些本构模型，return mapping 方程的非线性通常很强，这使得 Newton 类方法的收敛域很小，此时必须采用如初值优化，线搜索等策略提升收敛性能

## 其他算法

### Closest Point Projection

### The Generalised Trapezoidal Return Mapping

### The Generalised Midpoint Return Mapping

### The Cutting-Plane Return Mapping

