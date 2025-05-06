# 各向异性屈服准则

<span class="gray-text">
各向异性屈服准则能够更精确地描述具有方向依赖性的材料在不同加载方向上的屈服行为
</span>

Hill（1950）提出了各向异性形式的 von Mises 屈服准则，将原有的第二偏应力不变量 $J_{2}$ 替换为应力分量的一个更为一般的二次型函数

$$
\frac{1}{2} A_{ijkl} \sigma_{ij} \sigma_{kl} = \tau_{y}^2,
$$ (sec6-eq:anisotropic-1)

其中，$A_{ijkl} = A_{jikl} = A_{ijlk} = A_{klij}$ 是各向异性张量。将应力张量分解为静水压力部分和偏应力部分

$$
\sigma_{ij} = s_{ij} + p\delta_{ij},\quad p = \frac{1}{3}\sigma_{kk},
$$

于是式 {eq}`sec6-eq:anisotropic-1` 写为

$$
\frac{1}{2}A_{ijkl}s_{ij}s_{kl} + p A_{ijkk} s_{ij} + \frac{1}{2}p^2 A_{iijj} = \tau_{y}^2,
$$

如果塑性屈服准则与静水压力 $p$ 无关，则一定有 $A_{ijkk} = 0$，因此上式变为

$$
\frac{1}{2}A_{ijkl}s_{ij}s_{kl} = \tau_{y}^2.
$$ (sec6-eq:anisotropic-2)

当满足

$$
A_{ijkl} = \frac{1}{2} \left( \delta_{ik} \delta_{jl} + \delta_{il} \delta_{jk} \right) - \frac{1}{3} \delta_{ij} \delta_{kl}
$$

时，式 {eq}`sec6-eq:anisotropic-2` 退化为各向同性的 Mises 屈服准则

:::{admonition} 证明
:class: tip, dropdown

对于第一项

$$
\frac{1}{2} \left( \delta_{ik} \delta_{jl} + \delta_{il} \delta_{jk} \right)s_{ij}s_{kl} = \frac{1}{2}s_{ij}s_{ij}+\frac{1}{2}s_{ij}s_{ji} = s_{ij}s_{ij},
$$

对于第二项

$$
\frac{1}{3} \delta_{ij} \delta_{kl}s_{ij}s_{kl} = \frac{1}{3}s_{ii}s_{kk} = \frac{1}{3}\text{tr}(\mathbf{s})^{2} = 0.
$$

故式 {eq}`sec6-eq:anisotropic-2` 变为 

$$
\frac{1}{2}s_{ij}s_{ij} = J_{2} = \tau_{y}^2.
$$

:::


## Hill 正交各向异性屈服准则

Hill 正交各向异性屈服准则由 Hill 在 1948 年提出，在材料主轴系下表示为

$$
F(\sigma_{22} - \sigma_{33})^2 + G(\sigma_{33} - \sigma_{11})^2 + H(\sigma_{11} - \sigma_{22})^2 + 2L\sigma_{23}^2 + 2M\sigma_{31}^2 + 2N\sigma_{12}^2 = 1
$$ (sec6-eq:Hill)

- **材料主轴系**：指在该坐标系下，**材料的各向异性参数（如弹性模量、屈服参数等）矩阵为对角形式**，主方向之间不存在耦合项。材料主轴系是材料本身固有的属性，与外部加载方式无关，例如轧制方向、横向和厚度方向等，均属于主轴系的典型代表
- $F,G,H,L,M,N$：材料的各向异性参数
- **右侧为1**：归一化曲面

假设材料在主轴方向上的拉伸屈服应力为 $\sigma_{y1},\sigma_{y2},\sigma_{y3}$，则

$$
G+H = \frac{1}{\sigma_{y1}^{2}},\quad H+F = \frac{1}{\sigma_{y2}^{2}},\quad F+G = \frac{1}{\sigma_{y3}^{2}},
$$

于是解得

$$
\begin{equation}
\begin{aligned}
F &= \frac{1}{2} \left( \frac{1}{\sigma_{y2}^2} + \frac{1}{\sigma_{y3}^2} - \frac{1}{\sigma_{y1}^2} \right), \\
G &= \frac{1}{2} \left( \frac{1}{\sigma_{y3}^2} + \frac{1}{\sigma_{y1}^2} - \frac{1}{\sigma_{y2}^2} \right), \\
H &= \frac{1}{2} \left( \frac{1}{\sigma_{y1}^2} + \frac{1}{\sigma_{y2}^2} - \frac{1}{\sigma_{y3}^2} \right).
\end{aligned}
\end{equation}
$$

类似地，假设 $\tau_{y1},\tau_{y2},\tau_{y3}$ 分别是主轴面上的纯剪切屈服应力，则

$$
L = \frac{1}{2\tau_{y1}^2},\quad M = \frac{1}{2\tau_{y1}^2},\quad N=\frac{1}{2\tau_{y1}^2}.
$$

对于横向各向同性（例如，轴3平面各向同性），有

$$
N = F+2H = G+2H,\quad L=M.
$$

对于完全各向同性，有

$$
L=M=N=3F=3G=3H,
$$

此时，式 {eq}`sec6-eq:Hill` 退化为各向同性的 Mises 屈服准则

$$
\frac{1}{6}((\sigma_{22} - \sigma_{33})^2 + (\sigma_{33} - \sigma_{11})^2 + (\sigma_{11} - \sigma_{22})^2) + (\sigma_{23}^2 + \sigma_{31}^2 + \sigma_{12}^2) = J_{2} = \tau_{y}^2.
$$