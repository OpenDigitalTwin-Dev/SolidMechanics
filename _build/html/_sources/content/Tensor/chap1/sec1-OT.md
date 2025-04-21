# 正交变换

<span class="gray-text">
在固体力学中，正交变换是分析材料对称性、坐标系变换以及张量客观性的重要工具。正交变换通常由正交矩阵表示，用于描述坐标系的旋转，在应力、应变和本构关系的分析中尤为重要
</span>

## 基本定义

```{margin}
此处仅考虑实空间
```

正交变换是指在实内积空间（如欧几里得空间）中，保持向量内积不变的**线性变换**。若线性变换 $\mathcal{Q}:V\rightarrow V$ 满足：

$$
(\mathcal{Q}\mathbf{u},\mathcal{Q}\mathbf{v}) = (\mathbf{u},\mathbf{v})
$$

则称 $\mathcal{Q}$ 为正交变换


```{admonition} 等价定义一
:class: tip, dropdown

保持向量长度：$\|\mathcal{Q}\mathbf{v}\|=\|\mathbf{v}\|$ 对所有 $\mathbf{v}\in V $ 成立

$0\Rightarrow1$：

$$
(\mathcal{Q}\mathbf{u},\mathcal{Q}\mathbf{v}) = (\mathbf{u},\mathbf{v}) \Rightarrow (\mathcal{Q}\mathbf{v},\mathcal{Q}\mathbf{v}) = (\mathbf{v},\mathbf{v}) \Rightarrow \|\mathcal{Q}\mathbf{v}\|=\|\mathbf{v}\|
$$

$1\Rightarrow0$：

$$
(\mathcal{Q}(\mathbf{u}-\mathbf{v}),\mathcal{Q}(\mathbf{u}-\mathbf{v})) = ((\mathbf{u}-\mathbf{v}),(\mathbf{u}-\mathbf{v})) \Rightarrow (\mathcal{Q}\mathbf{u},\mathcal{Q}\mathbf{v}) = (\mathbf{u},\mathbf{v}) 
$$

```

```{admonition} 等价定义二
:class: tip, dropdown

在标准正交基下，对应的矩阵是正交矩阵 $Q$，满足 $Q^{T}Q=I$


$0\Rightarrow2$：

$$
\begin{equation}
\begin{aligned}
(\mathcal{Q}\mathbf{u},\mathcal{Q}\mathbf{v}) = (\mathbf{u},\mathbf{v}) &\Rightarrow (\mathcal{Q}\mathbf{e}_{i},\mathcal{Q}\mathbf{e}_{j}) = (\mathbf{e}_{i},\mathbf{e}_{j}) \\ 
&\Rightarrow  \mathbf{e}_{i}^{T}Q^{T}Q\mathbf{e}_{j}=\delta_{ij} \\
&\Rightarrow Q^{T}Q = I
\end{aligned}
\end{equation}
$$

$2\Rightarrow0$：

$$
Q^{T}Q = I \Rightarrow (\mathcal{Q}\mathbf{u},\mathcal{Q}\mathbf{v}) =\mathbf{u}^{T}Q^{T}Q\mathbf{v} = \mathbf{u}^{T}\mathbf{v} = (\mathbf{u},\mathbf{v})
$$

```

## 正交变换的性质

在正交变换具有以下核心性质：

```{margin}
计算实正交矩阵的特征值时应扩展到复空间，其中，$^{\dagger}$ 为共轭转置，设 $\mathbf{u}$ 和 $\lambda$ 满足 $Q\mathbf{u} = \lambda\mathbf{u}$
```

- 保持向量的长度不变：$\|Q\mathbf{v}\|=\|\mathbf{v}\|$
- 保持向量间夹角不变：$(Q\mathbf{u},Q\mathbf{v}) = (\mathbf{u},\mathbf{v})$
- $\det(Q)=\pm1$：$\det(Q)=1$ 时为旋转变换；$\det(Q)=-1$ 时为反射变换
- 特征值 $|\lambda| = 1$：$\mathbf{u}^{T}\mathbf{u} = \mathbf{u}^{\dagger}Q^{\dagger}Q\mathbf{u}=|\lambda|^2\mathbf{u}^{T}\mathbf{u}$
- $Q^{-1} = Q^{T}$
- $Q$ 的行/列向量，形成一组标准正交基：$Q^{T}Q = I$
- $Q_{1}, Q_{2}$ 为正交矩阵，则 $Q_{1}Q_{2}$ 也是正交矩阵：$(Q_{1}Q_{2})^{T}Q_{1}Q_{2} = Q_{2}^{T}Q_{1}^{T}Q_{1}Q_{2} = I$ 


