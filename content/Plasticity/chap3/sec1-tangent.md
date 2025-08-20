# 弹塑性切线模量

## 塑性乘子

根据塑性流动法则和硬化法则，有

$$
\begin{equation}
\begin{aligned}
\dot{\boldsymbol{\varepsilon}}^{p} &= \dot{\gamma}\mathbf{N}(\boldsymbol{\sigma},\mathbf{A}),\\
\dot{\boldsymbol{\alpha}} &= \dot{\gamma}\mathbf{H}(\boldsymbol{\sigma},\mathbf{A}),
\end{aligned}
\end{equation}
$$

其中，$\mathbf{H}$ 是一般化的硬化模量，决定了硬化参数 $\boldsymbol{\alpha}$ 的演化

若材料属于塑性屈服状态，则

$$
\dot{\Phi} = \frac{\partial \Phi}{\partial \boldsymbol{\sigma}}:\dot{\boldsymbol{\sigma}} + \frac{\partial \Phi}{\partial \mathbf{A}}\dot{\mathbf{A}},
$$ (sec1-eq:phi-der)

代入

$$
\dot{\boldsymbol{\sigma}} = \mathbf{D}^{e}:(\dot{\boldsymbol{\varepsilon}}-\dot{\boldsymbol{\varepsilon}}^p) = \mathbf{D}^{e}:(\dot{\boldsymbol{\varepsilon}}-\dot{\gamma}\mathbf{N})
$$ (sec1-eq:sigma-der)

和

$$
\dot{\mathbf{A}} = \frac{\mathrm{d} \frac{\partial \psi^p}{\partial \boldsymbol{\alpha}}}{\mathrm{d} t} = \frac{\partial^2 \psi^p}{\partial \boldsymbol{\alpha}^2}\dot{\boldsymbol{\alpha}} = \frac{\partial^2 \psi^p}{\partial \boldsymbol{\alpha}^2}\dot{\gamma}\mathbf{H}
$$

到式 {eq}`sec1-eq:phi-der` 得到

$$
\dot{\Phi} = \frac{\partial \Phi}{\partial \boldsymbol{\sigma}}:\mathbf{D}^{e}:(\dot{\boldsymbol{\varepsilon}}-\dot{\gamma}\mathbf{N}) + \dot{\gamma}\frac{\partial \Phi}{\partial \mathbf{A}}\frac{\partial^2 \psi^p}{\partial \boldsymbol{\alpha}^2}\mathbf{H}
$$

于是得到

$$
\dot{\gamma} = \frac{\frac{\partial \Phi}{\partial \boldsymbol{\sigma}}:\mathbf{D}^{e}:\dot{\boldsymbol{\varepsilon}}}{\frac{\partial \Phi}{\partial \boldsymbol{\sigma}}:\mathbf{D}^{e}:\mathbf{N}-\frac{\partial \Phi}{\partial \mathbf{A}}\frac{\partial^2 \psi^p}{\partial \boldsymbol{\alpha}^2}\mathbf{H}},
$$ (sec1-eq:gamma)

## 弹塑性切线模量

将式 {eq}`sec1-eq:gamma` 代入到式 {eq}`sec1-eq:sigma-der` 中，得到

$$
\dot{\boldsymbol{\sigma}} = \mathbf{D}^{ep}:\dot{\boldsymbol{\varepsilon}},
$$

其中

$$
\mathbf{D}^{ep} = \mathbf{D}^{e} - \frac{(\mathbf{D}^{e}:\mathbf{N})\otimes(\mathbf{D}^{e}:\frac{\partial \Phi}{\partial \boldsymbol{\sigma}})}{\frac{\partial \Phi}{\partial \boldsymbol{\sigma}}:\mathbf{D}^{e}:\mathbf{N}-\frac{\partial \Phi}{\partial \mathbf{A}}\frac{\partial^2 \psi^p}{\partial \boldsymbol{\alpha}^2}\mathbf{H}},
$$

是**弹塑性切线模量**，通常也被称为**连续弹塑性切线模量**，它是单轴拉伸应力-应变曲线中的常量模量 $E_{ep}$ 的高维一般化

### 对称性

对于关联塑性流动，有

$$
\mathbf{N} = \frac{\partial \Phi}{\partial \boldsymbol{\sigma}},
$$

此时， $\mathbf{D}^{ep}$ 是对称的；而对于非关联塑性流动，$\mathbf{D}^{ep}$ 一般是非对称的

