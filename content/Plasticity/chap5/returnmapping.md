# Return Mapping Algorithm

Return Mapping Algorithm（返回映射算法）是解决弹塑性材料本构积分问题的一种特定的、高效和鲁棒的数值积分策略，其核心思想是将复杂的弹塑性本构积分问题分解成两个更简单的步骤：

- **弹性预测**：假设在时间步长内，材料行为完全是弹性的，计算试应力
- **塑性修正**：检查试应力是否超出屈服面，若超出，则将应力拉回更新后的屈服面

以 Mises 屈服准则和关联流动法则为例，考虑小变形假设，故

**Mises 屈服函数**

$$
f(\boldsymbol{\sigma},\boldsymbol{\alpha},\bar{\varepsilon}^{p})=\sqrt{\frac{3}{2}}\|\mathbf{s} - \boldsymbol{\alpha}\|-\sigma_{y}(\bar{\varepsilon}^{p}),
$$

**关联流动法则**

$$
\dot{\boldsymbol{\varepsilon}}^{p}=\dot{\gamma}\frac{\partial f}{\partial \boldsymbol{\sigma}} = \dot{\gamma}\mathbf{n},
$$

## 弹性预测

假设整个步长是弹性的，则

```{margin}
**应力是由弹性形变产生的**
```

$$
\begin{equation}
\begin{aligned}
&\boldsymbol{\varepsilon}_{n+1}^{e, \text{trial}} = \boldsymbol{\varepsilon}_n^e + \Delta \boldsymbol{\varepsilon},\\
&\boldsymbol{\sigma}^{\text{trial}} = \mathbf{C}^e : \boldsymbol{\varepsilon}_{n+1}^{e, \text{trial}} = \boldsymbol{\sigma}_n + \mathbf{C}^e : \Delta \boldsymbol{\varepsilon}.
\end{aligned}
\end{equation}
$$

同时塑性应变和硬化模量不变

$$
\boldsymbol{\varepsilon}_{n+1}^{p, \text{trial}} = \boldsymbol{\varepsilon}_n^p, \quad \bar{\varepsilon}_{n+1}^{p, \text{trial}} = \bar{\varepsilon}_n^p,
$$

计算屈服函数

$$
f^{\text{trial}} = \sqrt{\frac{3}{2}} \left\| \mathbf{s}^{\text{trial}} \right\| - \sigma_y \left( \bar{\varepsilon}_n^p \right)
$$

若 $f^{\text{trial}} \leq 0$：则步长内为弹性变形，接受预测值：

$$
\boldsymbol{\sigma}_{n+1} = \boldsymbol{\sigma}^{\text{trial}}, \quad
\boldsymbol{\varepsilon}_{n+1}^p = \boldsymbol{\varepsilon}_n^p, \quad
\bar{\varepsilon}_{n+1}^p = \bar{\varepsilon}_n^p.
$$

否则，进入塑性修正阶段，找到满足 $t_{n+1}$ 时刻屈服条件的应力状态

## 塑性修正

结合流动法则

$$
\boldsymbol{\varepsilon}_{n+1}^p = \boldsymbol{\varepsilon}_n^p + \Delta \gamma\, \mathbf{n}_{n+1},
$$

弹性关系

$$
\boldsymbol{\sigma}_{n+1} = \mathbf{C}^e : \left( \boldsymbol{\varepsilon}_{n+1} - \boldsymbol{\varepsilon}_{n+1}^p \right)
= \mathbf{C}^e : \left( \boldsymbol{\varepsilon}_n + \Delta\boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}_{n+1}^p \right),
$$

以及应变分解

$$
\boldsymbol{\varepsilon}_n = \boldsymbol{\varepsilon}_n^e + \boldsymbol{\varepsilon}_n^p,
$$

得到

$$
\boldsymbol{\sigma}_{n+1} = \boldsymbol{\sigma}^{\text{trial}} - \mathbf{C}^e : \left( \boldsymbol{\varepsilon}_{n+1}^p - \boldsymbol{\varepsilon}_n^p \right)
= \boldsymbol{\sigma}^{\text{trial}} - \Delta\gamma\mathbf{C}^e :\mathbf{n}_{n+1}.
$$

### 各向同性硬化

此时，Mises 屈服函数为

$$
f(\boldsymbol{\sigma},\bar{\varepsilon}^{p})=\sqrt{\frac{3}{2}}\|\mathbf{s}\|-\sigma_{y}(\bar{\varepsilon}^{p}),
$$

因此 $\mathbf{n} = \sqrt{\frac{3}{2}} \frac{\mathbf{s}}{\|\mathbf{s}\|}$，结合关联流动法则，有

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
\boldsymbol{\sigma}_{n+1} &= \boldsymbol{\sigma}^{\text{trial}} - \Delta\gamma\mathbf{C}^e :\mathbf{n}_{n+1},\\
\bar{\varepsilon}_{n+1}^p &= \bar{\varepsilon}_n^p + \Delta \gamma,\\
f_{n+1}&=\sqrt{\frac{3}{2}}\|\mathbf{s}_{n+1}\|-\sigma_{y}(\bar{\varepsilon}^{p}_{n+1})=0,
\end{aligned}
\end{equation}
$$

