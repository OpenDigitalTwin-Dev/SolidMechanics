# 显式动力学求解

<span class="gray-text">
在动力学分析中，UL 方法因其在处理接触、摩擦等边界非线性问题上的天然优势而被广泛采用
</span>

使用 UL 方法结合 [Newmark 方法](../chap4/sec3-newmark.md)进行求解，其中 

$$
\beta = 0,\quad \gamma=0.5,
$$

相较于小位移小变形弹塑性问题，需在求解过程中需要做出以下重要改动

## 位置更新

采用显式 Newmark 方法时，在每个时间步开始，基于已知的位移、速度和加速度直接预测新构型的节点位置。由于该方法为显式格式，无需迭代修正，**预测的构型即为接受的新构型**。随后的内力计算、应变应力更新等均在这一新构型上进行。在 UL 框架下，这意味着积分域随每个时间步更新，**计算始终在当前时刻的构型上进行**

## 使用客观应力率和几何非线性

在 UL 框架的率形式本构关系中，使用变形率张量 

$$
\mathbf{D} = \frac{1}{2}(\mathbf{L} + \mathbf{L}^T)
$$ 
作为应变率度量。由于速度梯度 

$$
\mathbf{L} = \nabla \mathbf{v} = \dot{\mathbf{F}}\mathbf{F}^{-1}
$$ 

是对当前构型求导，几何非线性自然融入在 $\mathbf{D}$ 的定义中。这使得率形式本构关系（如 $\overset{\circ}{\boldsymbol{\sigma}} = \mathbb{C} : \mathbf{D}$）能够在大变形分析中保持客观性，同时避免显式使用非线性应变度量

### Jaumann 应力率

对于 Jaumann 应力率，有

$$
\overset{\circ}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} + \boldsymbol{\sigma} \mathbf{W} - \mathbf{W} \boldsymbol{\sigma}，
$$

由于

$$
\overset{\circ}{\boldsymbol{\sigma}} = \mathbb{C} : \mathbf{D},
$$

于是

$$
\mathbb{C} : \mathbf{D}_{n+1} = \frac{\boldsymbol{\sigma}_{n+1}^{\text{trial}} - \boldsymbol{\sigma}_{n}}{\Delta t} + \boldsymbol{\sigma}_{n} \mathbf{W}_{n+1} - \mathbf{W}_{n+1} \boldsymbol{\sigma}_{n}
$$

得到

$$
\boldsymbol{\sigma}_{n+1}^{\text{trial}}= \boldsymbol{\sigma}_{n} + \left(\mathbb{C} : \mathbf{D}_{n+1} + \mathbf{W}_{n+1} \boldsymbol{\sigma}_{n} - \boldsymbol{\sigma}_{n} \mathbf{W}_{n+1} \right)\Delta t
$$

若

$$
f^{\text{trial}}_{n+1}=\frac{3}{2}\left\|\mathbf{s}_{n+1}^{\text{trial}}\right\| - (\sigma_{0} + H\bar{\varepsilon}_n^p) > 0
$$

则进行塑性修正

$$
\bar{\varepsilon}_{n+1}^p=\bar{\varepsilon}_n^p + \frac{f^{\text{trial}}_{n+1}}{3\mu+H},
$$

且

$$
\boldsymbol{\sigma}_{n+1} = \boldsymbol{\sigma}_{n+1}^{\text{trial}}-2*\mu*\frac{f^{\text{trial}}_{n+1}}{3\mu+H}*\sqrt{\frac{3}{2}}\frac{\mathbf{s}_{n+1}^{\text{trial}}}{\left\|\mathbf{s}_{n+1}^{\text{trial}}\right\|},
$$


### Truesdell 应力率

类似地，在 Truesdell 应力率中

$$
\boldsymbol{\sigma}_{n+1}^{\text{trial}}= \boldsymbol{\sigma}_{n} + \left(\mathbb{C} : \mathbf{D}_{n+1} - \mathbf{L}_{n+1} \boldsymbol{\sigma}_{n} - \boldsymbol{\sigma}_{n} \mathbf{L}_{n+1} \right)\Delta t,
$$

其余步骤与 Jaumann 应力率类似