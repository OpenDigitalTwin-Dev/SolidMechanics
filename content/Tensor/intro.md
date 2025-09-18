# 张量运算

<span class="gray-text">
张量分析是描述连续介质力学行为不可或缺的数学工具
</span>

## 双点积（Double Dot Product）

双点积是一种缩并运算，它对两个张量的两对指标进行求和

$$
A:B:=A_{ij}B_{ij}.
$$

:::{admonition} $A:B=A_{ij}B_{ij}=\text{tr}(AB^{T})=\text{tr}(A^{T}B)=\text{tr}(B^{T}A)$
:class: tip, dropdown

$
A_{ij}B_{ij} = A_{ij}B^{T}_{ji} = \text{tr}(AB^{T})
$

且

$
\text{tr}(A) = \text{tr}(A^{T})
$

:::

:::{admonition} $A:BC=(B^{T}A):C$
:class: tip, dropdown

$
A:BC = \text{tr}(C^{T}B^{T}A) = (B^{T}A) : C
$

:::


## 双积（Dyadic Product）

双积，也称为外积（Outer Product）或张量积（Tensor Product），是一种将两个低阶张量组合成一个高阶张量的运算。