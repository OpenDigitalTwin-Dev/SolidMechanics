# 质量缩放

显式动力分析常用于求解高速瞬态问题（如碰撞和冲击），其稳定性取决于**临界时间步长**。临界时间步长由**材料波速**和**最小单元尺寸**共同决定。当模型中存在极小单元时，时间步长会显著减小，导致计算时间大幅增加。质量缩放通过调整单元质量来增大临界时间步长，从而有效提升计算效率

> L. Olovsson and K. Simonsson, "Iterative solution technique in selective mass scaling," Communications in Numerical Methods in Engineering, vol. 22, no. 1, pp. 77-82, 2006.

质量缩放策略在下述硕士论文过程中被引入到 CCX 中的

> C. Czech, "Efficiency evaluation of explicit finite element methods," Master' s thesis, Dept. of Civil, Geo and Environmental Engineering, Technical University of Munich, Germany, 2019.

在[波速](./sec1-timestep.md)一节中看到，波速与材料的力学性能和质量密度密切相关，密度越大，波速越慢，从而允许更大的临界时间步长。设目标最小时间步长为 ，对于每个网格单元，其临界时间步长为

$$
\delta {{t}_{\text{crit},i}}=\frac{{{L}_{i}}}{{{V}_{P,i}}}
$$

于是，对 $\delta {{t}_{\text{crit},i}}<\delta {{t}_{\text{tar}}}$ 的网格单元的密度进行缩放，缩放因子为

$$
{{s}_{i}}={{\left ({\frac{\delta {{t}_{\text{tar}}}}{\delta {{t}_{\text{crit},i}}}}\right )}^{2}},
$$

使用质量缩放虽然能够加速显式计算，但也导致了诸多问题

- 质量不守恒与能量不守恒
- 惯性效应失真
- 动力学响应失真
- 接触或边界条件异常

因此在使用质量缩放时应非常谨慎

- 减小缩放倍数（<10），尽量局部缩放而非全局缩放
- 只在准静态问题中使用，对于惯性主导的问题，避免使用质量缩放
- 后处理对相关量进行修正
- 优先优化网格划分