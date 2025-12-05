# 隐式静力学

相比于显式动力学方法，隐式静力学方法在实现上则复杂得多，其核心问题在于刚度矩阵的计算和本构积分中一致切线模量的计算

为简便起见，先不考虑边界条件，此时，平衡方程的弱形式为

$$
\begin{equation}
\int_{\Omega_{n+1}} \boldsymbol{\sigma}:\boldsymbol{\varepsilon} \, \mathrm{d}V_{n+1}
= \int_{\Omega_{n+1}}\mathbf{f}\cdot \mathbf{v}\,\mathrm{d}V_{n+1},
\end{equation}
$$ (sec2-eq:int_n+1)

其中，积分区域 $\Omega_{n+1}$ 未知，与 $\mathbf{u}_{n+1}$ 相关

记从 $\Omega_{n}$ 到 $\Omega_{n+1}$ 的变形梯度矩阵为

$$
\mathbf{F} = \frac{\partial \mathbf{x}_{n+1}}{\partial \mathbf{x}_{n}} = I + \nabla \mathbf{u},
$$

其中，$\mathbf{x}_{n+1}$ 和 $\mathbf{x}_{n}$ 分别为 $\Omega_{n+1}$ 和 $\Omega_{n}$ 下的坐标系；于是，上述积分变为

$$
\begin{equation}
\int_{\Omega_{n+1}} \boldsymbol{\sigma}:\boldsymbol{\varepsilon} \, \mathrm{d}V_{n+1} = \int_{\Omega_{n}} J\boldsymbol{\sigma}:\boldsymbol{\varepsilon} \, \mathrm{d}V_{n},
\end{equation}
$$ (sec2-eq:int_n)

其中，$J=\det(\mathbf{F})$，此时，$\boldsymbol{\sigma}$ 和 $\boldsymbol{\varepsilon}$ 应使用 $\Omega_{n}$ 下的坐标系 $\mathbf{x}_{n}$ 表示

于是

$$
\begin{equation}
\frac{\partial }{\partial \mathbf{u}}\int_{\Omega_{n}} J\boldsymbol{\sigma}:\boldsymbol{\varepsilon} \, \mathrm{d}V_{n} = \int_{\Omega_{n}} \frac{\partial (J\boldsymbol{\sigma})}{\partial \mathbf{u}}:\boldsymbol{\varepsilon} + J\boldsymbol{\sigma}:\frac{\partial \boldsymbol{\varepsilon}}{\partial\mathbf{u}}\, \mathrm{d}V_{n}
\end{equation}
$$

依次考虑每一项，首先

$$
\frac{\partial (J\boldsymbol{\sigma})}{\partial \mathbf{u}} = \frac{\partial J}{\partial \mathbf{u}}\boldsymbol{\sigma} + J\frac{\partial \boldsymbol{\sigma}}{\partial \mathbf{u}},
$$