求解变量为

$$
\boldsymbol{\sigma}_{n+1},\quad \bar{\varepsilon}_{n+1}^p,\quad \Delta \gamma
$$

通常这一非线性方程组使用 Newton-Raphson 方法进行求解：

记 $\mathbf{v} = \left[\boldsymbol{\sigma}=\boldsymbol{\sigma}_{n+1},\varepsilon=\bar{\varepsilon}_{n+1}^p,\Delta \gamma\right]^{T}$，

记 $\mathbf{r}=\left[\mathbf{r}_{\boldsymbol{\sigma}},r_{\varepsilon},r_{f}\right]^{T}$，其中

$$
\begin{equation}
\begin{aligned}
\mathbf{r}_{\boldsymbol{\sigma}} &= \boldsymbol{\sigma} - \boldsymbol{\sigma}^{\text{trial}} + \Delta\gamma\mathbf{C}^e : \mathbf{n}_{n+1},\\
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

### 运动硬化

此时，Mises 屈服函数为

$$
f(\boldsymbol{\sigma},\boldsymbol{\alpha})=\sqrt{\frac{3}{2}}\|\mathbf{s}-\boldsymbol{\alpha}\|-\sigma_{y},
$$

根据 Prager 运动硬化公式

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
\boldsymbol{\sigma}_{n+1} &= \boldsymbol{\sigma}^{\text{trial}} - \Delta\gamma\mathbf{C}^e :\mathbf{n}_{n+1},\\
\boldsymbol{\alpha}_{n+1}&=\boldsymbol{\alpha}_{n} + C\Delta\gamma\mathbf{n}_{n+1},\\
f_{n+1}&=\sqrt{\frac{3}{2}}\|\mathbf{s}_{n+1}-\boldsymbol{\alpha}_{n+1}\|-\sigma_{y}=0,
\end{aligned}
\end{equation}
$$

求解变量为

$$
\boldsymbol{\sigma}_{n+1},\quad \boldsymbol{\alpha}_{n+1},\quad \Delta \gamma
$$

记 $\mathbf{v} = \left[\boldsymbol{\sigma}=\boldsymbol{\sigma}_{n+1},\boldsymbol{\alpha}=\boldsymbol{\alpha}_{n+1},\Delta \gamma\right]^{T}$，

记 $\mathbf{r}=\left[\mathbf{r}_{\boldsymbol{\sigma}},r_{\boldsymbol{\alpha}},r_{f}\right]^{T}$，其中

$$
\begin{equation}
\begin{aligned}
\mathbf{r}_{\boldsymbol{\sigma}} &= \boldsymbol{\sigma} - \boldsymbol{\sigma}^{\text{trial}} + \Delta\gamma\mathbf{C}^e : \mathbf{n}_{n+1},\\
r_{\boldsymbol{\alpha}}&=\boldsymbol{\alpha}_{n+1}-\boldsymbol{\alpha}_{n} - C\Delta\gamma\mathbf{n}_{n+1},\\
r_{f}&=\sqrt{\frac{3}{2}}\|\mathbf{s}_{n+1}-\boldsymbol{\alpha}_{n+1}\|-\sigma_{y},
\end{aligned}
\end{equation}
$$

于是，Jacobian 矩阵为

$$
\begin{equation}
\mathbf{J} = \frac{\partial \mathbf{r}}{\partial \mathbf{v}}=
\begin{bmatrix}
\frac{\partial \mathbf{r}_{\boldsymbol{\sigma}}}{\partial \boldsymbol{\sigma}} & \frac{\partial \mathbf{r}_{\boldsymbol{\sigma}}}{\partial \boldsymbol{\alpha}} & \frac{\partial \mathbf{r}_{\boldsymbol{\sigma}}}{\partial \Delta \gamma} \\
\frac{\partial r_{\boldsymbol{\alpha}}}{\partial \boldsymbol{\sigma}} & \frac{\partial r_{\boldsymbol{\alpha}}}{\partial \boldsymbol{\alpha}} & \frac{\partial r_{\boldsymbol{\alpha}}}{\partial \Delta \gamma} \\
\frac{\partial r_{f}}{\partial \boldsymbol{\sigma}} & \frac{\partial r_{f}}{\partial \boldsymbol{\alpha}} & \frac{\partial r_{f}}{\partial \Delta \gamma}
\end{bmatrix}.
\end{equation}
$$

初值可选为 $\mathbf{v}^{(0)}=\left[\boldsymbol{\sigma}^{\text{trial}},\boldsymbol{\alpha}_{n},0\right]$. 注意，$\boldsymbol{\alpha}_{n}$ 使用的是当前时间步上一个外层非线性迭代的结果

### 混合硬化

此时，Mises 屈服函数为

