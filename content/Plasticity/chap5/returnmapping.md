# Return Mapping Algorithm

Return Mapping Algorithm（返回映射算法）是解决弹塑性材料本构积分问题的一种特定的、高效和鲁棒的数值积分策略，其核心思想是将复杂的弹塑性本构积分问题分解成两个更简单的步骤：

- **弹性预测**：假设在时间步长内，材料行为完全是弹性的，计算试应力
- **塑性修正**：检查试应力是否超出屈服面，若超出，则将应力拉回更新后的屈服面

以 Mises 屈服准则和关联流动法则为例，考虑小变形假设，故

**Mises 屈服函数**

$$
f(\boldsymbol{\sigma},\bar{\varepsilon}^{p})=\sqrt{\frac{3}{2}}\|\mathbf{s}\|-\sigma_{y}(\bar{\varepsilon}^{p})
$$

**关联流动法则**

$$
\dot{\boldsymbol{\varepsilon}}^{p}=\dot{\gamma}\frac{\partial f}{\partial \boldsymbol{\sigma}} = \dot{\gamma}\mathbf{n}
$$

其中，$\mathbf{n} = \sqrt{\frac{3}{2}} \frac{\mathbf{s}}{\|\mathbf{s}\|}$

## 弹性预测

假设整个步长是弹性的

```{margin}
**应力是由弹性形变产生的**
```

$$
\begin{equation}
\begin{aligned}
&\boldsymbol{\varepsilon}_{n+1}^{e, \text{trial}} = \boldsymbol{\varepsilon}_n^e + \Delta \boldsymbol{\varepsilon},\\
&\boldsymbol{\sigma}^{\text{trial}} = \mathbf{C}^e : \boldsymbol{\varepsilon}_{n+1}^{e, \text{trial}} = \boldsymbol{\sigma}_n + \mathbf{C}^e : \Delta \boldsymbol{\varepsilon}
\end{aligned}
\end{equation}
$$

同时塑性应变和硬化模量不变

$$
\boldsymbol{\varepsilon}_{n+1}^{p, \text{trial}} = \boldsymbol{\varepsilon}_n^p, \quad \bar{\varepsilon}_{n+1}^{p, \text{trial}} = \bar{\varepsilon}_n^p
$$

计算屈服函数

$$
f^{\text{trial}} = \sqrt{\frac{3}{2}} \left\| \mathbf{s}^{\text{trial}} \right\| - \sigma_y \left( \bar{\varepsilon}_n^p \right)
$$

若 $f^{\text{trial}} \leq 0$：则步长内为弹性变形，接受预测值：

$$
\boldsymbol{\sigma}_{n+1} = \boldsymbol{\sigma}^{\text{trial}}, \quad
\boldsymbol{\varepsilon}_{n+1}^p = \boldsymbol{\varepsilon}_n^p, \quad
\bar{\varepsilon}_{n+1}^p = \bar{\varepsilon}_n^p
$$

否则，进入塑性修正阶段，找到满足 $t_{n+1}$ 时刻屈服条件的应力状态

## 塑性修正

结合流动法则

$$
\boldsymbol{\varepsilon}_{n+1}^p = \boldsymbol{\varepsilon}_n^p + \Delta \gamma\, \mathbf{n}_{n+1}
$$

弹性关系

$$
\boldsymbol{\sigma}_{n+1} = \mathbf{C}^e : \left( \boldsymbol{\varepsilon}_{n+1} - \boldsymbol{\varepsilon}_{n+1}^p \right)
= \mathbf{C}^e : \left( \boldsymbol{\varepsilon}_n + \Delta\boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}_{n+1}^p \right)
$$

以及应变分解

$$
\boldsymbol{\varepsilon}_n = \boldsymbol{\varepsilon}_n^e + \boldsymbol{\varepsilon}_n^p
$$

得到

$$
\boldsymbol{\sigma}_{n+1} = \boldsymbol{\sigma}^{\text{trial}} - \mathbf{C}^e : \left( \boldsymbol{\varepsilon}_{n+1}^p - \boldsymbol{\varepsilon}_n^p \right)
= \boldsymbol{\sigma}^{\text{trial}} - \mathbf{C}^e : \Delta\gamma\, \mathbf{n}_{n+1}
$$

### 各向同性硬化法则

在各向同性硬化法则中，结合 Mises 屈服准则和关联流动法则，有

$$
\dot{\bar{\varepsilon}}^{p}=\sqrt{\frac{2}{3}}\|\dot{\boldsymbol{\varepsilon}}^{p}\|=\dot{\gamma}
$$

其离散形式为

$$
\bar{\varepsilon}_{n+1}^p = \bar{\varepsilon}_n^p + \Delta \gamma
$$

此外，需满足屈服条件

$$
f_{n+1}=\sqrt{\frac{3}{2}}\|\mathbf{s}_{n+1}\|-\sigma_{y}(\bar{\varepsilon}^{p}_{n+1})=0
$$

因此，求解方程组为

$$
\begin{equation}
\begin{aligned}
\boldsymbol{\sigma}_{n+1} &= \boldsymbol{\sigma}^{\text{trial}} - \mathbf{C}^e : \Delta\gamma\, \mathbf{n}_{n+1},\\
\bar{\varepsilon}_{n+1}^p &= \bar{\varepsilon}_n^p + \Delta \gamma,\\
f_{n+1}&=\sqrt{\frac{3}{2}}\|\mathbf{s}_{n+1}\|-\sigma_{y}(\bar{\varepsilon}^{p}_{n+1})=0
\end{aligned}
\end{equation}
$$

求解变量为

$$
\boldsymbol{\sigma}_{n+1},\quad \bar{\varepsilon}_{n+1}^p,\quad \Delta \gamma
$$

通常这一非线性方程组使用 Newton-Raphson 方法进行求解：

记 $\mathbf{v} = \left[\boldsymbol{\sigma}=\boldsymbol{\sigma}_{n+1},\varepsilon=\bar{\varepsilon}_{n+1}^p,\Delta \gamma\right]^{T}$

记 $\mathbf{r}=\left[\mathbf{r}_{\boldsymbol{\sigma}},r_{\varepsilon},r_{f}\right]^{T}$，其中

$$
\begin{equation}
\begin{aligned}
\mathbf{r}_{\boldsymbol{\sigma}} &= \boldsymbol{\sigma} - \boldsymbol{\sigma}^{\text{trial}} + \mathbf{C}^e : \Delta\gamma\, \mathbf{n}_{n+1},\\
r_{\varepsilon}&=\varepsilon - \bar{\varepsilon}_n^p - \Delta \gamma,\\
r_{f}&=\sqrt{\frac{3}{2}}\|\mathbf{s}_{n+1}\|-\sigma_{y}(\varepsilon)
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
\end{bmatrix}
\end{equation}.
$$

#### 一致性切线模量