## 相似变换

<span class="gray-text">
相似变换是同一线性变换在不同基下的矩阵表示之间的转换关系
</span>

### 基本定义

给定线性变换 

$$
\mathcal{T}: V\rightarrow V,
$$

设其在基 $\{\mathbf{v}_{1},\mathbf{v}_{2},\cdots,\mathbf{v}_{n}\}$ 的矩阵表示为 $A$，在基 $\{\mathbf{w}_{1},\mathbf{w}_{2},\cdots,\mathbf{w}_{n}\}$ 下的矩阵表示为 $B$，且两组基之间的转换矩阵为 $P$，即

$$
\begin{bmatrix}
\mathbf{w}_{1}&\mathbf{w}_{2}&\cdots&\mathbf{w}_{n}
\end{bmatrix}=
\begin{bmatrix}
\mathbf{v}_{1}&\mathbf{v}_{2}&\cdots&\mathbf{v}_{n}
\end{bmatrix}P,
$$

于是，向量 $\mathbf{x}$ 在基 $\{\mathbf{v}_{i}\}$ 下的坐标 $\mathbf{x}^{v}=[x^{v}_{1},x^{v}_{2},\cdots,x^{v}_{n}]^{T}$ 与在基 $\{\mathbf{w}_{i}\}$ 下的坐标 $\mathbf{x}^{w}=[x^{w}_{1},x^{w}_{2},\cdots,x^{w}_{n}]^{T}$ 满足

$$
\begin{equation}
\begin{aligned}
\mathbf{x} 
&= \begin{bmatrix}
\mathbf{v}_{1}&\mathbf{v}_{2}&\cdots&\mathbf{v}_{n}
\end{bmatrix}
\begin{bmatrix}
x^{v}_{1}\\x^{v}_{2}\\\vdots\\x^{v}_{n}\end{bmatrix}
=\begin{bmatrix}
\mathbf{w}_{1}&\mathbf{w}_{2}&\cdots&\mathbf{w}_{n}
\end{bmatrix}
\begin{bmatrix}
x^{w}_{1}\\x^{w}_{2}\\\vdots\\x^{w}_{n}\end{bmatrix}\\
&= \begin{bmatrix}
\mathbf{v}_{1}&\mathbf{v}_{2}&\cdots&\mathbf{v}_{n}
\end{bmatrix}P
\begin{bmatrix}
x^{w}_{1}\\x^{w}_{2}\\\vdots\\x^{w}_{n}\end{bmatrix},
\end{aligned}
\end{equation}
$$

即

$$
\mathbf{x}^{v}=P\ \mathbf{x}^{w},
$$

因此

$$
\begin{equation}
\begin{aligned}
\mathcal{T}(\mathbf{x}) &= \begin{bmatrix}
\mathbf{v}_{1}&\mathbf{v}_{2}&\cdots&\mathbf{v}_{n}
\end{bmatrix}A\ \mathbf{x}^{v}\\
&=\begin{bmatrix}
\mathbf{w}_{1}&\mathbf{w}_{2}&\cdots&\mathbf{w}_{n}
\end{bmatrix}P^{-1}AP\ \mathbf{x}^{w},
\end{aligned}
\end{equation}
$$

又因为

$$
\mathcal{T}(\mathbf{x}) = \begin{bmatrix}
\mathbf{w}_{1}&\mathbf{w}_{2}&\cdots&\mathbf{w}_{n}
\end{bmatrix}B\ \mathbf{x}^{w},
$$

故

$$
B = P^{-1}AP,
$$

称矩阵 $A$ 和矩阵 $B$ 是相似的

### 相似变换的性质

#### 保特征值

**代数重数**：代数重数是矩阵特征多项式的根的重数

$$
\det(\lambda I - B) = \det(\lambda I - P^{-1}AP) = \det(P^{-1}(\lambda I - A)P) = \det(\lambda I - A),
$$

故特征根及其重数保持不变

**几何重数**：几何重数是特征值对应特征空间的维数，即 $\dim(\ker(\lambda I-A))$

这是自然的，因为线性变换 $\ker(\lambda I-A)$ 和 $\ker(\lambda I-B)$ 通过 可逆变换 $P$ 和 $P^{-1}$ 一一对应

#### 保迹 $\text{tr}(A)$