$$
f(\boldsymbol{\sigma},\boldsymbol{\alpha},\bar{\varepsilon}^{p})=\sqrt{\frac{3}{2}}\|\mathbf{s} - \boldsymbol{\alpha}\|-\sigma_{y}(\bar{\varepsilon}^{p}),
$$

结合各向同性硬化和 Prager 运动硬化公式，得到求解方程组为

$$
\begin{equation}
\begin{aligned}
\boldsymbol{\sigma}_{n+1} &= \boldsymbol{\sigma}^{\text{trial}} - \Delta\gamma\mathbf{C}^e :\mathbf{n}_{n+1},\\
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

记 $\mathbf{v} = \left[\boldsymbol{\sigma}=\boldsymbol{\sigma}_{n+1},\varepsilon=\bar{\varepsilon}_{n+1}^p,\boldsymbol{\alpha}=\boldsymbol{\alpha}_{n+1},\Delta \gamma\right]^{T}$，

记 $\mathbf{r}=\left[\mathbf{r}_{\boldsymbol{\sigma}},r_{\varepsilon},r_{\boldsymbol{\alpha}},r_{f}\right]^{T}$，其中

$$
\begin{equation}
\begin{aligned}
\mathbf{r}_{\boldsymbol{\sigma}} &= \boldsymbol{\sigma} - \boldsymbol{\sigma}^{\text{trial}} + \Delta\gamma\mathbf{C}^e : \mathbf{n}_{n+1},\\
r_{\varepsilon}&=\varepsilon - \bar{\varepsilon}_n^p - \Delta \gamma,\\
r_{\boldsymbol{\alpha}}&=\boldsymbol{\alpha}_{n+1}-\boldsymbol{\alpha}_{n} - C\Delta\gamma\mathbf{n}_{n+1},\\
r_{f}&=\sqrt{\frac{3}{2}}\|\mathbf{s}_{n+1}-\boldsymbol{\alpha}_{n+1}\|-\sigma_{y},
\end{aligned}
\end{equation}
$$

于是，Jacobian 矩阵为

$$
\begin{equation}
\mathbf{J} = \frac{\partial \mathbf{r}}{\partial \mathbf{v}}=
\begin{bmatrix}
\frac{\partial \mathbf{r}_{\boldsymbol{\sigma}}}{\partial \boldsymbol{\sigma}} & \frac{\partial \mathbf{r}_{\boldsymbol{\sigma}}}{\partial \varepsilon} & \frac{\partial \mathbf{r}_{\boldsymbol{\sigma}}}{\partial \boldsymbol{\alpha}} & \frac{\partial \mathbf{r}_{\boldsymbol{\sigma}}}{\partial \Delta \gamma} \\
\frac{\partial r_{\varepsilon}}{\partial \boldsymbol{\sigma}} & \frac{\partial r_{\varepsilon}}{\partial \varepsilon} & \frac{\partial r_{\varepsilon}}{\partial \boldsymbol{\alpha}} & \frac{\partial r_{\varepsilon}}{\partial \Delta \gamma} \\
\frac{\partial r_{\boldsymbol{\alpha}}}{\partial \boldsymbol{\sigma}} & \frac{\partial r_{\boldsymbol{\alpha}}}{\partial \varepsilon} & \frac{\partial r_{\boldsymbol{\alpha}}}{\partial \boldsymbol{\alpha}} & \frac{\partial r_{\boldsymbol{\alpha}}}{\partial \Delta \gamma} \\
\frac{\partial r_{f}}{\partial \boldsymbol{\sigma}} & \frac{\partial r_{f}}{\partial \varepsilon} & \frac{\partial r_{f}}{\partial \boldsymbol{\alpha}} & \frac{\partial r_{f}}{\partial \Delta \gamma}
\end{bmatrix}.
\end{equation}
$$

初值可选为 $\mathbf{v}^{(0)}=\left[\boldsymbol{\sigma}^{\text{trial}},\bar{\varepsilon}_{n}^p,\boldsymbol{\alpha}_{n},0\right]$. 注意，$\bar{\varepsilon}_{n}^p,\boldsymbol{\alpha}_{n}$ 使用的是当前时间步上一个外层非线性迭代的结果

## 一致性切线模量 $\mathbf{C}_{ep}^{\text{alg}}$

```{margin}
一致性切线模量与算法匹配，若使用非算法相关的理论弹塑性模量 $\mathbf{C}_{ep}^{\text{theo}}$，则牛顿迭代肯能够收敛缓慢甚至发散
```

一致性切线模量（也称为**算法切线模量**）反映了应力对总应变的线性化增量关系，能够准确描述材料在弹塑性等非线性行为下的刚度变化。**在非线性有限元分析中，Jacobian 矩阵的计算采用一致性切线模量，可以显著提高全局非线性迭代的收敛速度和数值稳定性**。因此，在本构积分后，计算并返回一致性切线模量是实现高效、稳健有限元求解的关键步骤

一致性切线模量定义为

$$
C_{ep}^{\text{alg}}=\frac{\partial \boldsymbol{\sigma}_{n+1}}{\partial \boldsymbol{\varepsilon}_{n+1}}.
$$