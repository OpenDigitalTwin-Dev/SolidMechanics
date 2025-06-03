# 时间步长策略

在显示动力学分析中（通过 `*DYNAMIC` 关键字激活），由于不需要在每个时间步求解线性或非线性方程组，因此在单个时间步的迭代过程中比隐式方法快得多。然而，显示方法的稳定性较差，通常需要选择较小的时间步长。因此，时间步长的选取策略至关重要，需要在求解稳定性和计算效率之间达到平衡

在CCX中，运动方程使用 HHT- 方法进行时间积分

> Miranda, I., Ferencz, R. M., & Hughes, T. J. R. An improved implicit-explicit time integration method for structural dynamics. Earthquake Engineering & Structural Dynamics, 18(5), 643-653, 1989.

该方法完全按照下述文献的描述实现

> Dhondt, G. The Finite Element Method for Three-Dimensional Thermomechanical Applications. John Wiley & Sons, 2004.

通过引入参数 $\alpha$，可以有效地耗散高频振荡，而不会显著影响低频响应

- $\alpha\in\left[-\frac{1}{3},0\right]$：控制高频耗散，$\alpha = -\frac{1}{3}$ 对应最大耗散
- $\alpha = 0$：$\alpha$ 方法退化为经典的 Newmark 方法，此时没有人格高频耗散

**显示方法是条件稳定的：最大时间步长与机械波穿过网格中最小单元所需的时间成正比（CFL条件）**

## CFL 条件

### 波速

纵波和横波是固体力学中常见的两种基本波动类型

- **纵波（Primary Wave）**：质点的振动方向与波的传播方向平行，通过**压缩-膨胀**传递动能，典型特征为介质中形成‌疏密相间‌的区域，可在固体、液体、气体中传播；例如声波，弹簧纵波

- **横波（Secondary Wave）**：质点的振动方向与波的传播方向垂直，通过**剪切变形**传递动能，通常表现为‌凹凸起伏‌的波形，仅能在固体或具有切变弹性的液体中传播；例如水波，电磁波

在各向同性弹性介质中，纵波的速度和横波的速度分别为

$$
{{V}_{P}}=\sqrt{\frac{\lambda +2\mu }{\rho }}=\sqrt{\frac{E(1-\nu )}{\rho (1+\nu )(1-2\nu )}},\quad {{V}_{S}}=\sqrt{\frac{\mu }{\rho }}=\sqrt{\frac{E}{2\rho (1+\nu )}},
$$

其中，$\lambda,\mu$ 是拉梅常数，$\mu$ 即剪切模量，$E$ 是弹性模量，$\nu$ 是泊松比，$\rho$ 是材料密度

在[应力-应变矩阵](../../Elasticity/chap1/sec5-physical-equa.md)中
- $\lambda +2\mu$ 是正应力-正应变关系的对角部分，代表了正向拉压的响应刚度（抵抗体积变化）
- $\mu$ 是切应力-切应变关系的对角部分，代表了剪切变形的响应刚度（抵抗形状变化）

波速比定义为

$$
\frac{{{V}_{P}}}{{{V}_{S}}}=\sqrt{\frac{\lambda +2\mu }{\mu }}=\sqrt{\frac{2(1-\nu )}{1-2\nu }}.
$$

## CFL 条件

CFL条件的本质：**数值方法只考虑了相邻网格间的流动，当时间步过大，物理过程实际产生了跨网格流动，这种不一致性会使得计算结果不稳定，因此需要缩短时间步长**

<span class="gray-text">
跨网格运动意味着通量计算时使用的物理量不准确，从而引发数值不稳定性
</span>

因此，时间步长需满足

$$
\delta t\le C{\min_{i}(}\frac{{{L}_{i}}}{{{V}_{i}}}),
$$

其中：

```{margin}
此处特征长度和波速均没有考虑方向
```

- $L_{i}$：网格单元 $i$ 的特征长度（通常是最小单元尺寸）
- $V_{i} = \max{(}{{V}_{P}},{{V}_{S}})$：在固体介质中，P 波传播速度通常大于 S 波，因此 ${{V}_{max}}={{V}_{P}}$
- $C$：安全因子，通常取为 $0.5$~$0.9$ 以保证稳定性

由此可见，P 波速度越大，稳定求解的时间步长越小；网格尺寸越小，稳定求解的时间步长也越小