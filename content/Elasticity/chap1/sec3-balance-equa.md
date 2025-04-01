# 平衡方程

<span class="gray-text">
平衡方程揭示了物体在平衡状态下所受各个力之间的关系。通过力的平衡方程（平动平衡）和力矩平衡方程（转动平衡），可以确定不同力之间的数值关系和方向关系
</span>

如图所示，在弹性体内任一点 $C$ 处取出一个矩形微分体，其尺寸为 $\mathrm{d}x$ 和 $\mathrm{d}y$。舍去泰勒展开式中的高阶项后，可以得到各个面的应力分布

```{admonition} 泰勒展开式
:class: tip, dropdown

$$
f(x+\mathrm{d}x) = f(x) + f'(x)\,\mathrm{d}x + \frac{f''(x)}{2!}\,\mathrm{d}x^2 + \frac{f^{(3)}(x)}{3!}\,\mathrm{d}x^3 + \cdots
$$
```

```{margin}
注意应力的方向规定
```

```{margin}
在微分体中，各个面上所受的应力被假定为均匀分布，并作用于对应面的中心
```

```{figure} ../../../images/Elasticity/chap1/balance-equa.png
---
width: 800px
name: sec3-fig:balance-equa
---
矩形微分体应力分布示意图
```

## 切应力互等定理

考虑以 $C$ 点为中心的力矩平衡方程 $\Sigma M_{C}=0$：

$$
\tau_{xy}\cdot\mathrm{d}y\cdot\frac{1}{2}\mathrm{d}x+\left(\tau_{xy}+\frac{\partial \tau_{xy}}{\partial x}\mathrm{d}x\right)\cdot\mathrm{d}y\cdot\frac{1}{2}\mathrm{d}x-\\

\tau_{yx}\cdot\mathrm{d}x\cdot\frac{1}{2}\mathrm{d}y-\left(\tau_{yx}+\frac{\partial \tau_{yx}}{\partial y}\mathrm{d}y\right)\cdot\mathrm{d}y\cdot\frac{1}{2}\mathrm{d}x=0,
$$

整理得到

$$
\tau_{xy}+\frac{1}{2}\frac{\partial \tau_{xy}}{\partial x}\mathrm{d}x=\tau_{yx}+\frac{1}{2}\frac{\partial \tau_{yx}}{\partial y}\mathrm{d}y,
$$

于是得到**切应力互等方程**

$$
\tau_{xy}=\tau_{yx}.
$$ (sec3-eq:Shear_stress)

## 平衡方程
考虑 $x$ 轴方向的平衡方程 $\Sigma F_{x}=0$：

$$
\left( \sigma_{xx} + \frac{\partial \sigma_{xx}}{\partial x} dx \right) \cdot dy
-\sigma_{xx} \cdot dy
+
\left( \tau_{yx} + \frac{\partial \tau_{yx}}{\partial y} dy \right) \cdot dx
-\tau_{yx} \cdot dx
+f_x dx dy  = 0,
$$

整理得到

$$
\frac{\partial \sigma_{xx}}{\partial x} + \frac{\partial \tau_{yx}}{\partial y} + f_x = 0.
$$

类似地，可得到 $y$ 方向上的平衡方程。于是，二维问题中的**平衡方程**为

$$
\begin{cases}
\frac{\partial \sigma_{xx}}{\partial x} + \frac{\partial \tau_{yx}}{\partial y} + f_x = 0, \\
\frac{\partial \sigma_{yy}}{\partial y} + \frac{\partial \tau_{xy}}{\partial x} + f_y = 0.
\end{cases}
$$ (sec3-eq:balance)

可以写为

$$
\nabla\cdot \boldsymbol{\sigma} + \mathbf{f} = \mathbf{0},
$$

其中，$\boldsymbol{\sigma}$ 是应力张量（见后文），$\mathbf{f}$ 是体积力向量

## 任一点的应力状态

在实际问题中，为了全面了解材料在外力作用下的受力状态，通常需要研究某一点在不同取向截面上的应力分布。定义在同一点不同取向截面上的应力之间是否存在内在联系？

对于任意点 $P$ ，以它为中心取一个微元直角三角形 $\triangle ABC$，其中 $\overline{CA}$ 平行于 $x$ 轴，长度为 $\mathrm{d}x$，$\overline{CB}$ 平行于 $y$ 轴，长度为 $\mathrm{d}y$，
设 $\overline{AB}$ 的单位法向量为 $\mathbf{n}=(l,m)$，长度为 $\mathrm{d}s$，于是

$$
\mathrm{d}x = m\mathrm{d}s,\quad \mathrm{d}y = l\mathrm{d}s.
$$

```{figure} ../../../images/Elasticity/chap1/stress-tensor.png
---
width: 400px
name: sec3-fig:stress-tensor
---
任一点的应力状态
```

设 $\overline{AB}$ 上全应力为 $\mathbf{p}$，沿 $x$ 轴方向和 $y$ 方向的应力分量分别为 $p_{x}$ 和 $p_{y}$，分别建立沿 $x$ 轴方向和 $y$ 方向的平衡方程

```{margin}
切应力互等方程：$\tau_{xy}=\tau_{yx}$
```

$$
\begin{cases}
p_x \, \mathrm{d}s - \sigma_{xx} \, l\mathrm{d}s -  \tau_{yx} \, m  \mathrm{d}s + f_x \frac{l\mathrm{d}s \, m\mathrm{d}s}{2} = 0, \\
p_y \, \mathrm{d}s - \sigma_{yy} \, m  \mathrm{d}s -  \tau_{xy} \, l  \mathrm{d}s + f_y \frac{l\mathrm{d}s \, m\mathrm{d}s}{2} = 0.
\end{cases}
$$

