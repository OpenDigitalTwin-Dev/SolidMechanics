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

## 正交变换与相似变换

### 相似变换

相似变换是同一线性变换在不同基下的矩阵表示之间的转换关系。给定线性变换 

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
B = P^{-1}AP
$$

称矩阵 $A$ 和矩阵 $B$ 是相似的

#### 相似变换的性质

### 正交变换



