# 运动硬化模型

<span class="gray-text">
Kinematic Hardening 描述的是材料在经历塑性变形后，屈服面整体在应力空间中移动，而形状和尺寸均保持不变
</span>

在实验中，能频繁观察到在一个方向加载到硬化后，相反方向对于塑性屈服的抵抗增加了，这种现象被称为 Bauschinger effect，通常使用运动硬化模型来描述

以 Mises 屈服准则为例，运动硬化模型表现为

$$
\Phi(\boldsymbol{\sigma},\boldsymbol{\beta})=\sqrt{3J_{2}(\mathbf{s}(\boldsymbol{\sigma}) - \boldsymbol{\beta})} - \sigma_{y},
$$

其中，$\boldsymbol{\eta}(\boldsymbol{\sigma},\boldsymbol{\beta})=\mathbf{s}(\boldsymbol{\sigma}) - \boldsymbol{\beta}$ 被称为相对应力张量，$\boldsymbol{\beta}$ 被成为背应力，描述了屈服面的平移，$\sigma_{y}$ 是常值，描述了屈服面的大小

特别注意的是，$\Phi(\boldsymbol{\sigma},\boldsymbol{\beta})$ 是关于 $\boldsymbol{\eta}$ 而非 $\boldsymbol{\sigma}$ 的各向同性函数

由于

$$
\mathbf{N} = \frac{\partial \Phi}{\partial \boldsymbol{\sigma}}=\sqrt{\frac{3}{2}}\frac{\boldsymbol{\eta}}{\|\boldsymbol{\eta}\|},
$$

因此

$$
\dot{\boldsymbol{\varepsilon}}^{p}=\dot{\gamma}\sqrt{\frac{3}{2}}\frac{\boldsymbol{\eta}}{\|\boldsymbol{\eta}\|}.
$$