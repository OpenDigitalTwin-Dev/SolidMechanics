# Lagranigan 格式

拉格朗日格式（Lagrangian Formulation）是固体力学数值求解的基石，其核心在于采用物质坐标系描述运动，确立了计算网格与物质质点间的永久映射关系。在此框架下，网格随介质协同变形，使得求解器能够精确追踪材料的路径相关性（如塑性内变量的历史演化），并自动捕捉瞬时几何边界与接触界面。这种“物质跟随”的特性，从根本上契合了固体介质具有变形记忆与明确边界的物理本质


在大变形问题中，连续体构型的确定往往并不容易。设连续体在一系列载荷增量作用下依次经历如下构型序列：

$$
{}^{0}\Omega=\Omega_{0},\ {}^{1}\Omega,\ {}^{2}\Omega,\ \cdots,\ {}^{n-1}\Omega = \Omega_{1},\ {}^{n}\Omega = \Omega_{2}
$$

计算中通常选取某一参考构型，并结合外部载荷与边界条件来求解当前构型。若参考构型取为初始构型 ${}^{0}\Omega=\Omega_{0}$，则称为 Total Lagrangian 格式；若参考构型取为上一增量步的构型 ${}^{n-1}\Omega = \Omega_{1}$，则称为 Updated Lagrangian 格式，在 Updated Lagrangian 格式中，通常假定从 $\Omega_{1}$ 到 $\Omega_{2}$ 的载荷增量很小，而从 $\Omega_{0}$ 到 $\Omega_{1}$ 的载荷增量可以连续任意大

```{figure} ../../../images/Continuum/chap3/configurations.png
---
width: 400px
name: sec3-fig:configurations
---
初始构型，中间构型，当前构型
```