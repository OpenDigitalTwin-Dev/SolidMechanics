# 张量不变量

<span class="gray-text">
张量不变量是张量在坐标变换（基变换）下保持不变的标量量，这些不变量与观察的坐标系无关，反映了张量的内在几何或物理特性
</span>

## 应力张量不变量

### 主不变量

对于应力张量 $\boldsymbol{\sigma}$（对称张量），其不变量由张量的特征方程定义

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
I_{1} = \sigma_{1}+\sigma_{2}+\sigma_{3} = \text{tr}(\boldsymbol{\sigma}) := \sigma_{ii},
$$ (sec2-eq:stress-1st-priinvar)

第一主不变量 $I_{1}$ 与**平均应力**（静水压力）$\sigma_{m}$ 相关

$$
\sigma_{m} = \frac{1}{3}(\sigma_{1} + \sigma_{2} + \sigma_{3})=\frac{1}{3}I_{1},
$$

平均应力描述了材料在各个方向上的平均应力状态，反映了材料在受力后的**体积变化**趋势（膨胀或压缩）

#### 第二主不变量

$$
\begin{equation}
\begin{aligned}
I_{2} &= \sigma_{1}\sigma_{2}+\sigma_{2}\sigma_{3}+\sigma_{3}\sigma_{1} \\
&=\frac{1}{2}((\sigma_{1}+\sigma_{2}+\sigma_{3})^2 - (\sigma_{1}^2+\sigma_{2}^2+\sigma_{3}^2)) \\
&= \frac{1}{2}\left(\text{tr}(\boldsymbol{\sigma}\right)^2 - \text{tr}(\boldsymbol{\sigma}^2))\\
&=\frac{1}{2}(\sigma_{ii}\sigma_{jj} - \sigma_{ij}\sigma_{ij}) \\
&=\frac{1}{2}((\sigma_{11}+\sigma_{22}+\sigma_{33})^2 - (\sigma_{11}^{2}+\sigma_{22}^{2}+\sigma_{33}^{2}+2(\sigma_{12}\sigma_{21} +\sigma_{23}\sigma_{32}+\sigma_{31}\sigma_{13})))\\
&=\sigma_{11}\sigma_{22}+\sigma_{22}\sigma_{33}+\sigma_{33}\sigma_{11} - \sigma_{12}^{2} -\sigma_{23}^{2}-\sigma_{31}^{2},
\end{aligned}
\end{equation}
$$ (sec2-eq:stress-2nd-priinvar)

第二主不变量 $I_{2}$ 通常用于分析材料的**剪切变形和破坏**。这一不变量在塑性理论中具有重要意义，因为它与**剪切应力**和材料的**屈服条件**有关。例如，Von Mises屈服准则基于第二主不变量来描述材料在复杂应力状态下的屈服状态

#### 第三主不变量

$$
I_{3} = \sigma_{1}\sigma_{2}\sigma_{3} = \det(\boldsymbol{\sigma}),
$$ (sec2-eq:stress-3rd-priinvar)

第三主不变量 $I_{3}$ 反映了主应力的组合关系。在损伤力学和断裂力学中，$I_{3}$ 的正负在主应力同号时可以用来区分拉伸主导状态（全部主应力为正）与压缩主导状态（全部主应力为负）

### 偏不变量

#### 应力张量分解

将应力张量分解为**球形张量**（体积应力$\rightarrow$体积变化）和**偏斜张量**（剪切应力$\rightarrow$形状变化）的和

$$
\boldsymbol{\sigma} = \frac{I_{1}}{3}\mathbf{I}+\mathbf{s},
$$

偏应力张量 $\mathbf{s} = \boldsymbol{\sigma}-\frac{I_{1}}{3}\mathbf{I}$，是从总应力张量中去除体积应力（即平均正应力）后的部分，反映了材料内部的纯剪切作用。$\mathbf{s}$ 的特征根 

