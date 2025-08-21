# 流动法则

塑性流动理论通常分为两大类

- **关联塑性流动理论**：指材料的**塑性流动方向与屈服面法向一致**，即塑性流动势函数 $\Psi$ 与屈服函数 $\Phi$ 完全相同（$\Psi\equiv\Phi$）。该理论严格遵循最大塑性功原理，理论体系严密，数学处理简便，因而在金属等体积塑性变形不显著的材料本构建模中得到了广泛应用。然而，对于土壤、岩石等摩擦性材料，关联流动法则往往会显著高估材料的体积膨胀效应，导致其在描述此类材料实际力学行为时存在一定局限性

- **非关联塑性流动理论**：指材料的**塑性流动方向与屈服面法向不一致**，即塑性流动势函数 $\Psi$ 与屈服函数 $\Phi$ 不同（$\Psi\neq \Phi$）。这一理论不再严格遵循最大塑性功原理，在数学处理上较为复杂，但能够更灵活地描述摩擦性材料（如土壤、岩石、混凝土等）的剪胀效应和体积变化，更贴近实际工程中的材料变形特性

## 自由能

在固体力学中，自由能 $\psi(\boldsymbol{\varepsilon},\boldsymbol{\varepsilon}^{p},\boldsymbol{\alpha})$ 是描述材料内部能量状态的标量函数，它依赖于总应变 $\boldsymbol{\varepsilon}$、塑性应变 $\boldsymbol{\varepsilon}^{p}$，以及内部硬化变量 $\boldsymbol{\alpha}$

```{note} 
:class: tip, dropdown

$\boldsymbol{\alpha}$ 用于描述材料硬化状态，比如屈服面的位置、大小、形状等。常见的有各向同性硬化变量、运动硬化变量；对于各向同性硬化，$\boldsymbol{\alpha}$ 通常为累计塑性应变 $\bar{\varepsilon}^{p}$；对于运动硬化，$\boldsymbol{\alpha}$ 为背应力 $\boldsymbol{\xi}$，代表屈服面位置的移动

```

该自由能的定义不仅反映了材料由于弹性变形所储存的可逆能量，还涵盖与不可逆过程相关的能量（如塑性变形和硬化效应），该定义方式保证了热力学的一致性（能量守恒和熵增）

以下考虑单位体积的情形，将自由能分解为可逆的弹性部分和与硬化相关的塑性部分

$$
\begin{equation}
\begin{aligned}
\psi(\boldsymbol{\varepsilon},\boldsymbol{\varepsilon}^{p},\boldsymbol{\alpha})&=\psi^{e}(\boldsymbol{\varepsilon}-\boldsymbol{\varepsilon}^{p})+\psi^{p}(\boldsymbol{\alpha})\\
&=\psi^{e}(\boldsymbol{\varepsilon}^{e})+\psi^{p}(\boldsymbol{\alpha})
\end{aligned}
\end{equation}
$$

计算

$$
\begin{equation}
\dot{\psi} = \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}}:\dot{\boldsymbol{\varepsilon}} + \frac{\partial \psi}{\partial \boldsymbol{\varepsilon}^{p}}:\dot{\boldsymbol{\varepsilon}}^{p} + \frac{\partial \psi}{\partial \boldsymbol{\alpha}}:\dot{\boldsymbol{\alpha}}
\end{equation}
$$ (intro-eq:free-energy)

结合 $\boldsymbol{\varepsilon}^{e} = \boldsymbol{\varepsilon} - \boldsymbol{\varepsilon}^{p}$，得到

$$
\begin{equation}
\begin{aligned}
\frac{\partial \psi}{\partial \boldsymbol{\varepsilon}}&=\frac{\partial \psi^e}{\partial \boldsymbol{\varepsilon}} = \frac{\partial \psi^e}{\partial \boldsymbol{\varepsilon}^e}\frac{\partial \boldsymbol{\varepsilon}^e}{\partial \boldsymbol{\varepsilon}} = \frac{\partial \psi^e}{\partial \boldsymbol{\varepsilon}^e},\\
\frac{\partial \psi}{\partial \boldsymbol{\varepsilon}^p}&=\frac{\partial \psi^e}{\partial \boldsymbol{\varepsilon}^p}=\frac{\partial \psi^e}{\partial \boldsymbol{\varepsilon}^e}\frac{\partial \boldsymbol{\varepsilon}^e}{\partial \boldsymbol{\varepsilon}^p} = -\frac{\partial \psi^e}{\partial \boldsymbol{\varepsilon}^e},\\
\frac{\partial \psi}{\partial \boldsymbol{\alpha}}&=\frac{\partial \psi^p}{\partial \boldsymbol{\alpha}},
\end{aligned}
\end{equation}
$$

