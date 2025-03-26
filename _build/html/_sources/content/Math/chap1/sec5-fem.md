# 有限元计算

在有限元方法中，偏微分方程通过变分法与分片多项式进行离散，最终被转化为线性方程组的形式。例如，对于[线弹性问题](../../Elasticity/chap1/sec9-numerical-simple.md)，其形式为

$$
\left(\phi_{j}\sum_{i=0}^{n}c_{i}\left.\frac{\partial \phi_{i}}{\partial x}\, \right)\right|^{x=L}_{x=0} + \sum_{i=0}^{n}c_{i}\int_{0}^{L}\frac{\partial \phi_{i}}{\partial x}\frac{\partial \phi_{j}}{\partial x}\,\mathrm{d}x = \int_{0}^{L}f\,\phi_{j}\,\mathrm{d}x,\quad j=0:n.
$$

计算刚度矩阵与右端项的关键在于高效计算

$$
\int_{0}^{L}\frac{\partial \phi_{i}}{\partial x}\frac{\partial \phi_{j}}{\partial x}\,\mathrm{d}x,\, \int_{0}^{L}f\phi_{j}\,\mathrm{d}x,\, \phi_{j}\frac{\partial \phi_{i}}{\partial x}
$$

这些计算最终体现为形函数及其导数的相关数值计算

$$
\int_{T}\frac{\partial N_{1}}{\partial x}\frac{\partial N_{2}}{\partial x}\,\mathrm{d}x,\, \int_{T}fN_{1}\,\mathrm{d}x,\, N_{1}\frac{\partial N_{2}}{\partial x}
$$

## 形函数

在有限元方法中，为了简化计算，通常将复杂的**物理单元**（实际几何形状上的单元）映射到一个标准的**参考单元**上进行处理。参考单元是一个简单的几何形状，例如二维问题中的标准三角形或标准矩形，三维问题中的标准四面体或立方体。通过这种映射，可以在参考单元上定义形函数和积分规则，从而统一处理不同形状的单元

```{figure} ../../../images/Math/chap1/std-element.png
---
width: 400px
name: sec5-fig:element-switch
---
从标准单元映射到一般单元
```

**形函数**是定义在参考单元上的**多项式插值函数**，其主要作用包括

- 实现参考单元到物理单元的映射
- 对单元内部的场变量进行插值，例如，对位移场插值 $u(x,y)=\sum u_{i}N_{i}(x,y)$

形函数需要满足特定的数学性质，以确保插值的正确性和数值计算的稳定性

- 插值性：$N_{i}(\xi_{j}, \eta_{j}) = \delta_{ij}$
- 单位分解性：$\sum_{i=1}^{n}N_{i}(\xi, \eta) \equiv 1$
- 连续性：在相邻单元边界上满足 $C^{0}$ 连续


### 三角形单元

#### 三节点 Lagrange 元

考虑二维空间中具有如下形式的函数：

$$
\phi = c_{1} + c_{2}\xi + c_{3}\eta,
$$

因此需要 3 个形函数（基函数）

```{figure} ../../../images/Math/chap1/triangle-element-linear.png
---
width: 600px
name: sec5-fig:triangle-element-linear
---
三角形单元上的线性形函数
```


#### 六节点 Lagrange 元

考虑二维空间中具有如下形式的函数：

$$
\phi = c_{1} + c_{2}\xi + c_{3}\eta + c_{4}\xi\eta + c_{5}\xi^2 + c_{6}\eta^2,
$$

因此需要 6 个形函数（基函数）

```{figure} ../../../images/Math/chap1/triangle-element-quadratic.png
---
width: 600px
name: sec5-fig:triangle-element-quadratic
---
三角形单元上的二次形函数
```

### 四边形单元

#### 四节点 Lagrange 元


考虑二维空间中具有如下形式的函数：

$$
\phi(\xi, \eta) = c_1 + c_2 \xi + c_3 \eta + c_4 \xi \eta,

$$

因此需要 4 个形函数（基函数）

```{figure} ../../../images/Math/chap1/rectangular-element-bilinear.png
---
width: 600px
name: sec5-fig:rectangular-element-bilinear
---
四边形单元上的双线性形函数
```

#### 九节点 Lagrange 单元

考虑二维空间中具有如下形式的函数：

$$
\phi = c_1 + c_2 \xi + c_3 \eta + c_4 \xi \eta + c_5 \xi^2 + c_6 \eta^2 + c_7 \xi^2 \eta + c_8 \xi \eta^2 + c_9\xi^2\eta^2,
$$

因此需要 9 个形函数（基函数）

```{figure} ../../../images/Math/chap1/rectangular-element-9-node.png
---
width: 800px
name: sec5-fig:rectangular-element-9-node
---
四边形单元上的 9 节点二次形函数
```

#### 八节点 Serendipity 单元

考虑二维空间中具有如下形式的函数：

$$
\phi = c_1 + c_2 \xi + c_3 \eta + c_4 \xi \eta + c_5 \xi^2 + c_6 \eta^2 + c_7 \xi^2 \eta + c_8 \xi \eta^2,
$$

因此需要 8 个形函数（基函数）

```{figure} ../../../images/Math/chap1/rectangular-element-8-node.png
---
width: 800px
name: sec5-fig:rectangular-element-8-node
---
四边形单元上的 8 节点二次形函数
```


### 面积坐标

在有限元方法中，对于三角形或四面体等单纯形单元，除了常用的自然坐标系之外，还可以采用面积坐标系（或称体积坐标系）来构造形函数。这种方法基于单纯形单元的几何特性，具有显著的几何优势。其核心思想是通过空间点与单纯形顶点相关联的子单纯形（如边、面或体）的归一化面积或体积比例来定义形函数的分量


```{figure} ../../../images/Math/chap1/area-coordinate.png
---
width: 400px
name: sec5-fig:element-switch
---
面积坐标系
```

面积坐标为

$$
\begin{equation}
\begin{aligned}
L_{1}&=\frac{S_{\Delta{PP_{2}P_{3}}}}{S_{\Delta{P_{1}P_{2}P_{3}}}},\\
L_{2}&=\frac{S_{\Delta{PP_{3}P_{1}}}}{S_{\Delta{P_{1}P_{2}P_{3}}}},\\
L_{3}&=\frac{S_{\Delta{PP_{1}P_{2}}}}{S_{\Delta{P_{1}P_{2}P_{3}}}}.
\end{aligned}
\end{equation}
$$

在使用面积坐标（或体积坐标）构造形函数时，形函数的定义独立于三角形或四面体的具体几何形状，因此能够避免显式的参考单元到物理单元的映射

#### 线性单元

线性单元的形函数与面积坐标直接对应

```{figure} ../../../images/Math/chap1/area-triangle-element-linear.png
---
width: 600px
name: sec5-fig:area-triangle-element-linear
---
面积坐标下三角形单元上的二次形函数
```

#### 二次单元

线性单元的形函数与面积坐标直接对应

```{figure} ../../../images/Math/chap1/area-triangle-element-quadratic.png
---
width: 600px
name: sec5-fig:area-triangle-element-quadratic
---
面积坐标下三角形单元上的二次形函数
```

```{note}
:class: tip

在参考三角形中，面积坐标与自然坐标的形函数具有等价性。具体而言，
在参考三角形中，有 $\xi=L_{2}$，$\eta=L_{3}$，而 $1-\xi-\eta = 1 - L_{2} - L_{3} = L_{1}$
```

## 坐标变换