$$
s_{i}=\sigma_{i}-\frac{I_{1}}{3}
$$

称为**主偏应力**，满足

$$
s_{1}+s_{2}+s_{3} = 0.
$$

#### 第一偏不变量

$$
J_{1} = \text{tr}(\mathbf{s})\equiv0,
$$ (sec2-eq:stress-1st-parinvar)

表明偏应力张量仅描述剪切变形，与体积变形无关

#### 第二偏不变量

$$
J_{2} = \frac{1}{2}\mathbf{s}:\mathbf{s} = \frac{1}{2}s_{ij}s_{ij},
$$ (sec2-eq:stress-2nd-parinvar-0)

```{margin}
von Mises 等效应力是一种把复杂三维应力状态“等效”为单轴拉伸应力的方法，便于判断材料是否屈服
```

$J_{2}$ 反映了材料内部剪切应力的强度，是von Mises屈服准则的基础，在 von Mises 屈服准则中，von Mises 等效应力为

$$
\sqrt{3J_{2}}=:\sigma_{eq} \geq \sigma_{y},
$$

其中，$\sigma_{y}$ 为材料的屈服强度

:::{admonition} 等价形式
:class: tip, dropdown

1. ‌主偏应力平方和形式

$$
J_{2} = \frac{1}{2}(s_{1}^{2} + s_{2}^{2} + s_{3}^{2}),
$$ (sec2-eq:stress-2nd-parinvar-1)

因为 $s_{1}^{2},s_{2}^{2},s_{3}^{2}$ 是 $\mathbf{s}^{2}$ 的特征值，故 $\text{tr}(\mathbf{s}^{2}) = s_{1}^2 + s_{2}^2 + s_{3}^2$，由于 $\mathbf{s}$ 是对称张量，因此

$$
s_{ij}s_{ij} = \text{tr}({\mathbf{s}^{2}}) = s_{1}^2 + s_{2}^2 + s_{3}^2.
$$

2. 主应力差形式

$$
J_{2} = \frac{1}{6}((\sigma_{1}-\sigma_{2})^{2} + (\sigma_{2}-\sigma_{3})^{2} + (\sigma_{3}-\sigma_{1})^{2}),
$$ (sec2-eq:stress-2nd-parinvar-2)

代入 $s_{i} = \sigma_{i} - \frac{I_{1}}{3}$ 到式 {eq}`sec2-eq:stress-2nd-parinvar-1`，整理得到式 {eq}`sec2-eq:stress-2nd-parinvar-2`

3. ‌应力不变量组合形式

$$
J_{2} = \frac{I_{1}^{2}}{3} - I_{2},
$$ (sec2-eq:stress-2nd-parinvar-3)

代入 $I_{1} = \sigma_{1} + \sigma_{2} + \sigma_{3}$ 和 $I_{2}=\sigma_{1}\sigma_{2}+\sigma_{2}\sigma_{3}+\sigma_{3}\sigma_{1}$ 到式 {eq}`sec2-eq:stress-2nd-parinvar-2`，整理得到式 {eq}`sec2-eq:stress-2nd-parinvar-3`

4. ‌一般应力分量形式

$$
J_{2} = \frac{1}{6} \left[ (\sigma_{11} - \sigma_{22})^2 + (\sigma_{22} - \sigma_{33})^2 + (\sigma_{33} - \sigma_{11})^2 + 6(\sigma_{12}^2 + \sigma_{23}^2 + \sigma_{31}^2) \right],
$$ (sec2-eq:stress-2nd-parinvar-4)

代入 

$$
I_{1} = \sigma_{11}+\sigma_{22}+\sigma_{33}$$ 

和 

$$
I_{2}=\sigma_{11}\sigma_{22}+\sigma_{22}\sigma_{33}+\sigma_{33}\sigma_{11} - \sigma_{12}^{2} -\sigma_{23}^{2}-\sigma_{31}^{2}
$$

