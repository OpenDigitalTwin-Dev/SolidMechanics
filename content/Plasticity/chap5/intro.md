# 本构积分

<span class="gray-text">
本构积分决定了有限元分析的数值精度与收敛性，是实现复杂材料非线性行为模拟的核心环节
</span>

本构积分在有限元求解中作用于**单元应力更新阶段**，即根据**应变增量**（通过求解整体刚度矩阵得到的**位移增量**获得），更新材料点**应力**和**内变量状态**（如塑性应变、硬化参数）的核心计算过程


其核心在于路径依赖的应力更新：
1. 首先进行弹性预测，计算试应力
2. 若试应力超出屈服面，则通过塑性修正（如回归映射算法）将应力拉回更新后的屈服面
3. 依据流动法则更新塑性应变和硬化变量，确保严格满足屈服条件与塑性一致性要求，最终输出真实应力、一致切线模量及更新后的历史变量

即，已知

$$
\begin{equation}
\boldsymbol{\varepsilon}_{n}^{e},\ \boldsymbol{\varepsilon}_{n}^{p},\ \bar{\varepsilon}_{n}^{p},\ \boldsymbol{\sigma}_{n},\ \boldsymbol{\varepsilon}_{n+1}
\end{equation}
$$

求解

$$
\begin{equation}
\boldsymbol{\varepsilon}_{n+1}^{p},\ \bar{\varepsilon}_{n+1}^{p},\ \boldsymbol{\sigma}_{n+1},\ \dots
\end{equation}
$$