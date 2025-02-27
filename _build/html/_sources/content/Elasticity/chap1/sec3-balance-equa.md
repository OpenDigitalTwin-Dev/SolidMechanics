# 平衡方程

如图所示，在弹性体内任一点 $C$ 处取出一个矩形微分体，其尺寸为 $\mathrm{d}x$ 和 $\mathrm{d}y$。舍去泰勒展开式中的高阶项后，可以得到各个面的应力分布

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

```{margin}
建立方程时，采用了小变形假定，因此使用弹性体变形以前的尺寸作为微分体的几何尺寸，从而简化了力学分析
```

$$
\tau_{xy}\cdot\mathrm{d}y\cdot\frac{1}{2}\mathrm{d}x+\left(\tau_{xy}+\frac{\partial \tau_{xy}}{\partial x}\mathrm{d}x\right)\cdot\mathrm{d}y\cdot\frac{1}{2}\mathrm{d}x-\\

\tau_{yx}\cdot\mathrm{d}x\cdot\frac{1}{2}\mathrm{d}y+\left(\tau_{yx}+\frac{\partial \tau_{yx}}{\partial y}\mathrm{d}y\right)\cdot\mathrm{d}y\cdot\frac{1}{2}\mathrm{d}x=0,
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
\left( \sigma_x + \frac{\partial \sigma_x}{\partial x} dx \right) \cdot dy
-\sigma_x \cdot dy
+
\left( \tau_{yx} + \frac{\partial \tau_{yx}}{\partial y} dy \right) \cdot dx
-\tau_{yx} \cdot dx
+f_x dx dy  = 0,
$$

整理得到

$$
\frac{\partial \sigma_x}{\partial x} + \frac{\partial \tau_{yx}}{\partial y} + f_x = 0.
$$

类似地，可得到 $y$ 方向上的平衡方程。于是，二维问题中的**平衡方程**为

$$
\begin{cases}
\frac{\partial \sigma_x}{\partial x} + \frac{\partial \tau_{yx}}{\partial y} + f_x = 0, \\
\frac{\partial \sigma_y}{\partial y} + \frac{\partial \tau_{xy}}{\partial x} + f_y = 0.
\end{cases}
$$ (sec3-eq:balance)

## 任一点的应力状态

应力定义在其所作用的截面上，这表明应力的大小和方向依赖于截面的取向。在实际问题中，为了全面了解材料在外力作用下的受力状态，通常需要研究某一点在**不同取向截面上**的应力分布。为此，需要采用**应力张量**的数学描述，并通过应力变换公式将基准截面上的应力分量转换到任意取向的截面上

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
p_x \, \mathrm{d}s - \sigma_x \, l\mathrm{d}s -  \tau_{yx} \, m  \mathrm{d}s + f_x \frac{l\mathrm{d}s \, m\mathrm{d}s}{2} = 0, \\
p_y \, \mathrm{d}s - \sigma_y \, m  \mathrm{d}s -  \tau_{xy} \, l  \mathrm{d}s + f_y \frac{l\mathrm{d}s \, m\mathrm{d}s}{2} = 0.
\end{cases}
$$

消去微元量，得到

$$
\mathbf{p} = \begin{bmatrix}
p_{x}\\
p_{y}
\end{bmatrix}= \begin{bmatrix}
\sigma_{x} & \tau_{yx} \\
\tau_{xy} & \sigma_{y}
\end{bmatrix}
\begin{bmatrix}
l \\
m
\end{bmatrix},
$$ (sec3-eq:stress-tensor-1)

这表明，只需知道过点 $P$ 的平行于 $x$ 轴和 $y$ 轴的截面上的应力，就能够计算出任意取向截面上的应力。矩阵

```{margin}
应力张量的**列向量**是相应截面的应力
```

$$
\boldsymbol{\sigma}=\begin{bmatrix}
\sigma_{x} & \tau_{yx} \\
\tau_{xy} & \sigma_{y}
\end{bmatrix}
$$

被称为**应力张量**

```{note}
在二/三维情况下，只需知道任意两/三个不平行截面上的应力，就可以以类似的方法计算出任意取向截面上的应力（**柯西应力定理**）
```

$\overline{AB}$ 上的正应力 $\sigma_{n}$ 和切应力 $\tau_{n}$ 分别为

