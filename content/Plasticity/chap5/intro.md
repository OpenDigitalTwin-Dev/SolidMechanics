# 本构积分

<span class="gray-text">
本构积分决定了有限元分析的数值精度与收敛性，是实现复杂材料非线性行为模拟的核心环节
</span>

本构积分在有限元求解中作用于**单元应力更新阶段**，即根据**应变增量**（通过求解整体刚度矩阵得到的**位移增量**获得），更新材料点**应力**和**内变量状态**（如塑性应变、硬化参数）的核心计算过程，即，已知

$$
\begin{equation}
\boldsymbol{\varepsilon}_{n+1},\ \boldsymbol{\varepsilon}_{n}^{e},\ \boldsymbol{\varepsilon}_{n}^{p},\ \bar{\varepsilon}_{n}^{p},\ \boldsymbol{\sigma}_{n},\ \dots 
\end{equation}
$$

求解

$$
\begin{equation}
\boldsymbol{\sigma}_{n+1},\ \boldsymbol{\varepsilon}_{n+1}^{p},\ \bar{\varepsilon}_{n+1}^{p},\ \dots
\end{equation}
$$

## 弹塑性本构初值问题

已知

- 初始弹性应变 $\boldsymbol{\varepsilon}^e(t_0)$ 和 硬化变量 $\boldsymbol{\alpha}(t_0)$
- 应变历史 $\boldsymbol{\varepsilon}(t)$, $t \in [t_0, T]$

求解

$$
\boldsymbol{\varepsilon}^e(t),\ \boldsymbol{\alpha}(t),\ \dot{\gamma}(t)
$$

满足

- 弹性应变的演化方程

$$
\begin{equation}
\dot{\boldsymbol{\varepsilon}}^e(t) = \dot{\boldsymbol{\varepsilon}}(t) - \dot{\boldsymbol{\varepsilon}}^{p}(t)= \dot{\boldsymbol{\varepsilon}}(t) - \dot{\gamma}(t) \mathbf{n}(\boldsymbol{\sigma}(t), \mathbf{A}(t))
\end{equation}
$$

- 硬化变量的演化方程

$$
\begin{equation}
\dot{\boldsymbol{\alpha}}(t) = \dot{\gamma}(t) \mathbf{H}(\boldsymbol{\sigma}(t), \mathbf{A}(t))
\end{equation}
$$

- 屈服条件与一致性条件

$$
\begin{equation}
\dot{\gamma}(t) \geq 0, \quad \Phi(\boldsymbol{\sigma}(t), \mathbf{A}(t)) \leq 0, \quad \dot{\gamma}(t) \Phi(\boldsymbol{\sigma}(t), \mathbf{A}(t)) = 0
\end{equation}
$$

### 符号注记

#### 硬化变量 $\boldsymbol{\alpha}$

描述材料硬化状态，比如屈服面的位置、大小、形状等。常见的有各向同性硬化变量、运动硬化变量；对于各向同性硬化，$\boldsymbol{\alpha}$ 通常为累计塑性应变 $\bar{\varepsilon}^{p}$；对于运动硬化，$\boldsymbol{\alpha}$ 为背应力 $\boldsymbol{\xi}$，代表屈服面位置的移动

#### 自由能 $\psi=\psi(\boldsymbol{\varepsilon}^{e},\boldsymbol{\alpha})$

材料的状态函数，用来描述材料内部能量随变形和硬化状态的变化

例如，各向同性硬化自由能为

$$
\psi = \frac{1}{2} \boldsymbol{\varepsilon}^{e} : \mathbf{C} : \boldsymbol{\varepsilon}^{e} + \frac{1}{2} \mathbf{H} \boldsymbol{\alpha}^2,
$$

运动硬化自由能为

$$
\psi = \frac{1}{2} \boldsymbol{\varepsilon}^{e} : \mathbf{C} : \boldsymbol{\varepsilon}^{e} + \frac{1}{2} c (\boldsymbol{\alpha} - \boldsymbol{\alpha}_0)^2.
$$

此外，有

$$
\boldsymbol{\sigma} = \bar{\rho} \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}^{e}},\quad \mathbf{A} = \bar{\rho} \frac{\partial \psi}{\partial \boldsymbol{\alpha}},
$$

上式子中，$\bar{\rho}$ 是密度，$\mathbf{A}$ 是硬化热力学力

#### 屈服函数 $\Phi(\boldsymbol{\sigma},\mathbf{A})$

#### 塑性流动方向 $\mathbf{n}(\boldsymbol{\sigma},\mathbf{A})$

对于关联流动法则，塑性势函数等于屈服函数，有

$$
\mathbf{n}(\boldsymbol{\sigma},\mathbf{A}) = \frac{\partial \Phi}{\partial \boldsymbol{\sigma}}
$$

#### 硬化规律 $\mathbf{H}(\boldsymbol{\sigma},\mathbf{A})$

描述硬化变量如何随塑性变形演化

$$
\dot{\boldsymbol{\alpha}} = \mathbf{H}(\boldsymbol{\sigma},\mathbf{A})\dot{\gamma}
$$

## 隐式欧拉离散

在本构积分（尤其是塑性力学）过程中，隐式欧拉离散方法因其优异的数值稳定性、能够处理较大步长、适用于非线性本构关系积分，并且易于保证物理约束和计算收敛性，因而被广泛应用于工程与科学计算领域

因此，初值问题离散化为

$$
\begin{equation}
\begin{aligned}
&\boldsymbol{\varepsilon}^{e}_{n+1} = \boldsymbol{\varepsilon}^{e}_{n} + \Delta\boldsymbol{\varepsilon} - \Delta\gamma\mathbf{n}(\boldsymbol{\sigma}_{n+1},\mathbf{A}_{n+1}),\\
&\boldsymbol{\alpha}_{n+1} = \boldsymbol{\alpha}_{n} + \Delta\gamma\mathbf{H}(\boldsymbol{\sigma}_{n+1},\mathbf{A}_{n+1}),\\
&\Delta\gamma \geq 0, \quad \Phi(\boldsymbol{\sigma}_{n+1}, \mathbf{A}_{n+1}) \leq 0, \quad \Delta\gamma \Phi(\boldsymbol{\sigma}_{n+1}, \mathbf{A}_{n+1}) = 0,
\end{aligned}
\end{equation}
$$

其中，$\Delta(\cdot)=(\cdot)_{n+1}-(\cdot)_{n}$