```{margin}

$$
\text{tr}(AB)&= \sum_{i=1}^{n}\sum_{k=1}^{n}a_{ik}b_{ki} \\
&= \sum_{k=1}^{n}\sum_{i=1}^{n}b_{ki}a_{ik}\\
&=\text{tr}(BA)
$$
```

$$
\text{tr}(B) = \text{tr}(P^{-1}AP) = \text{tr}(APP^{-1}) = \text{tr}(A).
$$

#### 保行列式 $\det(A) = \prod_{i=1}^{n} \lambda_i$

```{margin}
$$
\det(AB)&=\det(E_{1}E_{2}\cdots E_{k}B)\\
&=\det(E_{1})\det(E_{2})\cdots \det(E_{k})\det(B)\\
&=\det(E_{1}E_{2}\cdots E_{k})\det(B)\\
&=\det(A)\det(B)
$$
```

$$
\det(B) = \det(P^{-1}AP) = \det(P^{-1}) \det(A) \det(P) = \det(A),
$$

或

$$
\det(A) = \det(A - \lambda I)|_{\lambda=0}=\prod_{i=1}^{n}(\lambda_{i}-\lambda)|_{\lambda=0}=\prod_{i=1}^{n}\lambda_{i}.
$$

## 合同变换

### 基本定义

对实对称矩阵 $A$，其二次型为

$$
f(\mathbf{x}) = \mathbf{x}^{T}A\mathbf{x},
$$

设存在变量替换 $\mathbf{x} = P\mathbf{y}$（不同基下的坐标表示，见相似变换），则

$$
f(\mathbf{x}) = f(P\mathbf{y}) = \mathbf{y}^{T}P^{T}AP\mathbf{y} = \mathbf{y}^{T}B\mathbf{y},
$$

则称 $A$ 与 $B$ 为合同矩阵，这种变换称为‌**合同变换**。合同变换的重要目标是将二次型化为标准形（对角矩阵形式）

$$
f(\mathbf{y})=\lambda_{1}y_{1}^2+\lambda_{2}y_{2}^2+\cdots+\lambda_{n}y_{n}^2.
$$

### 合同变换的性质

#### 保对称性

$$
B^{T} = P^{T}A^{T}P = P^{T}AP = B.
$$

#### Sylvester 惯性定理

对于任意实二次型 $ f(x) = x^T A x $ （$ A $ 为实对称矩阵），通过合同变换可唯一化简为以下标准形：

$$
f(y) = y_1^2 + \cdots + y_p^2 - y_{p+1}^2 - \cdots - y_{p+q}^2 \quad (p+q \leq n),
$$

其中正惯性指数 $ p $、负惯性指数 $ q $、零惯性指数 $ r = n - p - q $ 唯一确定，仅依赖于原二次型矩阵 $ A $ 的性质

根据 Sylvester 惯性定理，可得到以下结论：

- 合同变换下，矩阵的正定性、半正定性保持不变‌
- 二次曲面（如椭球面、双曲面）的类型由正负惯性指数唯一确定‌
- 惯性指数与特征值的符号直接相关，合同变换不改变符号分布‌

## 正交变换

由于正交矩阵满足 $Q^{T} = Q^{-1}$，因此正交变换

$$
B = Q^{T}AQ = Q^{-1}AQ,
$$

既是相似变换，也是合同变换（一般应用于对称矩阵）

### 正交变换的几何意义

由于正交变换保持向量的长度和向量间的夹角不变，这使得正交变换可以被视为刚体运动中的**旋转**和**反射**

#### 二维空间

在二维空间中，正交矩阵具有两种形式

$$
R = \begin{bmatrix}
\cos\theta & -\sin\theta \\
\sin\theta  & \cos\theta \\
\end{bmatrix},\qquad
M = \begin{bmatrix}
\cos\theta & \sin\theta \\
\sin\theta  & -\cos\theta \\
\end{bmatrix}
$$

- $R$ 表示旋转变换，旋转角度为 $\theta$
- $M$ 表示反射变换，对称面为 $y = \tan\frac{\theta}{2}x$

#### 三维空间

##### 旋转变换

**标准旋转矩阵：**

$$
R_x = \begin{bmatrix}
1 & 0 & 0 \\
0 & \cos \theta & -\sin \theta \\
0 & \sin \theta & \cos \theta
\end{bmatrix},\quad
R_y = \begin{bmatrix}
\cos \theta & 0 & \sin \theta \\
0 & 1 & 0 \\
-\sin \theta & 0 & \cos \theta
\end{bmatrix},\quad
R_z = \begin{bmatrix}
\cos \theta & -\sin \theta & 0 \\
\sin \theta & \cos \theta & 0 \\
0 & 0 & 1
\end{bmatrix}.
$$

