# Gaussian 公式

在前文提到的矩形公式、梯形公式和辛普森公式中，积分节点均匀分布在被积区间内，通过优化权重来逼近积分值。而在高斯求积公式中，**积分节点被视为自由度，通过同时优化节点位置和权重**，实现更高的逼近精度

高斯积分公式的核心思想是利用**正交多项式**的根作为积分节点，并计算对应的权重，从而实现最高代数精度

## 正交多项式

<span class="gray-text">
正交多项式，在物理学、数值分析、积分计算和量子力学中有广泛的应用
</span>

### Legendre 多项式 

#### 定义方式
Legendre 多项式通常有两类定义方法，考虑区间 $[-1,1]$

- Rodrigues 公式：
通过 Rodrigues 公式定义

$$
P_n(x) = \frac{1}{2^n n!} \frac{d^n}{dx^n} \left( (x^2 - 1)^n \right)
$$

- 递推公式：
通过递推关系生成

$$
(n + 1)\,P_{n+1}(x) = (2n + 1)\,xP_n(x) - n\,P_{n-1}(x)
$$

初始函数为：$P_{0}(x) = 1,\, P_{1}(x)=x$.

Legendre 多项式的根分布在区间 $(-1,1)$ 内且互异

#### 正交性

Legendre 多项式 $P_{n}(x)$ 满足

$$
\begin{equation}
\int_{-1}^1 P_m(x) P_n(x) \, dx = \frac{2}{2n+1} \delta_{mn}.
\end{equation}
$$

#### 积分权重

权重 $w_{i}$ 需满足对任意次数 $\leq 2n-1$ 的多项式 $f(x)$，积分精确成立。利用多项式插值理论，权重可通过积分  Lagrange 基函数 $L_{i}(x)$ 得到

$$
\begin{equation}
w_{i}=\int_{-1}^{1}L_{i}(x)\, \mathrm{d}x,\quad \text{其中} \quad L_i(x) = \prod_{\substack{j=0 \\ j \neq i}}^{n-1} \frac{x - x_j}{x_i - x_j},\quad i=1,2,...,n
\end{equation}
$$

其显式公式为

