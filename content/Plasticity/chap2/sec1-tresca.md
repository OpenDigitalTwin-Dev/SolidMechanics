# Tresca 屈服准则

<span class="gray-text">
Tresca 屈服准则被称为最大切应力理论，是最常用的屈服准则之一，属于各向同性屈服准则
</span>

Tresca 屈服准则，也称最大剪切应力准则：当某点的最大剪切应力达到临界值时，材料改点开始发生塑性变形

$$
\sigma_{\text{tresca}} = \max\left\{ |\sigma_1 - \sigma_2|, |\sigma_1 - \sigma_3|, |\sigma_2 - \sigma_3| \right\}\geq\sigma_{y},
$$

$\sigma_{y}$ 是**单轴拉伸**下的屈服强度，于是在屈服面上

$$
\sigma_{1}=\sigma_{y},\quad\sigma_{2} = 0,\quad \sigma_{3} = 0,
$$

得到

$$
\sigma_{\text{tresca}} = \sigma_{y}.
$$

设**纯剪切变形**下的屈服强度为 $\tau_{y}$，于是在屈服面上

$$
\sigma_{1}=\tau_{y},\quad\sigma_{2} = 0,\quad \sigma_{3} = -\tau_{y},
$$

得到

$$
\sigma_{\text{tresca}} = 2\tau_{y}.
$$

因此

$$
\sigma_{y} = 2\tau_{y}.
$$

$\sigma_{\text{tresca}}$ 也可以写为

$$
\sigma_{\text{tresca}} = \sigma_{\text{max}} - \sigma_{\text{min}}.
$$

根据 Tresca 屈服准则，位于中间的主应力对屈服没有任何影响

## 几何意义


## 最大剪切应力


设法向量为 $\mathbf{n}$ 的平面上的应力为 $\mathbf{t}_{\mathbf{n}}$，正应力为 $\sigma_{n}$，切应力为 $\tau_{\mathbf{n}}$，则

$$
\tau_{\mathbf{n}}^{2} = |\mathbf{t}_{\mathbf{n}}|^{2} - \sigma_{\mathbf{n}}^{2} = \mathbf{n}^{T}\boldsymbol{\sigma}^{2}\mathbf{n} - (\mathbf{n}^{T}\boldsymbol{\sigma}\mathbf{n})^{2},
$$

将 $\mathbf{n}$ 沿 $\boldsymbol{\sigma}$ 的单位特征向量 $\mathbf{n}_{1},\mathbf{n}_{2},\mathbf{n}_{3}$ （对应的特征值分别为 $\sigma_{1},\sigma_{2},\sigma_{3}$）分解

$$
\mathbf{n} = n_{1}\mathbf{n}_{1}+n_{2}\mathbf{n}_{3}+n_{2}\mathbf{n}_{3},
$$

其中 $n_{1}^2+n_{2}^2+n_{3}^2=1$， 于是

$$
\tau_{\mathbf{n}}^2 = n_{1}^{2}\sigma_{1}^{2}+n_{2}^{2}\sigma_{2}^{2}+n_{3}^{2}\sigma_{3}^{2}-(n_{1}^{2}\sigma_{1}+n_{2}^{2}\sigma_{2}+n_{3}^{2}\sigma_{3})^2,
$$ (sec2-eq:tau-1)

于是需在约束 $n_{1}^2+n_{2}^2+n_{3}^2=1$ 下最大化 $\tau_{\mathbf{n}}^2$，引入拉格朗日乘子 $\lambda$，构造目标函数

$$
L = \tau_{\mathbf{n}}^2 - \lambda(n_{1}^2+n_{2}^2+n_{3}^2-1)
$$

函数 $L$ 对 $n_{1},n_{2},n_{3}$ 的导数为

$$
\begin{equation}
\begin{aligned}
&(\sigma_{1}^2-2\sigma_{\mathbf{n}}\sigma_{1} - \lambda)n_{1} &= 0 \\
&(\sigma_{2}^2-2\sigma_{\mathbf{n}}\sigma_{2} - \lambda)n_{2} &= 0 \\
&(\sigma_{3}^2-2\sigma_{\mathbf{n}}\sigma_{3} - \lambda)n_{3} &= 0
\end{aligned}
\end{equation}
$$ (sec2-eq:L-der)

不失一般性

