# 物理方程

<span class="gray-text">
物理方程揭示了应变与应力之间的内在联系。通过实验研究与理论推导，对材料在不同载荷条件下的变形行为进行分析，建立了描述应力与应变关系的方程
</span>

在理想弹性体中，应变与应力的分量满足**胡克定律**

```{margin}
应力作用方向与应变方向之间的差异性
```

$$
\begin{equation}
\begin{aligned}
&\epsilon_x = \frac{1}{E} \left[ \sigma_x - \mu (\sigma_y + \sigma_z) \right],\\
&\epsilon_y = \frac{1}{E} \left[ \sigma_y - \mu (\sigma_z + \sigma_x) \right],\\
&\epsilon_z = \frac{1}{E} \left[ \sigma_z - \mu (\sigma_x + \sigma_y) \right],\\
&\gamma_{yz} = \frac{1}{G} \tau_{yz}, \quad \gamma_{zx} = \frac{1}{G} \tau_{zx}, \quad \gamma_{xy} = \frac{1}{G} \tau_{xy}.
\end{aligned}
\end{equation}
$$ (sec5-eq:strain-stress-1)

其中

```{margin}
由于假定材料具有完全弹性、均匀性和各向同性，这些常数不随应力应变的大小、位置或方向发生变化
```

1. $E$（**拉压弹性模量**）：又称**弹性模量**，是衡量材料在弹性范围内抵抗拉伸或压缩形变能力的物理量，反映材料的刚性或硬度
2. $G$（**切变模量**）：又称**剪切模量**或**刚度模量**，是描述材料在弹性范围内抵抗剪切形变能力的物理量，反映材料在受剪切力作用下的刚性
3. $\mu$（**泊松比**）：又称**泊松系数**，是描述材料在一个方向受拉伸或压缩时，横向形变与轴向形变之比的物理量，反映材料**变形**的各向异性特征

它们之间满足

$$
G = \frac{E}{2(1+\mu)}
$$ (sec5-eq:strain-stress-2)