故

$$
\begin{equation}
\begin{aligned}
\dot{\psi} &= \frac{\partial \psi^e}{\partial \boldsymbol{\varepsilon}^e}:\dot{\boldsymbol{\varepsilon}}-\frac{\partial \psi^e}{\partial \boldsymbol{\varepsilon}^e}:\dot{\boldsymbol{\varepsilon}}_{p} + \frac{\partial \psi}{\partial \boldsymbol{\alpha}}:\dot{\boldsymbol{\alpha}}\\
&=\frac{\partial \psi^e}{\partial \boldsymbol{\varepsilon}^e}:\dot{\boldsymbol{\varepsilon}}_{e}+ \frac{\partial \psi^p}{\partial \boldsymbol{\alpha}}:\dot{\boldsymbol{\alpha}},
\end{aligned}
\end{equation}
$$

代入到 Clausius-Duhem 不等式

$$
\boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}}-\dot{\psi}\geq0,
$$

有

$$
\boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}}-\frac{\partial \psi^e}{\partial \boldsymbol{\varepsilon}^e}:\dot{\boldsymbol{\varepsilon}}_{e}- \frac{\partial \psi}{\partial \boldsymbol{\alpha}}:\dot{\boldsymbol{\alpha}}\geq0,
$$

整理得到

$$
(\boldsymbol{\sigma}-\frac{\partial \psi^e}{\partial \boldsymbol{\varepsilon}^e}):\dot{\boldsymbol{\varepsilon}}_{e} + \boldsymbol{\sigma}\dot{\boldsymbol{\varepsilon}}_{p} - \frac{\partial \psi}{\partial \boldsymbol{\alpha}}:\dot{\boldsymbol{\alpha}}\geq0,
$$

由于弹性应变速率 $\dot{\boldsymbol{\varepsilon}}_{e}$ 可以取任意方向和任意大小，而 $\boldsymbol{\sigma}-\frac{\partial \psi^e}{\partial \boldsymbol{\varepsilon}^e}$ 在弹性阶段不受速率影响，因此必须有

$$
\boldsymbol{\sigma}=\frac{\partial \psi^e}{\partial \boldsymbol{\varepsilon}^e},
$$

此外

$$
\mathbf{A} \equiv \frac{\partial \psi^p}{\partial \boldsymbol{\alpha}}
$$

为**硬化热力学力**，

$$
\Upsilon^p(\boldsymbol{\sigma},\mathbf{A};\dot{\boldsymbol{\varepsilon}}^{p},\dot{\boldsymbol{\alpha}}) \equiv \boldsymbol{\sigma}\dot{\boldsymbol{\varepsilon}}_{p} - \frac{\partial \psi}{\partial \boldsymbol{\alpha}}:\dot{\boldsymbol{\alpha}}
$$

为**塑性耗散函数**

对于各向同性的线弹性材料，自由能形式为

$$
\begin{equation}
\psi^e = \frac{1}{2}\boldsymbol{\varepsilon}^{e}:\mathbf{D}^{e}:\boldsymbol{\varepsilon}^{e}=G\boldsymbol{\varepsilon}^{e}_{d}:\boldsymbol{\varepsilon}^{e}_{d}+\frac{K}{2}\text{tr}(\boldsymbol{\varepsilon}^{e})^2,
\end{equation}
$$

其中，$\boldsymbol{\varepsilon}^{e}_{d} = \text{dev}(\boldsymbol{\varepsilon}^{e})$ 是 $\boldsymbol{\varepsilon}^{e}$ 的偏张量部分

