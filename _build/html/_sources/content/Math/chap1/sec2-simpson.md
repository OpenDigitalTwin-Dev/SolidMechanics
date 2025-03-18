# 辛普森公式

假设积分区间 $[a,b]$ 被均匀地划分为**偶数**段 $n$，每段的长度为 $h=\frac{b-a}{n}$，划分节点依次为 $x_{0}, x_{1}, \cdots, x_{n}$，于是 $x_{i} = a + i\cdot h,\, i=0,2,\cdots,n$

辛普森公式在每个小区间 $[x_{i-1}, x_{i+1}]$ 上采用二次多项式对 $f(x)$ 插值，通过插值多项式的面积来近似积分值。使用拉格朗日插值多项式

$$
P(x) = f(x_{i-1})L_{i-1}(x) + f(x_{i})L_{i}(x) + f(x_{i+1})L_{i+1}(x)
$$

构造插值多项式，其中 $L_{i-1}(x), L_{i}(x), L_{i+1}(x)$ 是节点 $x_{i-1}, x_{i}, x_{i+1}$ 处的基函数

$$
\begin{equation}
\begin{aligned}
L_{i-1}(x)&=\frac{(x - x_{i})(x - x_{i+1})}{(x_{i-1} - x_{i})(x_{i-1} - x_{i+1})},\\
L_{i}(x)&=\frac{(x - x_{i-1})(x - x_{i+1})}{(x_{i} - x_{i-1})(x_{i} - x_{i+1})},\\
L_{i+1}(x)&=\frac{(x - x_{i-1})(x - x_{i})}{(x_{i+1} - x_{i-1})(x_{i+1} - x_{i})}.
\end{aligned}
\end{equation}
$$

于是，在区间 $[x_{i-1}, x_{i+1}]$ 上的积分为

$$
\int_{x_{i-1}}^{x_{i+1}}P(x)\,\mathrm{d}x = \frac{h}{3}\left[f(x_{i-1}) + 4f(x_{i})+f(x_{i+1})\right].
$$

插值多项式 $P(x)$ 的误差公式为

$$
\begin{equation}
e(x) = \frac{f'''(\xi)}{3!}(x-x_{i-1})(x-x_{i})(x-x_{i+1}),\quad \xi\in(x_{i-1},x_{i+1}).
\end{equation}
$$

```{admonition} 证明
:class: tip, dropdown

定义辅助函数

$$
g(t) = f(t) - P(t) - K\cdot (t-x_{i-1})(t - x_{i})(t-x_{i+1}).
$$

对于任意一点 $x\in[x_{i-1},x_{i+1}]$，令 $g(x) = 0$，其中 $x\neq x_{i-1},x_{i},x_{i+1}$，于是 $g(t)$ 至少有 4 个零点（ $x,x_{i-1},x_{i},x_{i+1}$ ）。反复运用罗尔定理，必然存在 $\xi\in[x_{i-1},x_{i+1}]$，使得

$$
g'''(\xi)=0,
$$

于是

$$
f'''(\xi) - P'''(\xi) - 6K = 0,
$$

因为 $P'''(t)\equiv0$，于是整理得到

$$
K = \frac{f'''(\xi)}{3!}.
$$

代入误差公式

$$
\begin{equation}
e(x) = f(x) - P(x) = \frac{f'''(\xi)}{3!}(t-x_{i-1})(t - x_{i})(t-x_{i+1}),\quad \xi\in[x_{i-1},x_{i+1}].
\end{equation}
$$

```

积分误差

$$
E = \int_{x_{i-1}}^{x_{i+1}}f(x) - P(x)\, \mathrm{d}x.
$$

令 $p(x) = (x-x_{i-1})(x-x_{i})(x-x_{i+1})$，构造辅助函数

$$
\phi(x)=f(x) - P(x) - kp(x) - \frac{E}{\int_{x_{i-1}}^{x_{i+1}}xp(x)\,\mathrm{d}x}xp(x)\,\mathrm{d}x,
$$

于是 $\phi(x_{i-1})=\phi(x_{i})=\phi(x_{i+1})=0$.由 $\int_{x_{i-1}}^{x_{i+1}}p(x)=0$，导出 $\int_{x_{i-1}}^{x_{i+1}}\phi(x)=0$. 此外，$\int_{x_{i-1}}^{x_{i}}p(x)\neq0$，因此存在 $k$ 使得 $\int_{x_{i-1}}^{x_{i}}\phi(x)=0$，由

$$
0=\int_{x_{i-1}}^{x_{i+1}}\phi(x)\,\mathrm{d}x=\int_{x_{i-1}}^{x_{i}}\phi(x)\,\mathrm{d}x + \int_{x_{i}}^{x_{i+1}}\phi(x)\,\mathrm{d}x
$$

得到 $\int_{x_{1}}^{x_{i+1}}\phi(x)=0$，这表面 $\phi(x)$ 在区间 $(x_{i-1}, x_{i})$ 和 $(x_{i},x_{i+1})$ 中分别至少存在一个零点，因此 $\phi(x)$ 在区间 $[x_{i-1},x_{i+1}]$ 中至少存在五个不同的零点。由罗尔定理，存在一点 $\xi$ 使得

$$
0 = \phi^{(4)}(\xi) = f^{(4)}(\xi) - \frac{4!E}{\int_{x_{i-1}}^{x_{i+1}}xp(x)\,\mathrm{d}x},
$$

于是

$$
E = \frac{f^{(4)}(\xi)}{4!}\int_{x_{i-1}}^{x_{i+1}}xp(x)\,\mathrm{d}x=-\frac{h^5}{90}f^{(4)}(\xi).
$$

在区间 $[a,b]$ 上有

$$
\int_{a}^{b}f(x)\,\mathrm{d}x \approx \frac{h}{3}(f(x_{0})+4\sum_{i=0}^{\frac{n}{2}-1}f(x_{2i+1})+2\sum_{i=1}^{\frac{n}{2}-1}f(x_{2i})+f(x_{n})),
$$

总误差为

$$
E_{\text{总}} = \sum_{i=1,3,...}^{n}-\frac{h^5}{90}f^{(4)}(\xi)=-\frac{(b-a)h^{4}}{180}f^{(4)}(\eta).
$$