到式 {eq}`sec2-eq:stress-2nd-parinvar-3` 整理得到式 {eq}`sec2-eq:stress-2nd-parinvar-4`

:::


#### 第三偏不变量

$$
J_{3} = s_{1}s_{2}s_{3}=\det(\mathbf{s}),
$$

$J_{3}$ 在屈服准则、破坏模式分析及本构模型中有重要应用

## 应变张量不变量

<span class="gray-text">
完全类似于应力张量不变量
</span>

对于应变张量 $\boldsymbol{\varepsilon}$（对称张量），$\varepsilon_{1},\varepsilon_{2},\varepsilon_{3}$ 是三个主应变，其大小等于 $\boldsymbol{\varepsilon}$ 的特征值

### 主不变量

#### 第一主不变量

$$
I_{1} = \varepsilon_{1}+\varepsilon_{2}+\varepsilon_{3} = \text{tr}(\boldsymbol{\sigma}) := \varepsilon_{ii},
$$ (sec2-eq:strain-1st-priinvar)

#### 第二主不变量

$$
\begin{equation}
\begin{aligned}
I_{2} &= \varepsilon_{1}\varepsilon_{2}+\varepsilon_{2}\varepsilon_{3}+\varepsilon_{3}\varepsilon_{1} \\
&=\frac{1}{2}((\varepsilon_{1}+\varepsilon_{2}+\varepsilon_{3})^2 - (\varepsilon_{1}^2+\varepsilon_{2}^2+\varepsilon_{3}^2)) \\
&= \frac{1}{2}\left(\text{tr}(\boldsymbol{\varepsilon}\right)^2 - \text{tr}(\boldsymbol{\varepsilon}^2))\\
&=\frac{1}{2}(\varepsilon_{ii}\varepsilon_{jj} - \varepsilon_{ij}\varepsilon_{ij}) \\
&=\frac{1}{2}((\varepsilon_{11}+\varepsilon_{22}+\varepsilon_{33})^2 - (\varepsilon_{11}^{2}+\varepsilon_{22}^{2}+\varepsilon_{33}^{2}+2(\varepsilon_{12}\varepsilon_{21} +\varepsilon_{23}\varepsilon_{32}+\varepsilon_{31}\varepsilon_{13})))\\
&=\varepsilon_{11}\varepsilon_{22}+\varepsilon_{22}\varepsilon_{33}+\varepsilon_{33}\varepsilon_{11} - \varepsilon_{12}^{2} -\varepsilon_{23}^{2}-\varepsilon_{31}^{2},
\end{aligned}
\end{equation}
$$ (sec2-eq:strain-2nd-priinvar)

#### 第三主不变量

$$
I_{3} = \varepsilon_{1}\varepsilon_{2}\varepsilon_{3} = \det(\boldsymbol{\varepsilon}),
$$ (sec2-eq:strain-3rd-priinvar)

### 偏不变量

将应变张量分解为**球形张量**（体积应变$\rightarrow$体积变化）和**偏斜张量**（剪切应变$\rightarrow$形状变化）的和

$$
\boldsymbol{\varepsilon} = \frac{I_{1}}{3}\mathbf{I}+\mathbf{e},
$$

偏应变张量 $\mathbf{e} = \boldsymbol{\varepsilon}-\frac{I_{1}}{3}\mathbf{I}$，是从总应变张量中去除体积应变后的部分，反映了材料内部的纯剪切变形。$\mathbf{e}$ 的特征根 

$$
e_{i}=\sigma_{i}-\frac{I_{1}}{3}
$$

称为**主偏应变**，满足

$$
e_{1}+e_{2}+e_{3} = 0.
$$

#### 第一偏不变量

$$
J_{1} = \text{tr}(\mathbf{e})\equiv0,
$$ (sec2-eq:strain-1st-parinvar)

表明偏应变张量仅描述剪切变形，与体积变形无关

#### 第二偏不变量

#### 第三偏不变量

## 应变率张量不变量