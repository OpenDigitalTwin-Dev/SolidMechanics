# 变形分析

## 变形梯度矩阵

材料的形变特征可以通过分析其内部任意一条曲线在受力后的变形来刻画，假设初始曲线为 

$$
\mathbf{X}(\xi) = [X_{1}(\xi),X_{2}(\xi),X_{3}(\xi)]^{T}
$$

受力变形后，曲线变为

$$
\mathbf{x}(\xi) = [x_{1}(\xi),x_{2}(\xi),x_{3}(\xi)]^{T}
$$

在曲线上任意一点，其切向量（即无穷小线段的逼近）在变形前后满足如下关系：

$$
\frac{\partial \mathbf{x}}{\partial \xi} = \frac{\partial \mathbf{x}}{\partial \mathbf{X}}\frac{\partial \mathbf{X}}{\partial \xi} =  \begin{bmatrix}
\frac{\partial x_1}{\partial X_1} & \frac{\partial x_1}{\partial X_2} & \frac{\partial x_1}{\partial X_3} \\
\frac{\partial x_2}{\partial X_1} & \frac{\partial x_2}{\partial X_2} & \frac{\partial x_2}{\partial X_3} \\
\frac{\partial x_3}{\partial X_1} & \frac{\partial x_3}{\partial X_2} & \frac{\partial x_3}{\partial X_3}
\end{bmatrix}\frac{\partial \mathbf{X}}{\partial \xi},
$$

其中，矩阵

$$
\mathbf{F} = \frac{\partial \mathbf{x}}{\partial{\mathbf{X}}} = 
\begin{bmatrix}
\frac{\partial x_1}{\partial X_1} & \frac{\partial x_1}{\partial X_2} & \frac{\partial x_1}{\partial X_3} \\
\frac{\partial x_2}{\partial X_1} & \frac{\partial x_2}{\partial X_2} & \frac{\partial x_2}{\partial X_3} \\
\frac{\partial x_3}{\partial X_1} & \frac{\partial x_3}{\partial X_2} & \frac{\partial x_3}{\partial X_3}
\end{bmatrix} = \nabla_{0}\mathbf{x},
$$

被称为**变形梯度矩阵**

$\mathbf{F}$ 包含了描述变形过程中长度、角度和体积变化所需的全部局部信息，是刻画材料变形的核心量，我们会在后面更多的例子中看见

于是，在初始构型 $\Omega_0$ 中，微元 $\mathrm{d}\mathbf{X}$ 经过运动后变为当前构型 $\Omega$ 中的微元 $\mathrm{d}\mathbf{x}$，两者之间满足

$$
\mathrm{d}\mathbf{x} = \mathbf{F}\mathrm{d}\mathbf{X},
$$

如果 $\mathbf{F}$ 不可逆，则可能出现 $\mathrm{d}\mathbf{x} = \mathbf{0}$ 的情况，即不同物质点在变形后发生重合，这种现象是非物理的。因此，$\mathbf{F}$ 必须是可逆的

$\mathbf{F}$ 的可逆性保证了变形前后材料点的一一对应关系

$$
\mathbf{F} = \nabla_{0}\mathbf{x} = \nabla_{0}\mathbf{u} + \mathbf{I},\quad \mathbf{F}^{-1}=\nabla\mathbf{X} = \mathbf{I} - \nabla\mathbf{u}
$$

## 面积与体积变换

### 面积变换

设初始构型 $\Omega_{0}$ 上的微元区域 $\mathrm{d}\mathbf{A}=\mathbf{N}\mathrm{d}A$ 变换到了当前构型中的 $\mathrm{d}\mathbf{a}=\mathbf{n}\mathrm{d}a$，根据 Nanson 公式，满足

$$
\mathbf{n}\mathrm{d}a = J\mathbf{F}^{-T}\mathbf{N}\mathrm{d}A
$$

