# 有限元计算

在有限元方法中，偏微分方程通过变分法与分片多项式进行离散，最终被转化为线性方程组的形式。例如，对于[线弹性问题](../../Elasticity/chap1/sec9-numerical-simple.md)，其形式为

$$
\left(\phi_{j}\sum_{i=0}^{n}c_{i}\left.\frac{\partial \phi_{i}}{\partial x}\, \right)\right|^{x=L}_{x=0} + \sum_{i=0}^{n}c_{i}\int_{0}^{L}\frac{\partial \phi_{i}}{\partial x}\frac{\partial \phi_{j}}{\partial x}\,\mathrm{d}x = \int_{0}^{L}f\,\phi_{j}\,\mathrm{d}x,\quad j=0:n.
$$

计算刚度矩阵与右端项的关键在于高效计算

$$
\int_{0}^{L}\frac{\partial \phi_{i}}{\partial x}\frac{\partial \phi_{j}}{\partial x}\,\mathrm{d}x,\, \int_{0}^{L}f\phi_{j}\,\mathrm{d}x,\, \phi_{j}\frac{\partial \phi_{i}}{\partial x}
$$

这些计算最终体现为单元上的形函数及其导数的数值计算

$$
\int_{T}\frac{\partial N_{1}}{\partial x}\frac{\partial N_{2}}{\partial x}\,\mathrm{d}x,\, \int_{T}fN_{1}\,\mathrm{d}x,\, N_{1}\frac{\partial N_{2}}{\partial x}
$$

## 单元坐标映射

在有限元方法中，为了简化计算，通常将复杂的物理单元（实际几何形状上的单元）映射到一个标准的参考单元上进行处理。参考单元是一个简单的几何形状，例如二维问题中的标准三角形或标准矩形，三维问题中的标准四面体或立方体。通过这种映射，可以在参考单元上定义形函数和积分规则，从而统一处理不同形状的单元