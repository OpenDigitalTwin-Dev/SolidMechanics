# 应变与位移

<span class="gray-text">
物体的变形源于其内部各质点之间的相对位移
</span>

当外力或环境条件发生变化时，物体内部的质点会产生不同程度的移动，这种相对位移导致了物体的几何形状和尺寸发生变化。通过对质点间相对位移的分析，可以定量描述材料的应变状态，并进一步研究其力学性能和变形规律

位移函数 $u:\Omega_{0}\rightarrow \mathbb{R}^{3}$ 可以表示为

$$
u(\mathbf{X}) = \mathbf{x} - \mathbf{X},
$$

其中，$\mathbf{X}=[X_{1},X_{2},X_{3}]^{T}$ 为物体内部任意一点的初始位置，$\mathbf{x}=[x_{1},x_{2},x_{3}]^{T}$ 为该点在受力作用下移动到的新位置

## 刚体运动

在刚体运动中，物体内部任意两点之间的距离始终保持不变，因此物体只发生整体的平移或旋转，而不会产生形变

### 平移

若 

$$
\mathbf{x} = \mathbf{X} + \mathbf{c},
$$

其中，$\mathbf{c} = [c_{1},c_{2},c_{3}]^{T}$，此时物体发生平移

$$
u(\mathbf{X}) = \mathbf{c}.
$$

### 旋转

若 

$$
\mathbf{x} = Q\mathbf{X},
$$

其中，$Q\in\mathbb{M}^{3}$ 是[正交矩阵](../chap2/sec1-OT.md)，则物体发生旋转，此时

$$
u(\mathbf{X}) = (Q-I)\mathbf{X}.
$$

## 均匀拉伸和压缩

在均匀拉伸或压缩运动中，物体在外力作用下沿某一方向均匀地变长或变短，表现为物体内部各质点的位置坐标按比例发生变化

$$
\begin{bmatrix}x_{1}\\x_{2}\\x_{3}\end{bmatrix} = \begin{bmatrix}k_{1}X_{1}\\k_{2}X_{2}\\k_{3}X_{3}\end{bmatrix} =\begin{bmatrix}k_{1}&&\\&k_{2}&\\&&k_{3}\end{bmatrix}\begin{bmatrix}X_{1}\\X_{2}\\X_{3}\end{bmatrix},
$$

其中，$k_{i}>0$，当 $k_{i}>1$ 时，为拉伸变形；当 $k_{i}<1$ 时，为压缩变形。此时

$$
u(\mathbf{X}) = (I - \text{diag}(k_{1},k_{2},k_{3}))\mathbf{X}.
$$

## 剪切变形

在剪切变形中，物体内部的某一层相对于另一层发生平行移动，导致物体的形状发生改变，但体积基本保持不变

### 简单剪切

简单剪切是材料层间沿固定方向发生相对滑动，而垂直于这些平面的方向保持长度不变的变形模式，例如

```{figure} ../../../images/Tensor/chap1/simple-shear.png
---
width: 200px
name: sec1-fig:simple-shear
---
二维简单剪切示意图
```

三维情形下，以 $x$-$y$ 面的剪切移动为例


$$
\begin{bmatrix}x_{1}\\x_{2}\\x_{3}\end{bmatrix} = \begin{bmatrix}X_{1} + \tan\theta_{xy}\cdot X_{2}\\X_{2}\\X_{3}\end{bmatrix} =\begin{bmatrix}1&\tan\theta_{xy}&0\\0&1&0\\0&0&1\end{bmatrix}\begin{bmatrix}X_{1}\\X_{2}\\X_{3}\end{bmatrix},
$$

注意到，变换矩阵的行列式等于 $1$，因此简单剪切变形并不会导致物体体积发生变化

可以考虑多个简单剪切的叠加

$$
\begin{equation}
\begin{aligned}
&\begin{bmatrix}1&0&0\\0&1&\tan\theta_{yz}\\0&0&1\end{bmatrix}
\begin{bmatrix}1&0&\tan\theta_{xz}\\0&1&0\\0&0&1\end{bmatrix}
\begin{bmatrix}1&\tan\theta_{xy}&0\\0&1&0\\0&0&1\end{bmatrix}\\
=&\begin{bmatrix}1&\tan\theta_{xy}&\tan\theta_{xz}\\0&1&\tan\theta_{yz}\\0&0&1\end{bmatrix}
\end{aligned}
\end{equation}
$$

在简单剪切变形过程中，物体的对称面会持续发生旋转

### 纯剪切

