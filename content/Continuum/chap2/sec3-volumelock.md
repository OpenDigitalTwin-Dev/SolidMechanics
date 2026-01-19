# 闭锁问题

*连续体在外部作用下需同时满足（不考虑温度因素）质量守恒方程与动量守恒方程*

动量守恒方程为

$$
\nabla \cdot \boldsymbol{\sigma} + \mathbf{f} = \rho \mathbf{a}
$$

在拉格朗日描述下，质量守恒方程通过体积映射自然成立（如 $\rho_{0}=J\rho$）。对于一般可压缩材料，应力张量可通过本构关系完全表示为位移（或速度）及其梯度的函数，从而实现对动量方程中应力变量的替换（消元）

然而，对于不可压问题，这种“消元”策略会失效。问题出在动量方程中与体积变形相关的应力分量的处理上

引入加法分解，将柯西应力张量 $\boldsymbol{\sigma}$ 拆分为“偏应力”和“球张量”两部分

$$
\boldsymbol{\sigma} = \mathbf{s} + p \mathbf{I},
$$

其中，$p = \frac{1}{3}\text{tr}(\boldsymbol{\sigma})$ 表示平均正应力。偏应力部分对应剪切畸变，球张量部分对应体积改变。动量守恒方程随之改写为：

$$
\nabla \cdot \mathbf{s} + \nabla p + \mathbf{f} = \rho \mathbf{a}
$$

对于**可压缩线弹性材料**，程是封闭的，因为 $\mathbf{s}$ 和 $p$ 均可由位移 $\mathbf{u}$ 显式表达：

1. $\mathbf{s} = 2\mu \text{dev}(\boldsymbol{\varepsilon}(\mathbf{u}))$ （$\mu$ 是剪切模量，偏应力由畸变决定）

2. $p = K (\nabla \cdot \mathbf{u})$ （$K$ 是体积模量，压力由体积应变决定）

对于**可压缩弹塑性材料（如金属）**，偏应力的演化具有历史依赖性，但在时间步内依然由运动学变量驱动：

$$
\mathbf{s}(\mathbf{u}, \text{history}) = \begin{cases} 
\mathbf{s}_n + 2\mu \text{dev}(\Delta \boldsymbol{\varepsilon}(\mathbf{u})) & \text{elasticity} \\
\alpha (\mathbf{u}) \left[ \mathbf{s}_n + 2\mu \text{dev}(\Delta \boldsymbol{\varepsilon}(\mathbf{u})) \right] & \text{elastoplasticity}
\end{cases}
$$

且压力率仍由体积胡克定律控制（考虑塑性不可压 $\text{tr}(\dot{\boldsymbol{\varepsilon}}^p) = 0$）：

$$
\dot{p} = K (\nabla \cdot \mathbf{v} - \underbrace{\text{tr}(\dot{\boldsymbol{\varepsilon}}^p)}_{0}) = K \nabla \cdot \mathbf{v}
$$

此时，方程组原则上仍可对 $p$ 进行消元

然而，**不可压缩材料（或不可压极限）**，密度恒定，根据质量守恒方程，有

$$
\nabla\cdot\mathbf{v} = 0
$$


由此引发出两个本质问题：

**1.本构关系的数学奇异性**：对于不可压弹性，$K \to \infty$ 且 $\nabla \cdot \mathbf{u} \to 0$（小变形），压力表达式变为 $0 \cdot \infty$ 的不定式：

$$
p = \lim_{K \to \infty} (-K \nabla \cdot \mathbf{u})
$$
这意味着压力无法再通过微小的体积应变来计算，物理上压力转变为由平衡方程与边界条件决定的独立**拉格朗日乘子**

**2.数值上的体积闭锁 (Volumetric Locking)**：对于金属塑性 (J2 流动理论)，虽然材料具有有限的体积模量 $K$，但在显著塑性流动阶段，塑性模量 $H$ 远小于体积模量 ($H \ll K$)，材料表现出**近乎不可压**特性。此时 $K$ 起到罚参数的作用。若强行使用纯位移格式进行消元，动量方程中将出现刚度极大的体积项。这在数值上导致刚度矩阵条件数恶化，在离散空间中导致有限元网格被过度约束，无法同时满足平衡方程与等容条件，从而引发**体积闭锁**


