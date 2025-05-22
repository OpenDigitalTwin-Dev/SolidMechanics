# 格林应变张量

<span class="gray-text">
格林应变张量（Green-Lagrange strain tensor）能够准确反映材料在大变形过程中的几何非线性特征，因此被广泛应用于非线性弹性力学、结构力学以及材料科学等领域
</span>

## 单轴应变度量

<span class="gray-text">
如何度量应变？
</span>

假设一根初始长度为 $L_{0}$ 的杆均匀伸长或缩短至长度 $L$，对于这种变形，存在多种不同的应变度量方式

### 工程应变

工程应变（又称名义应变）是基于物体**原始尺寸**的**小变形**线性近似

$$
\varepsilon_{eng} = \frac{L-L_{0}}{L_{0}}.
$$

- 计算简便
- 忽略了变形过程中几何形状的实时变化
- 忽略了几何非线性，无法准确描述大变形中的非线性效应，仅适用于小变形（通常应变 < 5%，弹性阶段）


### 真实应变

真实应变（自然应变）基于**瞬时尺寸**的**累积变形**，每一步应变增量均相对于当前长度计算，适用于连续变形过程，采用对数形式描述**大变形**

$$
\varepsilon_{true} = \int_{L_{0}}^{L}\frac{\mathrm{d}l}{l} = \ln\frac{L}{L_{0}}.
$$

- 具有可加性（同向变形），多个应变阶段的真实应变可直接相加
- 考虑了变形路径的影响，更符合物理实际
- 部分考虑了几何非线性

### 格林应变

```{margin}
有限应变理论（区分于小变形理论）是用于描述和分析材料或结构在发生较大、不可忽略几何非线性变形时的力学行为的理论体系
```

格林应变（Green-Lagrange应变）属于**有限应变理论**，基于变形前后长度的平方变化，是二阶张量形式，其一维形式如下

$$
\varepsilon_{Green} = \frac{1}{2}((\frac{L}{L_{0}})^2-1).
$$

- 包含位移梯度的线性项和二次项，完全考虑了几何非线性，适用于连续介质力学和有限元分析中的大变形问题
- 保持客观性（在刚体运动下不变），适合本构模型
- 格林应变在小变形极限下会退化为工程应变（线性应变张量）

## 格林应变张量

格林应变张量是连续介质力学中描述**有限变形**（即**大变形**）的重要工具之一。它在非线性弹性、超弹性材料本构模型以及有限元分析等领域具有重要地位。格林应变张量采用以初始构型为参考的拉格朗日描述，因此又被称为格林-拉格朗日应变张量

### 定义

格林应变张量基于变形前后长度的平方变化，通过对比变形前后任意两点间距离的差异来定义应变。参考构型中两点 $\mathbf{X}$ 和 $\mathbf{X}+\mathrm{d}\mathbf{X}$ 的距离平方为

$$
\mathrm{d}S^2 = \mathrm{d}\mathbf{X}\cdot\mathrm{d}\mathbf{X},
$$

变形后变为 $\mathbf{x}(\mathbf{X})$ 和 $\mathbf{x}(\mathbf{X}+\mathrm{d}\mathbf{X})$

$$
\begin{equation}
\begin{aligned}
\mathrm{d}s^2 &= \left|\mathbf{x}(\mathbf{X}+\mathrm{d}\mathbf{X}) - \mathbf{x}(\mathbf{X})\right|^2 \\
&\approx (\frac{\partial \mathbf{x}}{\partial \mathbf{X}}\mathrm{d}\mathbf{X})\cdot(\frac{\partial \mathbf{x}}{\partial \mathbf{X}}\mathrm{d}\mathbf{X}) \\
&= \mathrm{d}\mathbf{X}^{T}F^{T}F\mathrm{d}\mathbf{X}
\end{aligned}
\end{equation}
$$

于是

$$
\mathrm{d}s^2 - \mathrm{d}S^2 = \mathrm{d}\mathbf{X}^{T}(F^{T}F-I)\mathrm{d}\mathbf{X} = 2\ \mathrm{d}\mathbf{X}^{T}E\mathrm{d}\mathbf{X},
$$

定义格林应变张量为

$$
\mathbf{E} = \frac{1}{2}(F^{T}F-I),
$$

代入 $F = \frac{\partial \mathbf{u}}{\partial \mathbf{X}} + I$，得到

$$
\begin{equation}
\begin{aligned}
\mathbf{E}  &= \frac{1}{2}((\frac{\partial \mathbf{u}}{\partial \mathbf{X}} + I)^{T}(\frac{\partial \mathbf{u}}{\partial \mathbf{X}} + I) - I)\\
& = \frac{1}{2}((\frac{\partial \mathbf{u}}{\partial \mathbf{X}})^{T} + (\frac{\partial \mathbf{u}}{\partial \mathbf{X}}) + (\frac{\partial \mathbf{u}}{\partial \mathbf{X}})^{T}(\frac{\partial \mathbf{u}}{\partial \mathbf{X}})),
\end{aligned}
\end{equation}
$$

于是

$$
E_{ij} = \frac{1}{2}(\frac{\partial u_{i}}{\partial X_{j}} +\frac{\partial u_{j}}{\partial X_{i}} +  \frac{\partial u_{k}}{\partial X_{i}}\frac{\partial u_{k}}{\partial X_{j}}),
$$

- $\frac{\partial u_{i}}{\partial X_{j}} +\frac{\partial u_{j}}{\partial X_{i}}$：对应线性应变部分（与小变形理论中一致）
- $\frac{\partial u_{k}}{\partial X_{i}}\frac{\partial u_{k}}{\partial X_{j}}$：非线性项，由有限应变引起，在小变形下可忽略


### 性质

#### 对称性

$$
\mathbf{E} ^{T} = \mathbf{E} .
$$

#### 客观性

格林应变张量的客观性指其在刚体运动（平移、旋转）下保持不变，即仅反映材料的真实变形

将整个过程分解为纯变形和刚体运动（$\mathbf{x}$ 为纯变形后的位置）

$$
\mathbf{x}' = Q\mathbf{x}+\mathbf{c},
$$

其中，$Q$ 是常正交矩阵，$\mathbf{c}$ 是常向量，于是

$$
F' = \frac{\partial \mathbf{x}'}{\partial \mathbf{X}} = Q\frac{\partial \mathbf{x}}{\partial \mathbf{X}} = QF,
$$

于是

$$
\mathbf{E} ' = \frac{1}{2}((F')^{T}F' - I) =  \frac{1}{2}(F^{T}Q^{T}QF - I) = \frac{1}{2}(F^{T}F - I) = \mathbf{E} .
$$

这也可以通过矩阵的[极分解](../chap1/sec1-OT.md)得出，任意矩阵都可以分解为正交矩阵（表示刚体运动）$R$ 和对称半正定矩阵（表示形状变化）$U$ 的乘积

$$
F = RU,
$$

于是

$$
\mathbf{E}  = \frac{1}{2}(U^{T}R^{T}RU - I) = \frac{1}{2}(U^{T}U - I),
$$

这意味着在 $\mathbf{E} $ 中，刚体运动被消除了