**Rodrigues 旋转矩阵：**

设旋转轴为单位向量为 $\mathbf{u}=[u_{x},u_{y},u_{z}]$，旋转角为 $\theta$，则旋转矩阵为

$$
\begin{equation}
\begin{aligned}
R(\mathbf{u}, \theta) &= \cos \theta \cdot I + (1 - \cos \theta) \cdot \mathbf{uu}^T + \sin \theta \cdot [\mathbf{u}]_{\times}\\
&=\begin{bmatrix}
\cos \theta + u_x^2 (1 - \cos \theta) & u_x u_y (1 - \cos \theta) - u_z \sin \theta & u_x u_z (1 - \cos \theta) + u_y \sin \theta \\
u_y u_x (1 - \cos \theta) + u_z \sin \theta & \cos \theta + u_y^2 (1 - \cos \theta) & u_y u_z (1 - \cos \theta) - u_x \sin \theta \\
u_z u_x (1 - \cos \theta) - u_y \sin \theta & u_z u_y (1 - \cos \theta) + u_x \sin \theta & \cos \theta + u_z^2 (1 - \cos \theta)
\end{bmatrix}
\end{aligned}
\end{equation}
$$

对于旋转轴不经过原点的情况，则需要通过**平移-旋转-逆平移**的复合变换实现

:::{admonition} Rodrigues 公式证明
:class: tip, dropdown

将任意向量 $\mathbf{v}$ 进行分解

$$
\mathbf{v} = \mathbf{v}_{\scriptscriptstyle/\!/} + \mathbf{v}_{\perp},
$$

其中

- 平行于轴的分量：$\mathbf{v}_{\scriptscriptstyle/\!/}=\mathbf{u}\ (\mathbf{v}\cdot\mathbf{u})=\mathbf{u}\ (\mathbf{u}^{T}\mathbf{v}) = (\mathbf{u}\mathbf{u}^{T})\mathbf{v}$

- 垂直于轴的分量：$\mathbf{v}_{\perp}=\mathbf{v} - \mathbf{v}_{\scriptscriptstyle/\!/} = (I - \mathbf{u}\mathbf{u}^{T})\mathbf{v}$

绕 $u$ 旋转时（旋转是线性变换）

