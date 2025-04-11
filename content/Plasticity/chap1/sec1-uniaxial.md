# 单轴拉伸实验

## 实验现象

以金属棒的单轴拉伸实验为例，实验分为三个阶段：

- 阶段1：初始弹性加载（$O_{0} \rightarrow Y_{0}$）
- 阶段2：首次塑性加载与卸载（$Y_{0} \rightarrow Z_{0} \rightarrow O_{1}$）
- 阶段3：再加载与新塑性阶段（$O_{1} \rightarrow Y_{1} \rightarrow Z_{1}$）

```{margin}
实验过程力求做到均匀变形，故应力应变曲线是均匀变形假设下的近似，分析结果时使用均匀化假设（应力/应变均匀）
```

```{figure} ../../../images/Plasticity/chap1/uniaxial.png
---
width: 400px
name: sec1-fig:uniaxial
---
金属单轴拉伸应力-应变曲线
```

- 阶段1：在 $Y_{0}$ 之前，应力与应变成线性比例（胡克定律），斜率为弹性模量 $E$，若在 $Y_{0}$ 点前卸载，则材料沿原路径返回 $O_{0}$，无残余应变

```{margin}
残余塑性应变影响了材料的性质
```

- 阶段2：超过 $Y_{0}$ （屈服极限）后，材料进入塑性阶段（斜率显著变化），此时，应变包含**弹性**部分和**塑性**部分；从 $Z_{0}$ 开始卸载，应力-应变沿**近似平行**于初始弹性段的直线下降至 $O_{1}$，此时应力和弹性应变降至 0，且存在永久塑性应变 $\varepsilon_{p}$

- 阶段3：再加载，$O_{1} \rightarrow Y_{1}$ 仍为弹性段，但屈服极限提高至 $\sigma_{Y_{1}}$，超过 $Y_{1}$ 后，开始发生塑性流动




```{margin}
延性材料是指在受力时能够发生显著塑性变形而不发生断裂的材料
```

```{admonition} 材料案例
:class: tip, dropdown

- 金属（典型延性材料）：适用于单轴拉伸或压缩试验，能够直接观察到材料的弹性区域、塑性流动以及硬化行为，其中硬化主要表现为各向同性

- 土壤/岩石（非延性材料）：几乎不存在抗拉强度，单轴拉伸试验意义不大。通常通过三轴剪切试验来研究其剪切塑性变形特性

- 混凝土、复合材料：表现出拉压不对称的力学行为，损伤与塑性变形相互耦合。需结合多轴加载和非比例路径试验捕捉材料的各向异性特征
```


## 本构模型

### 理想应力-应变曲线

通过均匀变形假设，对应力-应变曲线进行简化，得到理想应力-应变曲线。在理想化曲线中

- 弹性区域与弹塑性区域之间的过渡体现为曲线斜率的非连续变化

```{margin}
因此，当材料被卸载后再次加载时，应力应变曲线会沿着同一条路径返回到**原始曲线**上
```

- 卸载和重新加载曲线之间的差异被忽略，并假设卸载起始点 $Z_{0}$ 与随后重新加载时的塑性屈服起始点 $Y_{1}$ 重合

```{figure} ../../../images/Plasticity/chap1/uniaxial-model.png
---
width: 400px
name: sec1-fig:uniaxial-model
---
理想应力-应变曲线
```

### 应变的加法分解

塑性力学小应变理论的基本假设是将总应变分解为**弹性应变**（可逆）和**塑性应变**（不可逆）：

$$
\varepsilon = \varepsilon^{e} + \varepsilon^{p},
$$

其中

- 弹性应变：$\sigma = E\varepsilon^{e} = E(\varepsilon-\varepsilon^{p})$

- 塑性应变：$\varepsilon^{p}$ 为永久变形，**与加载历史相关**

### 屈服函数

定义屈服函数用于判断材料是否进入塑性流动

$$
\Phi(\sigma,\sigma_{y}) = \left|\sigma\right| - \sigma_{y},
$$

其中，$\sigma_{y}$ 为当前屈服应力。定义弹性域为

$$
\mathcal{E} = \{ \sigma \mid \Phi(\sigma, \sigma_y) < 0 \} \quad \text{即} \quad |\sigma| < \sigma_y,
$$

当

```{margin}
记号：$\dot{\varepsilon} = \frac{\partial \varepsilon}{\partial t}$
```

- $\Phi<0$：材料处于弹性状态（$\dot{\varepsilon}=0$）

- $\Phi=0$：材料处于屈服边界，可能发生弹性卸载（$\dot{\varepsilon}^{p}=0$）或塑性加载（$\dot{\varepsilon}^{p}\neq0$）


