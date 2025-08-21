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

计算屈服函数 $\Phi^{\text{trial}}=f^{\text{trial}}$，若 $f^{\text{trial}} \leq 0$：则步长内为弹性变形，接受预测值：

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
&\boldsymbol{\varepsilon}^{e}_{n+1} = \boldsymbol{\varepsilon}^{e, \text{trial}} - \Delta\gamma\mathbf{N}_{n+1},\\
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
\dot{\boldsymbol{\varepsilon}}^{p} = \dot{\gamma}\mathbf{N}=\dot{\gamma}\frac{\partial f}{\partial \boldsymbol{\sigma}},
$$

### 各向同性硬化

$\boldsymbol{\alpha}$ 选为 $\bar{\varepsilon}^{p}$，Mises 屈服函数为

$$
f(\boldsymbol{\sigma},\bar{\varepsilon}^{p})=\sqrt{\frac{3}{2}}\|\mathbf{s}\|-\sigma_{y}(\bar{\varepsilon}^{p}),
$$

此时 $\mathbf{N} = \sqrt{\frac{3}{2}} \frac{\mathbf{s}}{\|\mathbf{s}\|}$，结合关联流动法则，有

$$
\dot{\bar{\varepsilon}}^{p}=\sqrt{\frac{2}{3}}\|\dot{\boldsymbol{\varepsilon}}^{p}\|=\sqrt{\frac{2}{3}}\|\dot{\gamma}\mathbf{N}\| =\dot{\gamma},
$$

其离散形式为

$$
\bar{\varepsilon}_{n+1}^p = \bar{\varepsilon}_n^p + \Delta \gamma,
$$

因此，求解方程组为

$$
\begin{equation}
\begin{aligned}
\boldsymbol{\varepsilon}^{e}_{n+1} &= \boldsymbol{\varepsilon}^{e, \text{trial}} - \Delta\gamma\mathbf{N}_{n+1},\\
\bar{\varepsilon}_{n+1}^p &= \bar{\varepsilon}_n^p + \Delta \gamma,\\
f_{n+1}&=\sqrt{\frac{3}{2}}\|\mathbf{s}_{n+1}\|-\sigma_{y}(\bar{\varepsilon}^{p}_{n+1})=0,
\end{aligned}
\end{equation}
$$

求解变量为

$$
\boldsymbol{\varepsilon}_{n+1}^{e},\quad \bar{\varepsilon}_{n+1}^p,\quad \Delta \gamma
$$

#### 方程组求解

这一非线性方程组可使用 Newton-Raphson 方法进行求解：

记 $\mathbf{v} = \left[\boldsymbol{\varepsilon}=\boldsymbol{\varepsilon}_{n+1}^{e},\bar{\varepsilon}=\bar{\varepsilon}_{n+1}^p,\Delta \gamma\right]^{T}$，

记 $\mathbf{r}=\left[\mathbf{r}_{\boldsymbol{\varepsilon}},r_{\bar{\varepsilon}},r_{f}\right]^{T}$，其中

$$
\begin{equation}
\begin{aligned}
\mathbf{r}_{\boldsymbol{\varepsilon}} &= \boldsymbol{\varepsilon}^{e}_{n+1} - \boldsymbol{\varepsilon}^{e, \text{trial}} + \Delta\gamma\mathbf{N}_{n+1},\\
r_{\bar{\varepsilon}}&=\bar{\varepsilon} - \bar{\varepsilon}_n^p - \Delta \gamma,\\
r_{f}&=\sqrt{\frac{3}{2}}\|\mathbf{s}_{n+1}\|-\sigma_{y}(\varepsilon),
\end{aligned}
\end{equation}
$$

于是，Jacobian 矩阵为

$$
\begin{equation}
\mathbf{J} = \frac{\partial \mathbf{r}}{\partial \mathbf{v}}=
\begin{bmatrix}
\frac{\partial \mathbf{r}_{\boldsymbol{\varepsilon}}}{\partial \boldsymbol{\varepsilon}} & \frac{\partial \mathbf{r}_{\boldsymbol{\varepsilon}}}{\partial \bar{\varepsilon}} & \frac{\partial \mathbf{r}_{\boldsymbol{\varepsilon}}}{\partial \Delta \gamma} \\
\frac{\partial r_{\bar{\varepsilon}}}{\partial \boldsymbol{\varepsilon}} & \frac{\partial r_{\bar{\varepsilon}}}{\partial \bar{\varepsilon}} & \frac{\partial r_{\bar{\varepsilon}}}{\partial \Delta \gamma} \\
\frac{\partial r_{f}}{\partial \boldsymbol{\varepsilon}} & \frac{\partial r_{f}}{\partial \bar{\varepsilon}} & \frac{\partial r_{f}}{\partial \Delta \gamma}
\end{bmatrix}.
\end{equation}
$$

