# 反对称矩阵

<span class="gray-text">
反对称矩阵是描述刚体旋转的核心数学工具
</span>


反对称矩阵定义为

$$
A^{T} = -A,
$$

对于三维空间中的任意反对称矩阵 $A$，均可表示为

$$
A=\begin{bmatrix}
0 & -a_{3} & a_{2} \\
a_{3} & 0 &  -a_{1} \\
-a_{2} & a_{1} & 0
\end{bmatrix} ,
$$

其中，$\mathbf{a} = [a_1,\, a_2,\, a_3]^{\mathrm{T}} \in \mathbb{R}^3$ 是唯一确定该矩阵的三维向量，故将 $A$ 记为

$$
A = \left[\mathbf{a}\right]_{\times}.
$$

三维反对称矩阵 $A$ 的特征值满足

$$
\det(A - \lambda I) = -\lambda \left(\lambda^2 + a_1^2 + a_2^2 + a_3^2\right),
$$

故特征值为

$$
\lambda_1 = 0, \quad \lambda_2 = +i\sqrt{a_1^2 + a_2^2 + a_3^2}, \quad \lambda_3 = -i\sqrt{a_1^2 + a_2^2 + a_3^2}.
$$

因此，$A$ 的秩为 $2$ 或 $0$

## 几何意义

对于任意的向量 $\mathbf{r}\in\mathbb{R}^{3}$，有

$$
A\mathbf{r} = \left[\mathbf{a}\right]_{\times} \mathbf{r}= \mathbf{a}\times\mathbf{r},
$$

这表明，三维反对称矩阵 $A$ 对向量 $\mathbf{r}$ 的线性变换，等价于向量 $\mathbf{a}$ 与 $\mathbf{r}$ 的叉乘运算


### 刚体旋转

根据 [Rodrigues 公式](../chap1/sec1-OT.md)，旋转轴为单位向量 $\mathbf{u}=[u_{x},u_{y},u_{z}]$，旋转角为 $\theta$ 的旋转变换矩阵为

$$
\begin{equation}
\begin{aligned}
R(\mathbf{u}, \theta) &= \cos \theta \cdot I  + \sin \theta \cdot [\mathbf{u}]_{\times} + (1 - \cos \theta) \cdot \mathbf{uu}^T\\
&=I  + \sin \theta \cdot [\mathbf{u}]_{\times} + (1 - \cos \theta) \cdot(\mathbf{uu}^T - I)
\end{aligned}
\end{equation}
$$

$\mathbf{u}$ 是单位向量，故满足

$$
\mathbf{uu}^T - I  = [\mathbf{u}]_{\times}^{2},
$$

因此，Rodrigues 公式可以写为

$$
R(\mathbf{u}, \theta) =I  + \sin \theta \cdot [\mathbf{u}]_{\times} + (1-\cos\theta)[\mathbf{u}]_{\times}^{2}.
$$

#### 指数形式

对于一般三维反对称矩阵 $A = \left[\mathbf{a}\right]_{\times}$，其中 $\mathbf{a} = \|\mathbf{a}\|\mathbf{u}=\theta\mathbf{u}$，于是

$$
A = \left[\mathbf{a}\right]_{\times} = \theta\left[\mathbf{u}\right]_{\times},
$$

根据李代数理论，绕轴 $\mathbf{u}$ 旋转 $\theta$ 度的矩阵可以表示为

```{margin}
根据旋转矩阵的正交性，可看出 $A$ 必须是反对称矩阵 
```

$$
R(A) = R(\mathbf{u},\theta) = e^{\theta\left[\mathbf{u}\right]_{\times}}=I+\frac{\theta\left[\mathbf{u}\right]_{\times}}{1!}+\frac{\theta^2\left[\mathbf{u}\right]_{\times}^2}{2!}+\frac{\theta^3\left[\mathbf{u}\right]_{\times}^3}{3!}+\cdots,
$$ (sec2-eq:Rodrigues)

通过计算容易证明

$$
[\mathbf{u}]_{\times}^{3} = -[\mathbf{u}]_{\times},\quad [\mathbf{u}]_{\times}^{4} = -[\mathbf{u}]^{2}_{\times},\quad [\mathbf{u}]_{\times}^{5} = [\mathbf{u}]_{\times},
$$

再结合 $\sin\theta$ 和 $\cos\theta$ 的泰勒展开式，能够推得 Rodrigues 公式

$$
R(\mathbf{u}, \theta) =I  + \sin \theta \cdot [\mathbf{u}]_{\times} + (1-\cos\theta)[\mathbf{u}]_{\times}^{2}.
$$

由此可见，旋转矩阵可以完全由 $A = \left[\mathbf{a}\right]_{\times}$ 确定，因此矩阵 $A$ 也被称为旋转矩阵的生成元

### 无穷小旋转

当 $\theta\rightarrow0$，此时

$$
\sin\theta\rightarrow\theta,\quad 1-\cos\theta\rightarrow\frac{1}{2}\theta^2,
$$

代入并舍弃高阶项，得到

$$
R(\mathbf{u}, \theta)\approx I  + \theta [\mathbf{u}]_{\times} = I + [\mathbf{a}]_{\times},
$$

上式可以作为旋转角度极小时的旋转矩阵的近似

若将 $\theta$ 视为 $\delta t$ 时间内均匀旋转的角度，则角速度 $\omega = \theta / \delta t$，于是

$$
R(\mathbf{u}, \theta)\approx I  + \omega [\mathbf{u}]_{\times}\delta t = I  + [\boldsymbol{\omega}]_{\times}\delta t.
$$
