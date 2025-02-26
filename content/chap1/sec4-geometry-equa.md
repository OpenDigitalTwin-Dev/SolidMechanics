# 几何方程

考虑弹性体内任一点 $P$，沿 $x$ 轴和 $y$ 轴的正方向取两个微小线段$\overline{PA} = \mathrm{d}x $ 和 $\overline{PA} = \mathrm{d}y$，假定弹性体受力后 $P,A,B$ 三点分别移动到了 $P^`,A^`,B^`$

```{figure} ../../images/chap1/displ_strain.png
---
width: 800px
name: sec4-fig:displ-strain
---
位移和应变关系示意图
```

```{margin}
建立方程时，采用了**小变形**假设，因此以弹性体变形前的尺寸作为微分体的几何尺寸，从而简化了力学分析
```

于是，$\overline{PA}$ 的线应变为

$$
\epsilon_x = \frac{\left( u + \frac{\partial u}{\partial x} \, \mathrm{d}x \right) - u}{\mathrm{d}x} = \frac{\partial u}{\partial x},
$$

类似地，$\overline{PB}$ 的线应变为

$$
\epsilon_y = \frac{\partial v}{\partial y}.
$$

对于 $\overline{PA}$ 的转角 $\alpha$ 有

$$
\alpha = \frac{\left( v + \frac{\partial v}{\partial x} \, \mathrm{d}x \right) - v}{\mathrm{d}x} = \frac{\partial v}{\partial x},
$$

类似地，$\overline{PB}$ 的转角

$$
\beta = \frac{\partial u}{\partial y},
$$

于是切应变 $\gamma_{xy}$ 为

$$
\gamma_{xy} = \alpha + \beta = \frac{\partial v}{\partial x} + \frac{\partial u}{\partial y}.
$$

将几何方程整理如下

$$
\begin{equation}
\begin{aligned}
&\epsilon_x = \frac{\partial u}{\partial x}, \\
&\epsilon_y = \frac{\partial v}{\partial y}, \\
&\gamma_{xy} = \frac{\partial v}{\partial x} + \frac{\partial u}{\partial y}.
\end{aligned}
\end{equation}
$$ (sec4-eq:geometry)

当位移分量 $u,v$ 完全确定时，应变分量 $\epsilon_x, \epsilon_y, \gamma_{xy}$ 也完全确定。反之，应变分量完全确定时，位移分量不能完全确定。
假设

$$
\epsilon_x = \epsilon_y = \gamma_{xy} = 0,
$$

则

$$
\frac{\partial u}{\partial x} = 0, \quad
\frac{\partial v}{\partial y} = 0, \quad
\gamma_{xy} = 0,
$$

根据前两式，可得

$$
u = u_{0} - wy,\quad
v = v_{0} - vx.
$$

$u_{0}$ 和 $v_{0}$ 分别表示物体沿 $x$ 轴和 $y$ 轴方向的**刚体平移**，而 $w$ 则为物体绕 $z$ 轴的**刚体转动**。当只有 $w$ 不为 0 时，对于坐标内任一点 $P$，其位移分量为 $u=-wy, v = wx$，满足

$$
\begin{bmatrix}
u & v
\end{bmatrix}
\begin{bmatrix}
x \\ y
\end{bmatrix} = 0,
$$

因此，点 $P$ 的位移方向为以原点 $O$ 为圆心，$\overline{OP}$ 为半径的圆在 $P$ 点的切向。由于位移是微小的（$w$非常小），因此运动表现为刚体转动，位移为

$$
\sqrt{u^2+v^2}=w\sqrt{x^2+y^2}.
$$
