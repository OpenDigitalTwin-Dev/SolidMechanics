# 各向同性硬化模型

<span class="gray-text">
各向同性硬化模型假设屈服函数是应力的各向同性函数，即在整个塑性变形过程中，屈服面以其中心为原点（位置不变），保持形状不变地向外均匀膨胀，反映了材料在各个方向上的屈服行为一致
</span>

在金属塑性中，硬化内变量的本质与晶体学微观结构中**位错密度**的变化密切相关，这种变化导致对塑性流动的阻力以各向同性的方式增加。在各向同性硬化的本构描述中，内变量集合 $\boldsymbol{\alpha}$ 通常仅包含一个**标量变量**，该变量决定了屈服面的大小。在各向同性硬化的建模过程中，**应变硬化**和**功硬化**是两种常用且有效的方法，广泛应用于对不同材料行为的建模

## 应变硬化

在应变硬化中，硬化内变量通常选为应变的标量度量，一个经典的例子是 **Mises 等效塑性应变**，也被称为 **累积塑性应变**

$$
\bar{\varepsilon}^{p} = \int_{0}^{t}\sqrt{\frac{2}{3}\dot{\boldsymbol{\varepsilon}}^{p}:\dot{\boldsymbol{\varepsilon}}^{p}}\ \mathrm{d}t=\int_{0}^{t}\sqrt{\frac{2}{3}}\|\dot{\boldsymbol{\varepsilon}}^{p}\|\ \mathrm{d}t,
$$

因此

$$
\dot{\bar{\varepsilon}}^{p} = \sqrt{\frac{2}{3}}\|\dot{\boldsymbol{\varepsilon}}^{p}\|,
$$ (sec1-eq:effective-strain)

对于 Mises 屈服准则，有

$$
\mathbf{N} = \frac{\partial \Phi}{\partial \boldsymbol{\sigma}}=\sqrt{\frac{3}{2}}\frac{\mathbf{s}}{\|\mathbf{s}\|},
$$

因此

$$
\dot{\boldsymbol{\varepsilon}}^{p}=\dot{\gamma}\frac{\partial \Phi}{\partial \boldsymbol{\sigma}}=\dot{\gamma}\sqrt{\frac{3}{2}}\frac{\mathbf{s}}{\|\mathbf{s}\|},
$$

代入到式 {eq}`sec1-eq:effective-strain` 中得到

$$
\dot{\bar{\varepsilon}}^{p} = \dot{\gamma}.
$$

相应地，Mises 各向同性应变硬化模型为

$$
\sigma_{y} = \sigma_{y}(\bar{\varepsilon}^{p}).
$$

### 线性硬化

$$
\sigma_{y}(\bar{\varepsilon}^{p})=\sigma_{y0}+H\bar{\varepsilon}^{p},
$$

其中，$\sigma_{y0}$ 是初始屈服强度

## 功硬化

在功硬化模型中，将**耗散塑性功**作为硬化状态的变量

$$
w^{p} = \int_{0}^{t}\boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}^{p}}\ \mathrm{d}t,
$$

于是

$$
\dot{w}^{p}=\boldsymbol{\sigma}:\dot{\boldsymbol{\varepsilon}^{p}},
$$

相应地，Mises 各向同性应变硬化模型为

$$
\sigma_{y} = \sigma_{y}(w^{p}),
$$

## 热力学方面

选取

$$
\boldsymbol{\alpha} = \{\bar{\varepsilon}_{n}^{p}\},\quad \mathbf{A} = \{\kappa\},
$$

硬化模型可以写为

$$
\sigma_{y}(\bar{\varepsilon}^p) = \sigma_{0} + \kappa(\bar{\varepsilon}^p),
$$


故

$$
\begin{equation}
\frac{\partial^2 \psi^p}{\partial \boldsymbol{\alpha}^2}=\frac{\partial \psi^p}{\partial {\bar{\varepsilon}^{p}}^{2}}=\frac{\partial \kappa}{\partial \bar{\varepsilon}^{p}} = H(\bar{\varepsilon}^{p}),
\end{equation}
$$

对于线性硬化，有 $H(\bar{\varepsilon}^{p}) \equiv H$. 