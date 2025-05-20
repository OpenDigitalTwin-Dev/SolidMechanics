# 客观应力率

## 应力率

应力率指的是材料内部应力随时间的变化率，用来描述在外力或变形作用下，材料内部应力的变化速度，根据链式法则，有

$$
\dot{\boldsymbol{\sigma}} = \frac{\mathrm{d} \boldsymbol{\sigma}}{\mathrm{d} t} = \frac{\partial \boldsymbol{\sigma}}{\partial t} + (\mathbf{v}\cdot\nabla)\boldsymbol{\sigma}.
$$

```{note}
:class: tip, dropdown
$$
\frac{\mathrm{d} \sigma_{ij}}{\mathrm{d} t} = \frac{\partial \sigma_{ij}}{\partial t} + \frac{\partial \sigma_{ij}}{\partial x_{k}}\frac{\partial x_{k}}{\partial t}
$$

写成张量形式后，$\mathbf{v}\cdot\nabla$ 是方向导数算子
```

建立本构关系时，必须使用纯变形下的应力率，以保证本构方程只反映材料在真实变形过程中的力学行为。然而，当物体发生刚体旋转时，应力张量的分量会因坐标系的旋转发生正交相似变换，即使此时物体并未发生真实形变，常规应力率 $\dot{\boldsymbol{\sigma}}$ 仍然不为零

:::{note}

平移运动不会影响应力分量，旋转运动则改变了坐标系（投影方式），从而改变了应力分量，因此在应力率不为 0
:::

## 客观应力率

常规应力率无法区分这种由坐标系旋转带来的表观变化与材料真实变形引起的应力变化，容易导致本构方程失去客观性。因此，引入客观应力率，用以**剔除刚体运动的影响**，使应力率准确反映材料在纯变形状态下的真实应力变化，从而保证本构关系的物理一致性

**由于对旋转速率的定义和处理方式不同**，衍生出了多种常见的客观应力率，包括 Jaumann 应力率、Truesdell 应力率和 Green-Naghdi 应力率等。这些应力率在连续介质力学和本构关系的研究中得到了广泛应用，能够较为准确地描述材料在不同变形情形下的应力演化过程

