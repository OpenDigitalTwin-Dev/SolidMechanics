# Jaumann 应力率

<span class="gray-text">
Jaumann 应力率的核心思想是：在随材料局部旋转的共旋坐标系中描述应力的变化，从而消除刚体旋转对应力率的影响
</span>

Jaumann 应力率通过引入修正项，有效剔除了由刚体旋转引起的虚假应力变化

$$
\overset{\circ}{\boldsymbol{\sigma}} = \dot{\boldsymbol{\sigma}} + \boldsymbol{\sigma} W - W \boldsymbol{\sigma},
$$

其中，$W$ 是旋转率张量，是速度梯度 $L=\nabla\mathbf{v}$ 的反对称部分

$$
W = \frac{1}{2}(L - L^{T}).
$$