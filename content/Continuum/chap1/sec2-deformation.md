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

在初始构型 $\Omega_0$ 中，微元 $\mathrm{d}\mathbf{X}$ 经过运动后变为当前构型 $\Omega$ 中的微元 $\mathrm{d}\mathbf{x}$，两者之间满足

$$
\mathrm{d}\mathbf{x} = \mathbf{F}\mathrm{d}\mathbf{X},
$$

如果 $\mathbf{F}$ 不可逆，则可能出现 $\mathrm{d}\mathbf{x} = \mathbf{0}$ 的情况，即不同物质点在变形后发生重合，这种现象是非物理的。因此，$\mathbf{F}$ 必须是可逆的

$\mathbf{F}$ 的可逆性保证了变形前后材料点的一一对应关系


