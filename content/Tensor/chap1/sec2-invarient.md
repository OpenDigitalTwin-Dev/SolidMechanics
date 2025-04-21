# 张量不变量

<span class="gray-text">
张量不变量是张量在坐标变换下保持不变的标量量。这些不变量反映了张量的内在几何或物理特性，与观察的坐标系无关
</span>

## 主不变量

对于二阶张量 $\mathbf{T}$，主不变量由张量的特征方程定义

$$
\begin{equation}
\begin{aligned}
0=\det(\lambda \mathbf{I} - \mathbf{T}) &= (\lambda-\lambda_{1})(\lambda-\lambda_{2})(\lambda-\lambda_{3}) \\
&= \lambda^{3} - I_{1}\lambda^{2}+I_{2}\lambda - I_{3},
\end{aligned}
\end{equation}
$$

其中，$\lambda_{1},\lambda_{2},\lambda_{3}$ 是张量的特征值，$I_{1},I_{2},I_{3}$ 是三个主不变量

- 第一主不变量：

$$
I_{1} = \lambda_{1}+\lambda_{2}+\lambda_{3} = \text{tr}(\mathbf{T}) := \sum_{i}T_{ii},
$$

- 第二不变量：

$$
I_{2} = \lambda_{1}\lambda_{2}+\lambda_{2}\lambda_{3}+\lambda_{3}\lambda_{1} = \frac{1}{2}\left(\text{tr}(\mathbf{T}\right)^2 - \text{tr}(\mathbf{T}^2)),
$$

- 第三不变量：

$$
I_{3} = \lambda_{1}\lambda_{2}\lambda_{3} = \det(\mathbf{T}),
$$