$$
w_i = \frac{2}{(1 - x_i^2)[P_n'(x_i)]^2}.
$$

#### 示例

$P_{2}(x)=\frac{1}{2}(3x^2-1)$，积分节点为 $x_{1,2}=\pm\frac{1}{\sqrt{3}}$，积分权重为 $w_1 = w_2 = 1$，对应的积分公式为

$$
\int_{-1}^1 f(x) \, dx \approx f\left(-\frac{1}{\sqrt{3}}\right) + f\left(\frac{1}{\sqrt{3}}\right).
$$

### 第一类 Chebyshev 多项式

#### 定义方式

- 三角函数：

$$
\begin{equation}
T_{n}(x) = \cos(n\arccos(x)),\quad x\in[-1,1]
\end{equation}
$$

- 递推关系

$$
\begin{equation}
T_{n+1}(x)=2x\,T_{n}(x)-T_{n-1}(x),\quad n\geq1
\end{equation}
$$

初始函数为：$T_{0}(x) = 1,\, T_{1}(x)=x$.

第一类 Chebyshev 多项式的根（Chebyshev 节点）：

$$
x_{i}=\cos(\frac{2i-1}{2n}\pi),\, i=1,2,...,n
$$

#### 正交性

第一类 Chebyshev 多项式在权函数 $w(x) = \frac{1}{\sqrt{1 - x^2}}$ 下正交

$$
\int_{-1}^1 \frac{T_m(x) T_n(x)}{\sqrt{1 - x^2}} \, dx =
\begin{cases} 
0, & m \neq n, \\
\pi, & m = n = 0, \\
\frac{\pi}{2}, & m = n \neq 0.
\end{cases}
$$


#### 积分权重


$$
w_{i} = \frac{\pi}{n}
$$


#### 示例

$T_{2}(x) = 2x^2-1$，积分节点为 $x_{1,2} = \pm\frac{\sqrt{2}}{2}$，积分权重为 $w_{1}=w_{2}=\frac{\pi}{2}$，于是积分公式为

$$
\int_{-1}^{1} \frac{f(x)}{\sqrt{1 - x^2}} \, dx \approx \frac{\pi}{2} \left( f\left(\frac{\sqrt{2}}{2}\right) + f\left(-\frac{\sqrt{2}}{2}\right) \right),
$$

将 $\sqrt{1-x^2}$ 移至右侧，得到

$$
\int_{-1}^{1} f(x) \, dx \approx \frac{\sqrt{2}\pi}{4} \left( f\left(\frac{\sqrt{2}}{2}\right) + f\left(-\frac{\sqrt{2}}{2}\right) \right).
$$

### 第二类 Chebyshev 多项式

#### 定义方式

- 三角函数：

$$
\begin{equation}
U_{n}(x) = \frac{\sin((n+1)\arccos(x))}{\sqrt{1-x^2}},\quad x\in[-1,1]
\end{equation}
$$

- 递推关系

$$
\begin{equation}
U_{n+1}(x)=2x\,U_{n}(x)-U_{n-1}(x),\quad n\geq1
\end{equation}
$$

初始函数为：$U_{0}(x) = 1,\, U_{1}(x)=2x$.

第二类 Chebyshev 多项式的根（Chebyshev 节点）：

$$
x_{i}=\cos(\frac{i}{n+1}\pi),\, i=1,2,...,n
$$

#### 正交性

第二类 Chebyshev 多项式在权函数 $w(x) = \sqrt{1-x^2}$ 下正交

$$
\int_{-1}^1 U_m(x) U_n(x)\sqrt{1 - x^2} \, dx =
\begin{cases} 
0, & m \neq n, \\
\frac{\pi}{2}, & m = n = 0.
\end{cases}
$$


#### 积分权重

$$
w_{i} = \frac{\pi}{n+1}\sin^2(\frac{i}{n+1}\pi)
$$


#### 示例

$U_{2}(x) = 4x^2 - 1$，积分节点为 $x_{1,2}=\pm\frac{1}{2}$，积分权重为 $w_{1,2}=\frac{\pi}{4}$，于是

$$
\int_{-1}^{1} f(x)\sqrt{1 - x^2} \, dx \approx \frac{\pi}{4} \left( f\left(\frac{1}{2}\right) + f\left(-\frac{1}{2}\right) \right),
$$

将 $\sqrt{1-x^2}$ 移至右侧，得到

$$
\int_{-1}^{1} f(x) \, dx \approx \frac{\sqrt{3}\pi}{6} \left( f\left(\frac{1}{2}\right) + f\left(-\frac{1}{2}\right) \right).
$$

## 代数精度

### 精确成立（ $\leq 2n-1$ ）

设 $f(x)$ 是次数 $\leq 2n-1$ 的多项式，根据多项式除法余数定理，将 $f(x)$ 分解为

$$
f(x) = Q(x)\cdot P_{n}(x)+R(x),
$$

其中 $P_{n}(x)$ 是 $n$ 次正交多项式，$Q(x)$ 和 $R(x)$ 是次数 $\leq n-1$ 的多项式

于是

$$
\int_{a}^{b}w(x)f(x)\, \mathrm{d}x=\int_{a}^{b}w(x)Q(x)P_n(x)\, \mathrm{d}x + \int_{a}^{b}w(x)R(x)\, \mathrm{d}x.
$$

由于 $P_{n}(x)$ 与所有次数 $<n$ 的多项式正交（正交性定义），因此

$$
\int_{a}^{b}w(x)Q(x)P_n(x)\, \mathrm{d}x = 0,
$$

于是积分简化为

$$
\int_{a}^{b}w(x)f(x)\, \mathrm{d}x=\int_{a}^{b}w(x)R(x)\, \mathrm{d}x.
$$

另一方面，根据高斯积分公式

$$
\sum_{i=1}^{n}w_{i}f(x_{i})=\sum_{i}^{n}w_{i}[Q(x_{i})P_{n}(x_{i})+R(x_{i})],
$$

由于节点 $\left\{x_{i}\right\}$ 是 $P_{n}(x)$ 的根，即 $P_{n}(x_{i})=0$，因此

$$
\sum_{i}^{n}w_{i}Q(x_{i})P_{n}(x_{i}) = 0,
$$

故求和式简化为

$$
\sum_{i}^{n}w_{i}R(x_{i}).
$$

接下来，只需选取 $\left\{w_{i}\right\}$ 使得

$$
\int_{a}^{b}w(x)R(x)\, \mathrm{d}x = \sum_{i}^{n}w_{i}R(x_{i})
$$

```{margin}
范德蒙矩阵
```

精确成立即可，其中 $R(x)$ 是次数 $\leq n-1$ 的多项式，这只需使得上式对于 $R(x)=1,x,\cdots,x^{n-1}$ 精确成立即可，这将得到一个线性方程组，显然该方程组存在解

因此

$$
\int_{a}^{b}w(x)f(x)\, \mathrm{d}x=\sum_{i=1}^{n}w_{i}f(x_{i})
$$

对于次数 $\leq 2n-1$ 的多项式精确成立


### 非精确成立（ $= 2n$ ）

取 $f(x) = P_{n}^2(x)$ ，其中 $P_{n}(x)$ 是 $n$ 次正交多项式，于是

$$
\int_{a}^{b}w(x)P_{n}^2(x)\,\mathrm{d}x > 0,
$$

而 

$$
\sum_{i=1}^{n}w_{i}f(x_{i}) = \sum_{i=1}^{n}w_{i}P_{n}^2(x_{i}) = 0,
$$

因此积分公式对于 $f(x) = P_{n}^2(x)$ 不精确成立

综上，高斯积分公式代数精度是 $2n-1$