## 解决策略

在工业界主流的有限元软件中，通常使用 F-bar (B-bar 的大变形版本) > 缩减积分 (带沙漏控制) > 混合元 的求解策略

**1.B-bar 方法（及其大变形版本 F-bar）：隐式分析（Implicit）中的“黄金标准”**

对于金属弹塑性（尤其是涉及大变形的金属成型），B-bar 和 F-bar 是最常用的处理体积闭锁的技术

**原理**：无需引入额外的压力节点（即不增加自由度）。通过修改单元的 应变-位移矩阵 (B矩阵)，强行把体积应变（导致锁死的部分）和偏应变（导致形状改变的部分）分开积分

B-bar：用于小变形

F-bar：用于大变形（有限应变），它对变形梯度张量 $\mathbf{F}$ 进行乘法分解（$\mathbf{F} = \mathbf{F}^{vol} \mathbf{F}^{dev}$）

**优点**

精度高：能通过“片试验 (Patch Test)”，精度通常优于缩减积分

无沙漏模式：不需要像缩减积分那样调节沙漏控制参数

效率高：虽然比缩减积分慢一些，但比混合元（增加自由度）快

**软件对应**

Ansys：SOLID185 单元默认开启 B-bar (Keyopt(2)=0)，处理全积分下的闭锁

Abaqus：对应于“非协调模式”单元（Incompatible mode, C3D8I），虽然内部实现略有不同，但目的和效果类似 F-bar，非常适合弯曲和塑性问题。

**2.缩减积分 (Reduced Integration)地位：显式动力学（Explicit）的首选，大模型隐式分析的妥协**

这是 LS-DYNA 和 Abaqus/Explicit 中的绝对主力

**原理**：对于六面体单元（8节点），全积分需要 $2\times2\times2=8$ 个积分点。缩减积分只用 1 个中心积分点。在中心点，不可压约束 $\nabla \cdot \mathbf{v} = 0$ 只是一个标量方程，而单元有多个节点自由度，约束数量 < 自由度数量，所以网格“软”了，不会锁死

**沙漏 (Hourglass)**：只有一个积分点会导致某些变形模式（梯形、沙漏形）下应变为 0（零能模式），导致网格发生非物理的畸变。必须引入 “沙漏控制” (Hourglass Control)（人为加一点刚度或粘性）来抑制

**优点**：

计算极快：计算代价小；无锁死

**软件对应**

Abaqus：C3D8R（Reduced）。做汽车碰撞（金属塑性大变形）时几乎全用该单元

Ansys：SOLID185 设置为缩减积分模式

**3.混合元 (Mixed Formulation / Hybrid Elements)地位：处理“极度”不可压（橡胶）的首选，金属塑性的备选**

虽然混合元（即联立求解 $\mathbf{u}-p$）理论最严谨，但在金属塑性中，它往往不是第一选择，除非问题极其困难

**原理**：把压力 $p$ 作为独立自由度求解

**缺点**

计算昂贵：增加了额外的自由度，且破坏了刚度矩阵的正定性（变成鞍点问题），对线性方程组求解器要求高，计算时间长

混合元更多用于橡胶（Hyperelasticity）。因为橡胶是绝对不可压（$\nu \approx 0.4999$），而金属塑性通常伴随弹性的体积变化，B-bar 通常足够

**软件对应**

Abaqus：C3D8H（H 代表 Hybrid，即混合元）。通常用于橡胶，或者当普通单元在金属大变形中表现不佳时使用

**针对金属弹塑性问题，实际工程中的选择策略如下：**

**首选方案（精度与效率平衡）**：使用 六面体单元 + B-bar/F-bar 技术。在 Abaqus 中，对应 C3D8I（非协调模式，抗剪切闭锁和体积闭锁效果好）。在 Ansys 中，对应 SOLID185（默认 B-bar）

**大变形/冲击/碰撞（显式求解）**：使用 六面体单元 + 缩减积分 + 增强沙漏控制。在 Abaqus 中，对应 C3D8R

**四面体网格（复杂几何）**：不要用一阶四面体（C3D4），它有严重的体积闭锁，算出来的力严重过大。建议使用二阶四面体（C3D10）或修正的四面体（C3D10M），这些单元内部通常已经内置了类似混合元的处理机制来防止闭锁