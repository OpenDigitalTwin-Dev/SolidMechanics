# 梯形公式

假设积分区间 $[a,b]$ 被均匀地划分为 $n$ 段，每段的长度为 $h=\frac{b-a}{n}$，划分节点依次为 $x_{0}, x_{1}, \cdots, x_{n}$，于是 $x_{i} = a + i\cdot h,\, i=0,2,\cdots,n$

## 矩形公式

矩形公式利用 **0** 次多项式对 $f(x)$ 插值，通过小区间的左端点、右端点或中点处的函数值作为矩形的高，以宽度 $h$ 的矩形面积来近似积分值

- **左端点公式**：

    $$
        \int_a^b f(x) \, \mathrm{d}x \approx h\sum_{i=0}^{n-1} f(x_{i})
    $$

- **右端点公式**：

    $$
        \int_a^b f(x) \, \mathrm{d}x \approx h\sum_{i=0}^{n-1} f(x_{i+1})
    $$

- **中点公式**：

    $$
        \int_a^b f(x) \, \mathrm{d}x \approx h\sum_{i=0}^{n-1} f(x_{i} + \frac{h}{2})
    $$

左、右端点公式的误差为 $O(h)$，中点公式的误差为 $O(h^{2})$

```{admonition} 证明
:class: tip, dropdown

考虑单个区间 $[x_{i}, x_{i} + h]$ 上的积分误差，对于左端点法

$$
    E_{\text{左}} = I - I_{\text{左}} = \int_{x_{i}}^{x_{i}+h}f(x)\, \mathrm{d}x - hf(x_{i}),
$$

将 $f(x)$ 在 $x_{i}$ 处泰勒展开

$$
    f(x) = f(x_i) + f'(x_i)(x - x_i) + \frac{f''(x_i)}{2}(x - x_i)^2 + O(h^3)
$$

于是

$$
    I = \int_{x_{i}}^{x_{i}+h}f(x_i) + f'(x_i)(x - x_i) + \frac{f''(x_i)}{2}(x - x_i)^2 + O(h^3)\, \mathrm{d}x,
$$

逐项积分

$$
    I = h f(x_i) + \frac{f'(x_i)}{2} h^2 + \frac{f''(x_i)}{6} h^3 + O(h^4),
$$

于是

$$
    E_{\text{左}} = \frac{f'(x_i)}{2} h^2 + \frac{f''(x_i)}{6} h^3 + O(h^4),
$$

因此在区间 $[x_{i}, x_{i} + h]$ 上，主误差项是 $O(h^2)$，因此总误差为

$$
    \text{总误差}\approx n\cdot O(h^2) = \frac{b-a}{h}\cdot O(h^2) = O(h).
$$

右端点法的证明类似

对于中点法，将 $f(x)$ 在 $x_{i+\frac{1}{2}} = x_{i} + \frac{h}{2}$ 处泰勒展开

$$
f(x) = f(x_{i+\frac{1}{2}}) + f'(x_{i+\frac{1}{2}}) (x - x_{i+\frac{1}{2}}) + \frac{f''(x_{i+\frac{1}{2}})}{2} (x - x_{i+\frac{1}{2}})^2 + O(h^3),
$$

代入积分公式

$$
    I=\int_{x_{i}}^{x_{i}+h} f(x_{i+\frac{1}{2}}) + \textcolor{red}{f'(x_{i+\frac{1}{2}}) (x - x_{i+\frac{1}{2}})} + \frac{f''(x_{i+\frac{1}{2}})}{2} (x - x_{i+\frac{1}{2}})^2 + O(h^3) \,\mathrm{d}x,
$$

逐项积分，其中**红色项积分为 0**，因此

$$
    I=hf(x_{i+\frac{1}{2}}) + \frac{f''(x_{i+\frac{1}{2}})}{24}h^3 +O(h^4).
$$

于是在区间 $[x_{i}, x_{i} + h]$ 上，主误差项是 $O(h^3)$，因此总误差为 $O(h^2)$

在每个小区间上，中点公式虽然也只采用 0 阶多项式逼近函数 $f(x)$ （精度为 $O(h)$），但由于误差项中 

$$f'(x_{i+\frac{1}{2}}) (x - x_{i+\frac{1}{2}})$$ 

在区间 $[x_{i}, x_{i} + h]$ 上关于 $x_{i+\frac{1}{2}}$ 中心对称，因此积分为零,使得积分逼近精度提高了一阶（精度为 $O(h^2)$）

```


## 梯形公式

梯形公式利用 **1** 次多项式对 $f(x)$ 插值，通过小区间的左端点和右端点的函数值，构成梯形的面积，对积分进行近似计算

$$
    \int_a^b f(x) \, \mathrm{d}x \approx \frac{h}{2}\sum_{i=0}^{n-1} [f(x_{i}) + f(x_{i+1})]
$$

其误差为 $O(h^2)$


```{admonition} 证明
:class: tip, dropdown

虑单个区间 $[x_{i}, x_{i} + h]$ 上的积分误差，将 $f(x_i)$ 和 $f(x_{i+1})$ 在 $x_{i+\frac{1}{2}} = x_{i} + \frac{h}{2}$ 处泰勒展开

$$
\begin{equation}
\begin{aligned}
f(x_i) &= f(x_{i+\frac{1}{2}}) - f'(x_{i+\frac{1}{2}}) \frac{h}{2} + \frac{f''(x_{i+\frac{1}{2}})}{2} \left(\frac{h}{2}\right)^2 - \frac{f'''(\xi_1)}{6} \left(\frac{h}{2}\right)^3, \\
f(x_{i+1}) &= f(x_{i+\frac{1}{2}}) + f'(x_{i+\frac{1}{2}}) \frac{h}{2} + \frac{f''(x_{i+\frac{1}{2}})}{2} \left(\frac{h}{2}\right)^2 + \frac{f'''(\xi_2)}{6} \left(\frac{h}{2}\right)^3.
\end{aligned}
\end{equation}
$$

于是

$$
f(x_{i})+f(x_{i+1})=2f(x_{i+\frac{1}{2}})+\frac{f''(x_{i+\frac{1}{2}})}{4}h^2 + O(h^3),
$$

将 $f(x)$ 在 $x_{i+\frac{1}{2}}$ 处展开并代入积分

$$
    I=hf(x_{i+\frac{1}{2}}) + \frac{f''(x_{i+\frac{1}{2}})}{24}h^3 +O(h^4).
$$

于是区间 $[x_{i}, x_{i}+h]$ 上的局部误差是

$$
I - \frac{h}{2}[f(x_{i})+f(x_{i+1})] = -\frac{f''(x_{i+\frac{1}{2}})}{12}h^3 + O(h^4),
$$

于是总误差

$$
\begin{equation}
\begin{aligned}
E_{\text{总}}&=-\frac{h^3}{12}\sum_{i=0}^{n}f''(x_{i+\frac{1}{2}}) + n \cdot O(h^4)\\
&=-\frac{(b-a)}{12}h^2f''(\xi).
\end{aligned}
\end{equation}
$$


```