消去微元量，整理得到

$$
\begin{cases}
p_{x} = \sigma_{xx} \, l +  \tau_{yx} \, m, \\
p_{y} = \sigma_{yy} \, m  +  \tau_{xy} \, l.
\end{cases}
$$

这表明，只需知道过点 $P$ 的平行于 $x$ 轴和 $y$ 轴的截面上的应力，就能够计算出任意取向截面上的应力

```{note}
**柯西应力定理**：在二/三维情况下，任意取向截面上的应力可以通过任意两/三个不平行截面上的应力计算出
```

将上式写为矩阵形式

$$
\mathbf{p} = \begin{bmatrix}
p_{x}\\
p_{y}
\end{bmatrix}= \begin{bmatrix}
\sigma_{xx} & \tau_{yx} \\
\tau_{xy} & \sigma_{yy}
\end{bmatrix}
\begin{bmatrix}
l \\
m
\end{bmatrix},
$$ (sec3-eq:stress-tensor-1)

其中

```{margin}
应力张量的**列向量**是相应截面的应力
```

$$
\boldsymbol{\sigma}=\begin{bmatrix}
\sigma_{xx} & \tau_{yx} \\
\tau_{xy} & \sigma_{yy}
\end{bmatrix}
$$

被称为**应力张量**

$\overline{AB}$ 上的正应力 $\sigma_{n}$ 和切应力 $\tau_{n}$ 分别为

$$
\begin{align*}
\sigma_{n} &= \mathbf{p}\cdot\mathbf{n}=l^{2}\sigma_{xx} + m^{2}\sigma_{yy}+2lm\tau_{xy}=\mathbf{n}^{T}\boldsymbol{\sigma}\mathbf{n},\\
\tau_{n} &= lp_{y}-mp_{x}=lm(\sigma_{yy} - \sigma_{xx})+(l^2-m^2)\tau_{xy}=(\mathbf{n}^\perp)^{T}\boldsymbol{\sigma}\mathbf{n}.
\end{align*}
$$ (sec3-eq:stress-tensor-3)

### 最大正应力和最大切应力

实际工程中通常关注最大正应力和最大切应力，因为它们分别反映了材料在拉伸/压缩和剪切方向上的**极限**受力状态

#### 最大正应力

由于 $\boldsymbol{\sigma}$ 是一个实对称矩阵，因此对于任意 $\mathbf{n}$ 满足

$$
\sigma_2 \leq \mathbf{n}^{T}\boldsymbol{\sigma}\mathbf{n} \leq \sigma_1,
$$

其中，$\sigma_{1}\geq \sigma_{2}$ 为应力张量 $\boldsymbol{\sigma}$ 的特征值。这表明，在点 $P$ 处的最大正应力等于 $\boldsymbol{\sigma}$ 的最大特征值。当截面法向量 $\mathbf{n}$ 与 $\sigma_{1}$ 对应的（单位）特征向量 $\mathbf{n}_{1}$ 平行时，正应力达到最大值。此时

$$
\mathbf{p} = \boldsymbol{\sigma}\mathbf{n}_{1} = \sigma_{1}\mathbf{n}_{1},
$$

这表明截面上的应力与截面的法方向相同，此时，切应力为 0。将该截面称为**主应力面**，主应力面上的正应力被称为**主应力**，主应力面的法向方向被称为**主应力方向**

此外，由于 $\boldsymbol{\sigma}$ 是实对称矩阵，因此其特征值所对应的特征向量是正交的，即**主应力相互正交**

如果将 $x$ 轴和 $y$ 轴分别选定为两个主应力方向，则在该坐标系下，应力张量表示为一个对角矩阵

$$
\boldsymbol{\sigma}=\begin{bmatrix}
\sigma_{1} & 0 \\
0 & \sigma_{2}
\end{bmatrix}.
$$

```{admonition} 基变换与张量变换
:class: tip, dropdown

将张量视为一个将任意截面法向量映射为作用在该截面上的应力的线性算子，则在不同的基选择下，应力张量的矩阵表示是相似的
```

#### 最大切应力

```{margin}
主应力面上切应力为零，这一特性可用于简化应力分析过程
```

将 $x$ 轴和 $y$ 轴分别选定为两个主应力方向，此时，根据切应力计算公式 {eq}`sec3-eq:stress-tensor-3`，有

$$
\tau_{n} = lm(\sigma_{2} - \sigma_{1}),
$$

代入 $l^2 + m^2 = 1$ 消去 $m$，得到

$$
\tau_n = \pm \sqrt{\frac{1}{4} - \left(\frac{1}{2} - l^2\right)^2} \, (\sigma_2 - \sigma_1),
$$

当 $ \frac{1}{2} - l^2 = 0 $ 时，切应力 $ \tau_n $ 取得最大值，为 $\tau_{n} = \frac{1}{2} (\sigma_1 - \sigma_2)$，
此时对应截面的法向量与主应力面之间的夹角为 $ 45^\circ $，此时正应力为 $\sigma_{n} = \frac{1}{2} (\sigma_1 + \sigma_2)$

```{note}
对于三维情形，最大切应力为 $\tau_{n} = \frac{1}{2} (\sigma_1 - \sigma_3)$
```