```{note} 
:class: tip, dropdown

$$
\boldsymbol{\sigma}=\mathbf{D}^e:\boldsymbol{\varepsilon}^{e} = 2G\ \text{dev}(\boldsymbol{\varepsilon}^{e})+K\text{tr}(\boldsymbol{\varepsilon}^{e})\mathbf{I}
$$
```

例如，通常各向同性硬化自由能为

$$
\psi = \frac{1}{2} \boldsymbol{\varepsilon}^{e} : \mathbf{D}^{e} : \boldsymbol{\varepsilon}^{e} + \frac{1}{2} \mathbf{H} \boldsymbol{\alpha}^2,
$$

运动硬化自由能为

$$
\psi = \frac{1}{2} \boldsymbol{\varepsilon}^{e} : \mathbf{D}^{e} : \boldsymbol{\varepsilon}^{e} + \frac{1}{2} c (\boldsymbol{\alpha} - \boldsymbol{\alpha}_0)^2.
$$

## 塑性流动势

塑性流动势是用来描述材料在塑性变形时，塑性应变速率与应力之间关系的函数。它决定了材料在屈服后的流动方向和变形规律，是建立塑性本构关系的重要基础

塑性流动势通常可以写为

$$
\Psi=\Psi(\boldsymbol{\sigma},\mathbf{A}),
$$

塑性流动方向为（模长不为 $1$）

$$
\mathbf{N} \equiv \frac{\partial \Psi}{\partial \boldsymbol{\sigma}},
$$

若硬化规则使用相同的流动势，则

$$
\mathbf{H} \equiv -\frac{\partial \Psi}{\partial \mathbf{A}}.
$$

此时，$\Psi$ 是一个非负的，关于 $\boldsymbol{\sigma}$ 和 $\mathbf{A}$，且在原点处零值，即 $\Psi(\mathbf{0},\mathbf{0}) = 0$

## 关联塑性流动理论

关联塑性流动模型假定

$$
\Psi = \Phi,
$$

塑性应变和硬化变量的演化方程如下

$$
\begin{equation}
\begin{aligned}
\dot{\boldsymbol{\varepsilon}}^{p}&=\dot{\gamma}\frac{\partial \Phi}{\partial \boldsymbol{\sigma}},\\
\dot{\boldsymbol{\alpha}}&=-\dot{\gamma}\frac{\partial \Phi}{\partial \mathbf{A}},
\end{aligned}
\end{equation}
$$

其中，$\dot{\gamma}$ 是塑性乘子

### 最大塑性耗散原理

任何可行的应力状态 $(\boldsymbol{\sigma},\mathbf{A})$ 应满足 $\Phi(\boldsymbol{\sigma},\mathbf{A}) \leq 0$，把它们形成的集合记为 $\mathcal{A}$，最大塑性耗散原理揭示了，对于任意给定的塑性应变率 $\dot{\boldsymbol{\varepsilon}}^{p}$ 和 硬化内变量变化速率 $\dot{\boldsymbol{\alpha}}$，真实应力状态应满足

$$
\Upsilon^p(\boldsymbol{\sigma},\mathbf{A};\dot{\boldsymbol{\varepsilon}}^{p},\dot{\boldsymbol{\alpha}}) \geq \Upsilon^p(\boldsymbol{\sigma}^{*},\mathbf{A}^{*};\dot{\boldsymbol{\varepsilon}}^{p},\dot{\boldsymbol{\alpha}}),\quad \forall\ (\boldsymbol{\sigma}^{*},\mathbf{A}^{*})\in\mathcal{A},
$$

同时，Kuhn-Tucker 最优性条件对应为

$$
\Phi(\boldsymbol{\sigma},\mathbf{A}) \leq 0,\quad \dot{\gamma}\geq0,\quad \Phi(\boldsymbol{\sigma},\mathbf{A})\dot{\gamma}=0.
$$

最大塑性耗散原理及其关联性定律并非普遍适用。虽然该原理在晶体塑性和金属材料中得到了验证，但对于土壤等颗粒材料，实验结果常常与关联性定律不符。在这些情况下，需采用非关联性定律来更准确地描述材料行为