在塑性加载过程中，‌应力状态的演化必须与屈服面的变化同步

$$
\Phi\equiv0 \quad \rightarrow \quad
\dot{\Phi}\equiv0,
$$

被称为**一致性条件**

### 塑性流动规则

塑性应变速率 $\dot{\varepsilon}^{p}$ 可正（拉伸），可负（压缩），定义塑性乘子，表示塑性流动的速率

$$
\dot{\varepsilon}^{p} = \dot{\gamma}\cdot\text{sign}(\sigma),
$$

因此

$$
\dot{\gamma}\geq0.
$$

塑性流动的发生（从弹性状态转为塑性状态）需满足**互补条件**

$$
\begin{align}
\Phi\cdot\dot{\gamma} &= 0,
\end{align}
$$

互补条件用来控制塑性流动的启停，明确区分弹性与塑性阶段

### 硬化法则

硬化法则用于描述材料在塑性变形过程中**‌屈服应力随塑性应变增加而演化‌**的现象（即材料变硬或变软），硬化函数

$$
\sigma_{y} = \sigma_{y}(\bar{\varepsilon}^{p}),
$$

其中，$\bar{\varepsilon}^{p}$ 是累积轴向塑性应变

$$
\bar{\varepsilon}^p \equiv \int_0^t |\dot{\varepsilon}^p| \, \mathrm{d}t,
$$

因此，在单调拉伸试验‌中，有

$$
\bar{\varepsilon}^p = \varepsilon^p,
$$

在单调压缩试验‌中，有

$$
\bar{\varepsilon}^p = -\varepsilon^p,
$$

因此

$$
\dot{\bar{\varepsilon}}^p = \left|\dot{\varepsilon}^{p}\right|=\dot{\gamma}.
$$

硬化函数 $\sigma_{y}(\bar{\varepsilon}^{p})$ 的图像被称称为硬化曲线

### 塑性乘子

在塑性加载过程中，满足

$$
\dot{\Phi} = \text{sign}(\sigma) \cdot \dot{\sigma} - H \cdot \dot{\bar{\varepsilon}}^p = 0,
$$

其中 $H=\frac{\partial \sigma_{y}}{\partial \bar{\varepsilon}^p}$ 为**硬化模量**，是描述材料塑性流动难易程度的重要指标，当

- $H>0$：材料表现出硬化特性，即在屈服后其承载能力增强，更难变形

- $H=0$：材料表现为理想塑性，即屈服后承载能力保持不变

- $H<0$：材料表现出软化特性，即在屈服后其承载能力下降，更易变形

将

$$
\begin{equation}
\dot{\sigma} = E(\dot{\varepsilon} - \dot{\varepsilon}^p) = E(\dot{\varepsilon} - \dot{\gamma} \cdot \text{sign}(\sigma)),
\end{equation}
$$ (sec1-eq:stress-rate)

和

$$
\dot{\bar{\varepsilon}}^p =\dot{\gamma},
$$

代入上式得到

$$
E(\dot{\varepsilon} \cdot \text{sign}(\sigma) - \dot{\gamma}) - H\dot{\gamma} = 0,
$$

因此

$$
\begin{equation}
\dot{\gamma} = \frac{E}{H + E} \cdot \text{sign}(\sigma) \cdot \dot{\varepsilon} = \frac{E}{H + E} |\dot{\varepsilon}|.
\end{equation}
$$ (sec1-eq:plasticity-multiplier)

#### 弹塑性切线模量

将式 {eq}`sec1-eq:plasticity-multiplier` 代入到应力率表达式 {eq}`sec1-eq:stress-rate`中，得到

$$
\begin{equation}
\dot{\sigma} = E \dot{\varepsilon} \left(1 - \frac{E}{E + H}\right) = \frac{EH}{E + H} \dot{\varepsilon} = E_{ep}\cdot\dot{\varepsilon},
\end{equation}
$$ (sec1-eq:Eep01)

其中

$$
E_{ep}=\frac{EH}{E+H}
$$

为**弹塑性切线模量**，其值小于弹性模量 $E$，且随硬化模量 $H$ 增大而增大

由于

$$
E_{ep}=\frac{\dot{\sigma}}{\dot{\varepsilon}} = \frac{\partial \sigma}{\partial \varepsilon},
$$

因此，$E_{ep}$ 是应力-应变曲线的切线斜率，反映了材料在塑性阶段的刚度

此外，可以用 $E_{ep}$ 表示硬化模量 $H$

$$
H = \frac{E^{ep}}{1 - E^{ep}/E}.
$$