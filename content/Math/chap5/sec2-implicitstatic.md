# 隐式静力学

相比于显式动力学方法，隐式静力学方法在实现上则复杂得多，其核心问题在于刚度矩阵的计算和本构积分中一致切线模量的计算

简便起见，先不考虑边界条件

## 几何线性

首先考虑线性的位移-应变关系

$$
\boldsymbol{\varepsilon}(\mathbf{u}) = \frac{1}{2}(\nabla \mathbf{u} + \nabla\mathbf{u}^{T}),
$$

此时，平衡方程的弱形式为

$$
\begin{equation}
\int_{\Omega_{n+1}} \boldsymbol{\sigma}:\boldsymbol{\varepsilon}(\mathbf{v}) \, \mathrm{d}V_{n+1}
= \int_{\Omega_{n+1}}\mathbf{f}\cdot \mathbf{v}\,\mathrm{d}V_{n+1},
\end{equation}
$$ (sec2-eq:int_n+1)

其中，积分区域 $\Omega_{n+1}$ 未知，与 $\mathbf{u}_{n+1}$ 相关

记从 $\Omega_{n}$ 到 $\Omega_{n+1}$ 的变形梯度矩阵为

$$
\mathbf{F} = \frac{\partial \mathbf{x}_{n+1}}{\partial \mathbf{x}_{n}} = I + \nabla \mathbf{u},
$$

其中，$\mathbf{x}_{n+1}$ 和 $\mathbf{x}_{n}$ 分别为 $\Omega_{n+1}$ 和 $\Omega_{n}$ 下的坐标系；**注意，$\mathbf{u}$ 表示从 $\Omega_{n}$ 到 $\Omega_{n+1}$ 的增量位移**

于是，上述积分变为

$$
\begin{equation}
\int_{\Omega_{n+1}} \boldsymbol{\sigma}:\boldsymbol{\varepsilon}(\mathbf{v}) \, \mathrm{d}V_{n+1} = \int_{\Omega_{n}} J\boldsymbol{\sigma}:\boldsymbol{\varepsilon}(\mathbf{v}) \, \mathrm{d}V_{n},
\end{equation}
$$ (sec2-eq:int_n)

其中，$J=\det(\mathbf{F})$，此时，$\boldsymbol{\sigma}$ 和 $\boldsymbol{\varepsilon}$ 应使用 $\Omega_{n}$ 下的坐标系 $\mathbf{x}_{n}$ 表示

将其线性化，于是

$$
\begin{equation}
\begin{aligned}
\Delta\int_{\Omega_{n}} J\boldsymbol{\sigma}:\boldsymbol{\varepsilon}(\mathbf{v}) \, \mathrm{d}V_{n} 
&= \int_{\Omega_{n}} \Delta (J\boldsymbol{\sigma}):\boldsymbol{\varepsilon}(\mathbf{v}) + J\boldsymbol{\sigma}:\Delta \boldsymbol{\varepsilon}(\mathbf{v})\, \mathrm{d}V_{n}\\
&=\int_{\Omega_{n}} \Delta J\boldsymbol{\sigma}:\boldsymbol{\varepsilon}(\mathbf{v}) + J\Delta \boldsymbol{\sigma}:\boldsymbol{\varepsilon}(\mathbf{v}) + J\boldsymbol{\sigma}:\Delta \boldsymbol{\varepsilon}(\mathbf{v})\, \mathrm{d}V_{n}
\end{aligned}
\end{equation}
$$

### 体积项

类似于[体积变化速率公式](../../Tensor/chap3/sec1-velocity-gradient.md)

$$
\dot{J} = J\ \text{tr}(\dot{\mathbf{F}}\mathbf{F}^{-1}),
$$

有

$$
\Delta J = J\ \text{tr}(\Delta \mathbf{F}\mathbf{F}^{-1}) = J\Delta \mathbf{F}:\mathbf{F}^{-T},
$$

其中

$$
\Delta \mathbf{F} = \frac{\partial 
\Delta \mathbf{u}}{\partial \mathbf{x}_{n}} = \nabla_{n}\Delta \mathbf{u},
$$

### 应力变化项

$$
\Delta \boldsymbol{\sigma} = \mathbb{C}_{\text{alg}}:\Delta \boldsymbol{\varepsilon},
$$

其中，$\mathbb{C}_{\text{alg}}$ 是算法一致性切线模量，而

$$
\boldsymbol{\varepsilon} 
= \frac{1}{2}(\nabla_{n+1} \mathbf{u} + \nabla_{n+1}\mathbf{u}^{T}) 
= \frac{1}{2}(\nabla_{n} \mathbf{u}\ \mathbf{F}^{-1} + \mathbf{F}^{-T}\nabla_{n}\mathbf{u}^{T}),
$$

## 几何非线性