```{admonition} Nanson 公式证明
:class: tip, dropdown

在参考构型 $\Omega_{0}$ 中，取两个微小线元，$\mathrm{d}\mathbf{X}_{1}$ 和 $\mathrm{d}\mathbf{X}_{2}$，于是

$$
\mathbf{N}\ \mathrm{d}A = \mathrm{d}\mathbf{X}_{1}\times\mathrm{d}\mathbf{X}_{2},
$$

在当前构型 $\Omega$ 中，$\mathrm{d}\mathbf{x}_{i} = \mathbf{F}\mathrm{d}\mathbf{X}_{i}$，于是

$$
\begin{equation}
\begin{aligned}
\mathbf{n}\ \mathrm{d}a = \mathrm{d}\mathbf{x}_{1}\times\mathrm{d}\mathbf{x}_{2} &= (\mathbf{F}\mathrm{d}\mathbf{X}_{1})\times(\mathbf{F}\mathrm{d}\mathbf{X}_{2})\\
&=\det(\mathbf{F})\mathbf{F}^{-T}(\mathrm{d}\mathbf{X}_{1}\times\mathrm{d}\mathbf{X}_{2})\\
&=J\mathbf{F}^{-T}\mathbf{N}\ \mathrm{d}A,
\end{aligned}
\end{equation}
$$


**证明：** $(\mathbf{F}\mathbf{b})\times(\mathbf{F}\mathbf{c})=\det(\mathbf{F})\mathbf{F}^{-T}(\mathbf{b}\times\mathbf{c})$ 


若 $\mathbf{a},\mathbf{b},\mathbf{c}$ 线性无关且可逆，则

$$
\frac{\mathbf{F}\mathbf{a}\cdot(\mathbf{F}\mathbf{b}\times \mathbf{F}\mathbf{c})}{\mathbf{a}\cdot(\mathbf{b}\times \mathbf{c})}=
\frac{\det\left(\begin{bmatrix}
\mathbf{F}\mathbf{a}&\mathbf{F}\mathbf{b}&\mathbf{F}\mathbf{c}
\end{bmatrix}\right)}{
\det\left(\begin{bmatrix}
\mathbf{a}&\mathbf{b}&\mathbf{c}
\end{bmatrix}\right)
} = \det(\mathbf{F}),
$$

分别取 $\mathbf{a} = \mathbf{e}_{1},\mathbf{e}_{2},\mathbf{e}_{3}$ 代入，得到结论

```

```{admonition} Piola 恒等式
:class: tip, dropdown

$$
\nabla\cdot\mathbf{q}=\frac{1}{J}\nabla_{0}\cdot(J\mathbf{F}^{-1}\mathbf{q})
$$ (sec2-eq:piola-eqs)

其中，$\mathbf{q}$ 是向量场

**证明：**

$$
\begin{aligned}
\int_{\Omega}\nabla\cdot\mathbf{q}\ \mathrm{d}v=\oint_{\partial\Omega}\mathbf{q}\cdot\mathbf{n}\ \mathrm{d}s&=\oint_{\partial\Omega_{0}}\mathbf{q}\cdot (J\mathbf{F}^{-T}\mathbf{N})\ \mathrm{d}S\\
&=\oint_{\partial\Omega_{0}}\mathbf{N}\cdot (J\mathbf{F}^{-1}\mathbf{q})\ \mathrm{d}S\\
&=\int_{\Omega_{0}}\nabla_{0}\cdot (J\mathbf{F}^{-1}\mathbf{q})\ \mathrm{d}V
\end{aligned}
$$

另一方面

$$
\int_{\Omega}\nabla\cdot\mathbf{q}\ \mathrm{d}v = \int_{\Omega_{0}}J\nabla\cdot\mathbf{q}\ \mathrm{d}V
$$

由 $\Omega_{0}$ 的任意性，得到

$$
\nabla\cdot\mathbf{q} = \frac{1}{J}\nabla_{0}\cdot (J\mathbf{F}^{-1}\mathbf{q})
$$

```


### 体积变换

设初始构型 $\Omega_{0}$ 上 $\mathbf{X}$ 为顶点的平行六面体的三条线元为 $\mathrm{d}\mathbf{X}^{(1)}$,$\mathrm{d}\mathbf{X}^{(2)}$,$\mathrm{d}\mathbf{X}^{(3)}$，运动到当前构型 $\Omega$ 中，有

$$
\mathrm{d}\mathbf{x}^{(i)}=\mathbf{F}\mathrm{d}\mathbf{X}^{(i)},\quad i=1,2,3
$$

于是

$$
\begin{aligned}
\mathrm{d}v&=\mathrm{d}\mathbf{x}^{(1)}\cdot\mathrm{d}\mathbf{x}^{(2)}\times\mathrm{d}\mathbf{x}^{(3)}\\
&=(\mathbf{F}\mathbf{N}_{1}\mathrm{d}X^{(1)})\cdot(\mathbf{F}\mathbf{N}_{1}\mathrm{d}X^{(1)})\times(\mathbf{F}\mathbf{N}_{1}\mathrm{d}X^{(1)})\\
&=(\mathbf{F}\mathbf{N}_{1}\cdot\mathbf{F}\mathbf{N}_{1}\times\mathbf{F}\mathbf{N}_{1})\mathrm{d}X^{(2)}\mathrm{d}X^{(1)}\mathrm{d}X^{(3)}\\
&=\det(F)(\mathbf{N}_{1}\cdot\mathbf{N}_{1}\times\mathbf{N}_{1})\mathrm{d}X^{(2)}\mathrm{d}X^{(1)}\mathrm{d}X^{(3)}\\
&=J\mathrm{d}V
\end{aligned}
$$