初值可选为 $\mathbf{v}^{(0)}=\left[\boldsymbol{\varepsilon}^{e, \text{trial}},\bar{\varepsilon}_{n}^p,0\right]$. 注意，$\bar{\varepsilon}_{n}^p$ 使用的是当前时间步上一个外层非线性迭代的结果

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
\mathbf{D}^e:(\Delta\gamma\mathbf{N}_{n+1})=\mathbf{D}^e:(\Delta\boldsymbol{\varepsilon}^{p})=2G\text{dev}(\Delta\boldsymbol{\varepsilon}^{p})=2G\Delta\boldsymbol{\varepsilon}^{p}=2G\Delta\gamma\mathbf{N}_{n+1},
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
$$ (sec1-eq:gamma)

对于线性硬化，如

$$
\sigma_{y}(\bar{\varepsilon}_n^p + \Delta \gamma) = \sigma_{0} + H(\bar{\varepsilon}_n^p + \Delta \gamma),
$$

方程 {eq}`sec1-eq:gamma` 是线性的；对于非线性硬化，方程是非线性的，通常使用 Newton-Rapshon 求解

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

$\boldsymbol{\alpha}$ 选为 $\boldsymbol{\beta}$，Mises 屈服函数为

$$
f(\boldsymbol{\sigma},\boldsymbol{\beta})=\sqrt{\frac{3}{2}}\|\mathbf{s}-\boldsymbol{\beta}\|-\sigma_{y},
$$

此时 $\mathbf{N} = \sqrt{\frac{3}{2}} \frac{\mathbf{s}-\boldsymbol{\beta}}{\|\mathbf{s}-\boldsymbol{\beta}\|}$，根据 Prager 运动硬化公式

$$
\mathrm{d}\boldsymbol{\beta}=C\mathrm{d}\gamma\mathbf{N}_{n+1},
$$

其中，$C$ 是运动硬化模量，其离散形式为

$$
\boldsymbol{\beta}_{n+1}=\boldsymbol{\beta}_{n} + C\Delta\gamma\mathbf{N}_{n+1},
$$

因此，求解方程组为

$$
\begin{equation}
\begin{aligned}
\boldsymbol{\varepsilon}^{e}_{n+1} &= \boldsymbol{\varepsilon}^{e, \text{trial}} - \Delta\gamma\mathbf{N}_{n+1},\\
\boldsymbol{\beta}_{n+1}&=\boldsymbol{\beta}_{n} + C\Delta\gamma\mathbf{N}_{n+1},\\
f_{n+1}&=\sqrt{\frac{3}{2}}\|\mathbf{s}_{n+1}-\boldsymbol{\beta}_{n+1}\|-\sigma_{y}=0,
\end{aligned}
\end{equation}
$$

求解变量为

$$
\boldsymbol{\varepsilon}^{e}_{n+1},\quad \boldsymbol{\beta}_{n+1},\quad \Delta \gamma
$$

使用 Newton-Raphson 方法求解方程组，初值可选为 $\mathbf{v}^{(0)}=\left[\boldsymbol{\varepsilon}^{e, \text{trial}},\boldsymbol{\alpha}_{n},0\right]$. 注意，$\boldsymbol{\alpha}_{n}$ 使用的是当前时间步上一个外层非线性迭代的结果

### 混合硬化

$\boldsymbol{\alpha}$ 选为 $\{\bar{\varepsilon}^{p},\boldsymbol{\beta}\}$，Mises 屈服函数为

$$
f(\boldsymbol{\sigma},\boldsymbol{\beta},\bar{\varepsilon}^{p})=\sqrt{\frac{3}{2}}\|\mathbf{s} - \boldsymbol{\beta}\|-\sigma_{y}(\bar{\varepsilon}^{p}),
$$

此时 $\mathbf{N} = \sqrt{\frac{3}{2}} \frac{\mathbf{s}-\boldsymbol{\beta}}{\|\mathbf{s}-\boldsymbol{\beta}\|}$，结合各向同性硬化和 Prager 运动硬化公式，得到求解方程组为

$$
\begin{equation}
\begin{aligned}
\boldsymbol{\varepsilon}^{e}_{n+1} &= \boldsymbol{\varepsilon}^{e, \text{trial}} - \Delta\gamma\mathbf{N}_{n+1},\\
\bar{\varepsilon}_{n+1}^p &= \bar{\varepsilon}_n^p + \Delta \gamma,\\
\boldsymbol{\beta}_{n+1}&=\boldsymbol{\beta}_{n} + C\Delta\gamma\mathbf{N}_{n+1},\\
f_{n+1}&=\sqrt{\frac{3}{2}}\|\mathbf{s}_{n+1}-\boldsymbol{\beta}_{n+1}\|-\sigma_y \left( \bar{\varepsilon}_{n+1}^p \right)=0,
\end{aligned}
\end{equation}
$$

求解变量为

$$
\boldsymbol{\varepsilon}^{e}_{n+1},\quad \bar{\varepsilon}_{n+1}^p,\quad \boldsymbol{\beta}_{n+1},\quad \Delta \gamma
$$


使用 Newton-Raphson 方法求解方程组，初值可选为 $\mathbf{v}^{(0)}=\left[\boldsymbol{\varepsilon}^{e,\text{trial}},\bar{\varepsilon}_{n}^p,\boldsymbol{\beta}_{n},0\right]$. 注意，$\bar{\varepsilon}_{n}^p,\boldsymbol{\beta}_{n}$ 使用的是当前时间步上一个外层非线性迭代的结果

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

