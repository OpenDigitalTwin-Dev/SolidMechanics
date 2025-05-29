# 运动硬化模型（Kinematic Hardening）

<span class="gray-text">
Kinematic Hardening 描述的是材料在经历塑性变形后，屈服面整体在应力空间中移动，而形状和尺寸均保持不变
</span>

为了解释 **[Bauschinger 效应](../chap1/sec2-uniaxial.md)**和**各向异性硬化**，从而更好地描述材料在循环载荷下的反应，Melan 和 Prager 引入了运动硬化简单模型

根据该模型，在塑性变形过程中，初始屈服曲面的大小和形状不会改变，而是在应力空间中**平移**。如果屈服准则与压力无关，则可以假定

$$
f(\mathbf{s} - \boldsymbol{\alpha},K_{0}) = 0,\quad K_{0}=\text{const}.,
$$

其中

- $\boldsymbol{\alpha}$：表示屈服面（在应力空间中）的中心，反映了材料内部因历史塑性变形而产生的一种“反作用”，因此也被称为背应力
- $f$：关于应力差 $\mathbf{s} - \boldsymbol{\alpha}$ 的各向同性函数
- $K_{0}$：代表屈服面的大小，反映了材料的屈服强度

此时，持续塑性变形的一致性条件为

$$
\frac{\partial f}{\partial \boldsymbol{\sigma}} : \left(\overset{\nabla}{\boldsymbol{\tau}} - \overset{\nabla}{\boldsymbol{\alpha}} \right) = 0,
$$

假定屈服面瞬时移动，则背应力的演化方程为

$$
\overset{\nabla}{\boldsymbol{\alpha}} = c(\alpha, \vartheta)\, \mathbf{D}^{\text{p}} + \mathbf{C}(\alpha, \vartheta)\, (\mathbf{D}^{\text{p}} : \mathbf{D}^{\text{p}})^{1/2},
$$ (sec2-eq:kinematic)

```{margin}
$k$ 阶齐次：$f(\lambda x) = \lambda^{k}f(x)$
```

上式关于塑性变形速率 $\mathbf{D}$ 是一阶齐次的，因此符合塑性变形的速率无关假设，即材料的塑性响应只依赖于应变路径，与加载的快慢（速率）无关（所有状态变量的演化只是速度改变，路径不变）

此时，硬化参数为

$$
H = c \left( \frac{\partial f}{\partial \boldsymbol{\sigma}} : \frac{\partial f}{\partial \boldsymbol{\sigma}} \right)
+ \left( \frac{\partial f}{\partial \boldsymbol{\sigma}} : \frac{\partial f}{\partial \boldsymbol{\sigma}} \right)^{1/2}
\left( \mathbf{C} : \frac{\partial f}{\partial \boldsymbol{\sigma}} \right).
$$

如果屈服函数为

$$
f = \frac{1}{2}(\mathbf{s} - \boldsymbol{\alpha}):(\mathbf{s} - \boldsymbol{\alpha}) - k_{0}^{2} = 0,
$$ (sec2-eq:yield-1)

此时

$$
\frac{\partial f}{\partial \boldsymbol{\sigma}} = \mathbf{s} - \boldsymbol{\alpha},
$$

加载速率为

$$
\dot{\gamma} = \frac{1}{H} \left( \mathbf{s} - \boldsymbol{\alpha} \right): \overset{\nabla}{\boldsymbol{\tau}},
$$

其中

$$
H = 2ck_{0}^{2} + \sqrt{2}k_{0}\mathbf{C}:(\mathbf{s} - \boldsymbol{\alpha}).
$$

## Prager 线性运动硬化模型

取 $\mathbf{C} = 0$，$c = 2h_{\text{t}}^{\text{p}}$，则式{eq}`sec2-eq:kinematic`为 Prager 线性运动硬化模型，根据式{eq}`intro-eq:strain-t` 和{eq}`sec2-eq:yield-1`，对应的弹塑性本构方程为

$$
\mathbf{D} = \left[ \mathbf{M}^{e} + \frac{1}{2 h_{\text{t}}^{\text{p}}} 
\frac{(\mathbf{s} - \boldsymbol{\alpha})\otimes(\mathbf{s} - \boldsymbol{\alpha})}
{(\mathbf{s} - \boldsymbol{\alpha}) : (\mathbf{s} - \boldsymbol{\alpha})} \right] : \nabla \boldsymbol{\tau},
$$

在塑性加载阶段，满足

$$
\frac{\partial f}{\partial \boldsymbol{\sigma}} : \overset{\nabla}{\boldsymbol{\tau}} = (\mathbf{s} - \boldsymbol{\alpha}) : \overset{\nabla}{\boldsymbol{\tau}} > 0.
$$

其逆形式为

$$
\overset{\nabla}{\boldsymbol{\tau}} = \left( \boldsymbol{\Lambda}^{\text{e}} - \frac{2\mu}{1 + h_{\text{t}}^{\text{p}}/\mu} \frac{(\mathbf{s} - \boldsymbol{\alpha})\otimes(\mathbf{s} - \boldsymbol{\alpha})}
{(\mathbf{s} - \boldsymbol{\alpha}) : (\mathbf{s} - \boldsymbol{\alpha})} \right) : \mathbf{D},
$$

类似地

$$
(\mathbf{s} - \boldsymbol{\alpha}) : \mathbf{D} > 0.
$$

若 $\boldsymbol{\alpha}$ 是偏张量，即 $\text{tr}(\boldsymbol{\alpha}) = 0$，则可与[上一节](./sec1-isotropichardening.md)中类似证明

$$
\begin{equation}
\begin{aligned}
(\mathbf{s} - \boldsymbol{\alpha}):\overset{\nabla}{\boldsymbol{\tau}} =\frac{2h_{\text{t}}^{\text{p}}}{1+h_{\text{t}}^{\text{p}}/\mu}\ (\mathbf{s} - \boldsymbol{\alpha}):\mathbf{D}.
\end{aligned}
\end{equation}
$$

## Armstrong-Frederick 非线性运动硬化模型

取 $c = 2h,\mathbf{C} = -c_{0}\boldsymbol{\alpha}$，其中，$h,c_{0}$ 是常材料参数，此时

$$
\overset{\nabla}{\boldsymbol{\alpha}} = 2h\, \mathbf{D}^{\text{p}} -c_{0}\boldsymbol{\alpha}\, (\mathbf{D}^{\text{p}} : \mathbf{D}^{\text{p}})^{1/2},
$$

非线性项（此处也称记忆项）的引入，使得反向塑性加载下的硬化模量与实验数据更加吻合。此时

$$
\mathbf{D}^{\text{p}} = \frac{1}{2h(1-m)}\frac{(\mathbf{s}-\boldsymbol{\alpha}):\overset{\nabla}{\boldsymbol{\tau}}}{(\mathbf{s}-\boldsymbol{\alpha}):(\mathbf{s}-\boldsymbol{\alpha})}\ (\mathbf{s}-\boldsymbol{\alpha}),
$$

其中

$$
m = \frac{c_{0}}{2h}\frac{(\mathbf{s}-\boldsymbol{\alpha}):\boldsymbol{\alpha}}{\left[(\mathbf{s}-\boldsymbol{\alpha}):(\mathbf{s}-\boldsymbol{\alpha})\right]^{1/2}}.
$$