**1.** 若 $n_{2}=n_{3}=0$，此时 $n_{1}=\pm1$，代入到式 {eq}`sec2-eq:tau-1` 中，得到 $\tau_{\mathbf{n}}=0$，显然不是最大值

**2.** 若 $n_{1}\neq0,n_{2}\neq0,n_{3}=0$，代入到式 {eq}`sec2-eq:tau-1` 中，得到

$$
\tau_{\mathbf{n}}^2 = n_{1}^2\sigma_{1}^2+n_{2}^2\sigma_{2}^2 - (n_{1}^2\sigma_{1}+n_{2}^2\sigma_{2})^2,
$$

代入 $n_{2}^2 = 1 - n_{1}^2$，并记 $\ell = n_{1}^2$，于是

$$
\begin{equation}
\begin{aligned}
\tau_{\mathbf{n}}^2 &= \ell\sigma_{1}^2+(1 - \ell)\sigma_{2}^2 - (\ell\sigma_{1}+(1 - \ell)\sigma_{2})^2\\
&=-(\sigma_{1}-\sigma_{2})^2\ell^2-(\sigma_{1}^2-\sigma_{2}^2 - 2(\sigma_{1}-\sigma_{2})\sigma_{2})\ell\\
&=-(\sigma_{1}-\sigma_{2})^2(\ell^2 - \ell),
\end{aligned}
\end{equation}
$$ (sec2-eq:tau-2)

因此，当 $\ell = n_{1}^2=\frac{1}{2}$ 时，$\tau_{\mathbf{n}}$ 取得极值，此时 $n_{2}^2=\frac{1}{2}$，代入到式 {eq}`sec2-eq:tau-1`，得到

$$
\tau_{\mathbf{n}} = \frac{1}{2}|\sigma_{1}-\sigma_{2}|.
$$

截面法向量为 

$$
(\pm\frac{\sqrt{2}}{2})\mathbf{n_{1}}+(\pm\frac{\sqrt{2}}{2})\mathbf{n}_{2},
$$

与 $\sigma_{1}$ 截面和 $\sigma_{2}$ 截面夹角为 $45$ 度

**3.** 若 $n_{1}\neq0,n_{2}\neq0,n_{3}\neq0$，则此时 $\sigma_{1},\sigma_{2},\sigma_{3}$ 都是二次方程 $\sigma^2-2\sigma_{\mathbf{n}}\sigma - \lambda = 0$ 的根

- 若 $\sigma_{1}=\sigma_{2}=\sigma_{3}$，此时 $\boldsymbol{\sigma}$ 为

$$
\boldsymbol{\sigma} = Q^{T}(\sigma_{1}I)Q = \sigma_{1}I \quad\Longrightarrow\quad \tau_{\mathbf{n}}\equiv0
$$

- 若 $\sigma_{1}=\sigma_{2}\neq\sigma_{3}$，此时

$$
\tau_{\mathbf{n}}^2 = (n_{1}^{2}+n_{2}^{2})\sigma_{1}^{2}+n_{3}^{2}\sigma_{3}^{2}-((n_{1}^{2}+n_{2}^{2})\sigma_{1}+n_{3}^{2}\sigma_{3})^2,
$$ (sec2-eq:tau-3)

记 $n_{1}^2+n_{2}^2 = \ell$，于是 $n_{3}^2 = 1-\ell$，此时式 {eq}`sec2-eq:tau-3` 与式 {eq}`sec2-eq:tau-2` 有完全一样的形式，由此可知极值为

$$
\tau_{\mathbf{n}} = \frac{1}{2}|\sigma_{1}-\sigma_{3}|.
$$

此时 $n_{1}^2+n_{2}^2=n_{3}^2=\frac{1}{2}$，截面法向量为 

$$
n_{1}\mathbf{n_{1}}+(\pm\sqrt{\frac{1}{2}-n_{1}^2})\mathbf{n}_{2}+(\pm\frac{\sqrt{2}}{2})\mathbf{n}_{3},
$$

与 $\sigma_{3}$ 平面夹角为 $45$ 度

综上，考虑到方程 {eq}`sec2-eq:L-der` 的对称性，得到 

$$
\max_{\mathbf{n}} \tau_{\mathbf{n}} = \frac{1}{2}\max\left\{ |\sigma_1 - \sigma_2|, |\sigma_2 - \sigma_3|, |\sigma_3 - \sigma_1| \right\}.
$$

在截面与主应力面呈 $45$ 度夹角的平面处达到
