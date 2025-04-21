# 张量不变量

<span class="gray-text">
张量不变量是张量在坐标变换（基变换）下保持不变的标量量。这些不变量反映了张量的内在几何或物理特性，与观察的坐标系无关
</span>

## 应力张量不变量

### 主不变量

对于 Cauchy 应力张量 $\boldsymbol{\sigma}$，其不变量由张量的特征方程定义

$$
\begin{equation}
\begin{aligned}
0=\det(\lambda \mathbf{I} - \boldsymbol{\sigma}) &= (\lambda-\lambda_{1})(\lambda-\lambda_{2})(\lambda-\lambda_{3}) \\
&= \lambda^{3} - I_{1}\lambda^{2}+I_{2}\lambda - I_{3},
\end{aligned}
\end{equation}
$$

其中，$\lambda_{1},\lambda_{2},\lambda_{3}$ 是张量的特征值，其值等于三个主应力 $\sigma_{1},\sigma_{2},\sigma_{3}$ 的大小，通过主应力，可以定义三个主不变量

#### 第一主不变量

$$
I_{1} = \sigma_{1}+\sigma_{2}+\sigma_{3} = \text{tr}(\boldsymbol{\sigma}) := \sum_{i}\boldsymbol{\sigma}_{ii},
$$

第一主不变量 $I_{1}$ 与**平均应力**（静水压力）$\sigma_{m}$ 相关

$$
\sigma_{m} = \frac{1}{3}(\sigma_{1} + \sigma_{2} + \sigma_{3})=\frac{1}{3}I_{1},
$$

平均应力反映了材料在各个方向上的平均应力状态，主导材料的**体积变化**（如压缩或膨胀）

#### 第二主不变量

$$
I_{2} = \sigma_{1}\sigma_{2}+\sigma_{2}\sigma_{3}+\sigma_{3}\sigma_{1} = \frac{1}{2}\left(\text{tr}(\boldsymbol{\sigma}\right)^2 - \text{tr}(\boldsymbol{\sigma}^2)),
$$

第二主不变量 $I_{2}$ 通常用于分析材料的**剪切变形和破坏**。这一不变量在塑性理论中具有重要意义，因为它与**剪切应力**和材料的**屈服条件**有关。例如，Von Mises屈服准则基于第二主不变量来描述材料在复杂应力状态下的屈服状态

#### 第三主不变量

$$
I_{3} = \sigma_{1}\sigma_{2}\sigma_{3} = \det(\boldsymbol{\sigma}),
$$

第三主不变量 $I_{3}$ 反映主应力组合的对称性

### 偏不变量

#### 应力张量分解

将应力张量分解为**球形张量**（体积应力，体积变化）和**偏斜张量**（剪切部分，形状变化）的和

$$
\boldsymbol{\sigma} = \frac{1}{3}I_{1}\mathbf{I}+\mathbf{S},
$$

偏张量 $\mathbf{S}$ 的不变量 $J_{2},J_{3}$ 主导塑性变形

#### 第二偏不变量

$$
J_{2} = \frac{1}{2}\mathbf{S}:\mathbf{S},
$$

#### 第三偏不变量

$$
J_{3} = \det(\mathbf{S}),
$$

## 应变张量不变量

## 应变率张量不变量