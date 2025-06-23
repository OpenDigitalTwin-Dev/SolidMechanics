# 塑性

关键字：

- `*PLASTIC`

参考示例：

- [Wire Bending](../chap6/sec2-wirebending.md)

应紧接着 `*ELASTIC` 使用

## 硬化模型

`*PLASTIC` 关键字用于定义材料的塑性行为，它描述了材料在弹性阶段后的屈服和硬化特性，是金属等可塑性材料分析的核心，有五类硬化模型可选

- `ISOTROPIC`：默认选项，各向同性硬化模型，屈服面随塑性应变均匀扩展，常用于大多数金属
- `KINEMATIC`：屈服面整体平移，适用于循环加载等情况
- `COMBINED`：结合上述两种机制：屈服面扩展 + 屈服面平移
- `USER`：通过用户子程序自定义硬化曲线
- `JOHNSON COOK`：Johnson-Cook本构模型，常用于高速冲击、热-力耦合等复杂场景


如果**弹性数据是各向同性**的，则当 `STEP` 卡片上的 `NLGEOM` 参数被启用时，采用文献

> Simo, J.C., A framework for finite strain elastoplasticity based on maximum plastic dissipation and the multiplicative decomposition: Part I. Continuum formulation. Computer Methods in Applied Mechanics and Engineering. 66, 199-219 (1988).

> Simo, J.C., A framework for finite strain elastoplasticity based on maximum plastic dissipation and the multiplicative decomposition: Part II: computational aspects. Computer Methods in Applied Mechanics and Engineering. 68, 1-31 (1988).

的方法处理大应变粘塑性理论，否则使用线性理论。如果**弹性数据是正交各向异性**的，则采用无穷小应变模型，因此硬化最多只能是线性的。
此外，如果硬化曲线的温度数据点与 `*ELASTIC` 卡片的温度数据点不一致，则会在后者的点上进行插值。因此，对于弹性正交各向异性材料，建议在与弹性数据相同的温度下定义硬化曲线


### ISOTROPIC-KINEMATIC-COMBINED

对于 `ISOTROPIC`，`KINEMATIC` 和 `COMBINED` 的情形，通过一组或多组 

<p style="text-align:center; font-weight:bold;">
  Von Mises 应力 — 等效塑性应变 — 温度
</p>

值来定义**硬化曲线**，例如

```
*PLASTIC, HARDENING=ISOTROPIC
800.  ,0.    ,273.
900.  ,0.05  ,273.
1000. ,0.15  ,273.
700.  ,0.    ,873.
750.  ,0.04  ,873.
800.  ,0.13  ,873.
```

定义了两条应力应变曲线，一条对应温度 $T=273$，一条对应温度 $T=873$，曲线的第一个点表示**初始屈服**，即等效塑性应变为零时的 Von Mises 应力

对于 `HARDENING=COMBINED` 的**各向同性**硬化曲线定义，需使用 `*CYCLIC HARDENING` 关键字

```
*PLASTIC,HARDENING=COMBINED // 总体硬化曲线（含运动 + 各向同性）
800.,0.
1600.,.1
*CYCLIC HARDENING           // 各向同性硬化曲线
800.,0.
1600.,.1
```

### USER

用户自定义硬化曲线应在用户子程序 `uhardening.f` 中进行定义

### JOHNSON COOK

对于 Johnson-Cook（JC）硬化，材料必须是各向同性的，且需使用 `*RATE DEPENDENT` 来定义硬化曲线的应变率依赖性。JC 硬化包含六个输入常数

- $A$
- $B$
- $n(>0)$
- $m(>0)$
- $T_{m}$：熔化温度
- $T_{0}$：转变温度

```
*PLASTIC,HARDENING=JOHNSON COOK
1, 1, 1, 1, 1， 1

*RATE DEPENDENT, TYPE=JOHNSON COOK
应变率敏感性系数, 参考应变率(>0)
```


温度依赖性已经包含在模型方程中，可以通过将**转变温度**设置为**熔化温度**以使温度依赖性失效