- 平行分量保持不变：$\mathbf{v}_{\scriptscriptstyle/\!/}^{'} = \mathbf{v}_{\scriptscriptstyle/\!/}$

- 垂直分量绕 $\mathbf{u}$ 旋转 $\theta$：$\mathbf{v}_{\perp}^{'}=\cos\theta\cdot\mathbf{v}_{\perp} + \sin\theta\cdot(\mathbf{u}\times\mathbf{v}_{\perp})$

关于垂直分量：

$\mathbf{v}_{\perp}$ 和 $\mathbf{u}\times\mathbf{v}_{\perp}$ 是垂直于 $\mathbf{u}$ 的平面上的一组正交基，且满足 

$$
\mathbf{v}_{\perp}^{'}\cdot\mathbf{v}_{\perp}=\cos\theta,
$$

和

$$\mathbf{v}_{\perp}^{'}\cdot\mathbf{v}_{\perp}^{'}=\cos^{2}\theta\cdot\mathbf{v}_{\perp}\cdot\mathbf{v}_{\perp} + \sin^{2}\theta\cdot(\mathbf{u}\times\mathbf{v}_{\perp})\cdot(\mathbf{u}\times\mathbf{v}_{\perp})=\mathbf{v}_{\perp}\cdot\mathbf{v}_{\perp}.$$

于是，总旋转后的向量为

$$
\mathbf{v}^{'}=\mathbf{v}_{\scriptscriptstyle/\!/}^{'}+\mathbf{v}_{\perp}^{'}=(\mathbf{u}\mathbf{u}^{T})\mathbf{v}+\cos\theta(I - \mathbf{u}\mathbf{u}^{T})\mathbf{v}+\sin\theta\cdot(\mathbf{u}\times\mathbf{v}),
$$

由于

$$
\mathbf{u}\times\mathbf{v}=\begin{bmatrix}
0 & -u_z & u_y \\
u_z & 0 & -u_x \\
-u_y & u_x & 0
\end{bmatrix}
\begin{bmatrix}
v_{x}\\v_{y}\\v_{z}
\end{bmatrix} = [\mathbf{u}]_{\times},
$$

因此

$$
\mathbf{v}^{'}=[\cos\theta\cdot I+(1-\cos\theta)\cdot\mathbf{u}\mathbf{u}^{T}+\sin\theta\cdot[\mathbf{u}]_{\times}]\mathbf{v},
$$

故

$$
R(\mathbf{u}, \theta) = \cos \theta \cdot I + (1 - \cos \theta) \cdot \mathbf{uu}^T + \sin \theta \cdot [\mathbf{u}]_{\times}.
$$

:::


##### 反射变换

**标准反射矩阵**

$$
M_{xy}=\begin{bmatrix}
1 & 0 & 0 \\
0 & 1 & 0 \\
0 & 0 & -1
\end{bmatrix},\quad
M_{yz}=\begin{bmatrix}
-1 & 0 & 0 \\
0 & 1 & 0 \\
0 & 0 & 1
\end{bmatrix},\quad
M_{xz}=\begin{bmatrix}
1 & 0 & 0 \\
0 & -1 & 0 \\
0 & 0 & 1
\end{bmatrix}.
$$

**一般反射矩阵**

关于单位法向量 $\mathbf{n}=[n_{x}\ n_{y}\ n_{z}]^{T}$ 定义的（过原点的）平面的反射矩阵为

$$
M=I-2\mathbf{n}\mathbf{n}^{T} = \begin{bmatrix}
1 - 2n_{x}^2 & -2n_{x}n_{y} & -2n_{x}n_{z} \\
-2n_{x}n_{y} & 1-2n_{y}^2 & -2n_{y}n_{z} \\
-2n_{x}n_{z} & 2n_{y}n_{z} & 1-2n_{z}^2\\
\end{bmatrix},
$$

对于平面不经过原点的情况，则需要通过**平移-反射-逆平移**的复合变换实现

:::{admonition} 反射公式证明
:class: tip, dropdown

将任意向量 $\mathbf{v}$ 进行分解

$$
\mathbf{v} = \mathbf{v}_{\scriptscriptstyle/\!/} + \mathbf{v}_{\perp},
$$

其中

- 平行于平面的分量：$\mathbf{v}_{\scriptscriptstyle/\!/}$

- 垂直于平面的分量：$\mathbf{v}_{\perp}=\mathbf{n}\ (\mathbf{v}\cdot\ \mathbf{n})=(\mathbf{n}\mathbf{n}^{T})\mathbf{v}$

反射操作不改变 $\mathbf{v}_{\scriptscriptstyle/\!/}$，并将 $\mathbf{v}_{\perp}$ 反向，故反射后的向量为

$$
\mathbf{v}^{'}=\mathbf{v}_{\scriptscriptstyle/\!/}-\mathbf{v}_{\perp}=\mathbf{v}-2\mathbf{n}\mathbf{n}^{T}\mathbf{v} = (I-2\mathbf{n}\mathbf{n}^{T})\mathbf{v},
$$

因此，反射矩阵为

$$
M = I-2\mathbf{n}\mathbf{n}^{T}.
$$

:::

### 实对称矩阵的对角化

对于实对称矩阵 $A$，存在正交矩阵 $Q$ 和对角矩阵 $\Lambda$，使得

$$
Q^{-1}AQ = Q^{T}AQ = \Lambda.
$$


#### 矩阵 $A$ 的特征值为实数

设 $\lambda\in\mathbb{C}$ 为矩阵 $A$ 的特征值，$\mathbf{v}\in\mathbb{C}^{n}$ 为对应的特征向量，则

$$
A\mathbf{v} = \lambda\mathbf{v} \Rightarrow \mathbf{v}^{\dagger}A\mathbf{v}=\lambda\mathbf{v}^{\dagger}\mathbf{v},
$$

另一方面

$$
A\mathbf{v} = \lambda\mathbf{v} \Rightarrow \mathbf{v}^{\dagger}A^{\dagger}=\bar{\lambda}\mathbf{v}^{\dagger} \Rightarrow \mathbf{v}^{\dagger}A=\bar{\lambda}\mathbf{v}^{\dagger} \Rightarrow \mathbf{v}^{\dagger}A\mathbf{v}=\bar{\lambda}\mathbf{v}^{\dagger}\mathbf{v},
$$

由于 $\mathbf{v}^{\dagger}\mathbf{v}>0$，故 $\lambda = \bar{\lambda}$，得到 $\lambda\in\mathbb{R}$

设 $\mathbf{v} = \mathbf{a} + i\mathbf{b}$，其中，$\mathbf{a},\mathbf{b}\in\mathbb{R}^{n}，$则

$$
A\mathbf{v} = \lambda\mathbf{v} \Rightarrow A(\mathbf{a} + i\mathbf{b}) = A\mathbf{a} + iA\mathbf{b} = \lambda\mathbf{a} + i\lambda\mathbf{b},
$$

因此

$$
A\mathbf{a} = \lambda\mathbf{a},\quad A\mathbf{b} = \lambda\mathbf{b},
$$

这表明特征值 $\lambda$ 存在对应的实特征向量

#### 不同特征根的特征向量正交

设特征值 $\lambda_{1}\neq\lambda_{2}$ 对应的特征向量分别为 $\mathbf{v}_{1}\in\mathbb{R}^{n}$ 和 $\mathbf{v}_{2}\in\mathbb{R}^{n}$，则

$$
\lambda_{1}\mathbf{v}_{1}^{T}\mathbf{v}_{2}=(\lambda_{1}\mathbf{v}_{1})^{T}\mathbf{v}_{2}=(A\mathbf{v}_{1})^{T}\mathbf{v}_{2}=\mathbf{v}_{1}^{T}A\mathbf{v}_{2}=\lambda_{2}\mathbf{v}_{1}^{T}\mathbf{v}_{2},
$$

由于 $\lambda_{1} \neq \lambda_{2}$，因此 $\mathbf{v}_{1}^{T}\mathbf{v}_{2} = 0$,

#### 正交对角化

假设对于 $n-1$ 阶实对称矩阵，结论成立，则对于 $n$ 阶实对称矩阵 $A$，取其某一单位特征向量 $\mathbf{v}_{1}$，构造正交矩阵 $V = [\mathbf{v}_{1}\ V_{n-1}]\in\mathbb{R}^{n\times n}$，则

$$
\begin{equation}
\begin{aligned}
V^{T}AV &= \begin{bmatrix}\mathbf{v}_{1}^{T} \\ V_{n-1}^{T}\end{bmatrix}A\ [\mathbf{v}_{1}\ V_{n-1}]\\
&=\begin{bmatrix}
\mathbf{v}_{1}^{T}A\mathbf{v}_{1} & \mathbf{v}_{1}^{T}AV_{n-1} \\
V_{n-1}^{T} A\ \mathbf{v}_{1} & V_{n-1}^{T} A\ V_{n-1}
\end{bmatrix} \\
&= \begin{bmatrix}
\lambda_{1} & \mathbf{0} \\
\mathbf{0} & V_{n-1}^{T} A\ V_{n-1}
\end{bmatrix},
\end{aligned}
\end{equation}
$$

由于矩阵 $V_{n-1}^{T} A\ V_{n-1}$ 是 $n-1$ 阶实对称矩阵，因此存在正交矩阵 $M\in\mathbb{R}^{(n-1)\times (n-1)}$ 将其对角化

$$
M^{T}(V_{n-1}^{T} A\ V_{n-1})M = \Lambda_{n-1},
$$

因此

$$
(V\begin{bmatrix}
I & \\ & M
\end{bmatrix})^{T}A\ (V\begin{bmatrix}
I & \\ & M
\end{bmatrix}) = \begin{bmatrix}
\lambda_{1} & \\ & \Lambda_{n-1}
\end{bmatrix},
$$

其中，$(V\begin{bmatrix}
I & \\ & M
\end{bmatrix})\in\mathbb{R}^{n\times n}$ 是正交矩阵

由于

$$
Q^{-1}AQ = \Lambda \Rightarrow AQ = Q\Lambda,
$$

代入 $Q=[\mathbf{q}_{1}\ \mathbf{q}_{2}\ \cdots \mathbf{q}_{n}]$，和 $\Lambda = \text{diag}(\lambda_{1},\lambda_{2},\cdots,\lambda_{n})$，得到

$$
\begin{bmatrix}A\mathbf{q}_{1}& A\mathbf{q}_{2}& \cdots & A\mathbf{q}_{n}\end{bmatrix} = \begin{bmatrix}\lambda_{1}\mathbf{q}_{1}& \lambda_{1}\mathbf{q}_{2}& \cdots& \lambda_{1}\mathbf{q}_{n}\end{bmatrix},
$$

因此 $Q$ 的列向量是矩阵 $A$ 的特征向量，$\Lambda$ 的对角元素是对应的特征值

