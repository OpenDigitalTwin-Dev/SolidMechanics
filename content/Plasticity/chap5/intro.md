# 本构积分

<span class="gray-text">
本构积分决定了有限元分析的数值精度与收敛性，是实现复杂材料非线性行为模拟的核心环节
</span>

本构积分在有限元求解中作用于**单元应力更新阶段**，即根据**应变增量**（通过求解整体刚度矩阵得到的**位移增量**获得），更新材料点**应力**和**内变量状态**（如塑性应变、硬化参数）的核心计算过程，即，已知

$$
\begin{equation}
\boldsymbol{\varepsilon}_{n+1},\ \boldsymbol{\varepsilon}_{n}^{e},\ \boldsymbol{\varepsilon}_{n}^{p},\ \bar{\varepsilon}_{n}^{p},\ \boldsymbol{\sigma}_{n},\ \dots 
\end{equation}
$$

求解

$$
\begin{equation}
\boldsymbol{\sigma}_{n+1},\ \boldsymbol{\varepsilon}_{n+1}^{p},\ \bar{\varepsilon}_{n+1}^{p},\ \dots
\end{equation}
$$