$$
\begin{align*}
\sigma_{n} &= \mathbf{p}\cdot\mathbf{n}=l^{2}\sigma_{x} + m^{2}\sigma_{y}+2lm\tau_{xy}=\mathbf{n}^{T}\boldsymbol{\sigma}\mathbf{n},\\
\tau_{n} &= lp_{y}-mp_{x}=lm(\sigma_y - \sigma_x)+(l^2-m^2)\tau_{xy}=(\mathbf{n}^\perp)^{T}\boldsymbol{\sigma}\mathbf{n}.
\end{align*}
$$ (sec3-eq:stress-tensor-3)

### 主应力

如果经过点 $P$ 的某一截面上的切应力为 0，仅存在正应力，则该截面称为**主应力面**，此时的正应力被称为点 $P$ 的一个**主应力**，而该截面的法向方向被称为**主应力方向**

此时，切应力为 0，全应力与正应力同向，即与 $\mathbf{n}$ 同向。设其大小为 $p$，则有 $\mathbf{p} = p\,\mathbf{n}$，代入到{eq}`sec3-eq:stress-tensor-1`，整理得到

$$
(\boldsymbol{\sigma} - p\,\mathbf{I})\,\mathbf{n} = \mathbf{0},
$$

这表明，主应力的大小是应力张量 $\boldsymbol{\sigma}$ 的特征值，其方向则是对应的特征向量。于是 $p$ 满足特征方程

$$
p^2 - (\sigma_x + \sigma_y)\,p + (\sigma_x \sigma_y - \tau_{xy}^2) = 0.
$$ (sec3-eq:stress-tensor-2)

由于

$$
(\sigma_x + \sigma_y)^2 - 4\,(\sigma_x \sigma_y - \tau_{xy}^2)=(\sigma_x - \sigma_y)^2 + 4\tau_{xy}^2 > 0,
$$

因此特征方程 {eq}`sec3-eq:stress-tensor-2` 总是有两个实根 $p_{1}\geq p_{2}$，且满足

$$
p_{1}+p_{2} = \sigma_{x} + \sigma_{y}.
$$

由于 $\boldsymbol{\sigma}$ 是一个实对称矩阵，因此其特征值 $p_1, p_2$ 所对应的单位特征向量 $\mathbf{n}_{1},\mathbf{n}_{2}$ 是正交的。这意味着主应力方向彼此正交，即**主应力相互正交**。不仅如此，由于

```{margin}
$\mathbf{n}$ 是单位法向量
```

$$
p_2 \leq \mathbf{n}^{T}\boldsymbol{\sigma}\mathbf{n} \leq p_1,
$$

因此，$p_1$ 和 $p_2$ 分别是点 $P$ 上最大与最小的正应力，即**两个主应力分别是最大与最小的正应力**

```{margin}
应力主面上切应力为 0
```

如果将 $x$ 轴和 $y$ 轴分别选定为两个主应力方向，则在该坐标系下，应力张量表示为一个对角矩阵

$$
\boldsymbol{\sigma}=\begin{bmatrix}
p_{1} & 0 \\
0 & p_{2}
\end{bmatrix}.
$$

```{admonition} 基变换与张量变换
:class: tip, dropdown
将张量视为一个将任意截面法向量映射为作用在该截面上的应力的线性算子，则在不同的基选择下，应力张量的矩阵表示是相似的。
```

此时，根据切应力计算公式 {eq}`sec3-eq:stress-tensor-3`，有

$$
\tau_{n} = lm(p_{2} - p_{1}),
$$

代入 $l^2 + m^2 = 1$ 消去 $m$，得到

$$
\tau_n = \pm \sqrt{\frac{1}{4} - \left(\frac{1}{2} - l^2\right)^2} \, (\sigma_2 - \sigma_1),
$$

当 $ \frac{1}{2} - l^2 = 0 $ 时，切应力 $ \tau_n $ 取得最大值。此时，最大切应力为 $\tau_{n} = \frac{1}{2} (p_1 - p_2)$，
且对应截面的法向量与主应力面之间的夹角为 $ 45^\circ $。最小切应力为 0

```{note}
对于三维情形，最大切应力为 $\tau_{n} = \frac{1}{2} (p_1 - p_3)$
```
