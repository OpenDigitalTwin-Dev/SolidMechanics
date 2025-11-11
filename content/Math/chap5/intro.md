# Newmark 方法

Newmark 方法是一类针对微分方程求解的时间积分方法，对于弹塑性初值问题

$$
\begin{equation}
\begin{cases}
\mathbf{M} \ddot{\mathbf{u}}_{k+1} + \mathbf{C} \dot{\mathbf{u}}_{k+1} + \mathbf{F}^{\text{int}}_{k+1} = \mathbf{F}^{\text{ext}}_{k+1} \\
\mathbf{u}(t_0) = \mathbf{u}_0, \quad \dot{\mathbf{u}}(t_0) = \dot{\mathbf{u}}_0
\end{cases}
\end{equation}
$$ (intro-eq:equations)

使用插值公式

$$
\begin{equation}
\begin{aligned}
\mathbf{u}_{k+1} &= \mathbf{u}_k + \dot{\mathbf{u}}_k \Delta t + \ddot{\mathbf{u}}_k ( \frac{1}{2} - \beta ) \Delta t^2 + \ddot{\mathbf{u}}_{k+1} \beta \Delta t^2 \\
\dot{\mathbf{u}}_{k+1} &= \dot{\mathbf{u}}_k + \ddot{\mathbf{u}}_k (1 - \gamma) \Delta t + \ddot{\mathbf{u}}_{k+1} \gamma \Delta t
\end{aligned}
\end{equation}
$$ (intro-eq:interpolations)

其中，$\beta$ 和 $\gamma$ 是积分算法的参数，当 $\beta = 0$ 时为显式方法，$\beta \neq 0$ 时为隐式方法，对于一些特例

- $\gamma = \frac{1}{2}, \beta = \frac{1}{6}$：具有线性加速，$\Delta t_{cr} = \frac{3.464}{\omega}$
- $\gamma = \frac{1}{2}, \beta = \frac{1}{4}$：具有常平均加速，无条件稳定
- $\gamma = \frac{1}{2}, \beta = 0$：**中心差分方法**，$\Delta t_{cr} = \frac{2}{\omega}$

记

$$
\begin{equation}
\begin{aligned}
\tilde{\mathbf{u}}_{k+1} &= \mathbf{u}_k + \dot{\mathbf{u}}_k \Delta t + \ddot{\mathbf{u}}_k ( \frac{1}{2} - \beta ) \Delta t^2 \\
\dot{\tilde{\mathbf{u}}}_{k+1} &= \dot{\mathbf{u}}_k + \ddot{\mathbf{u}}_k (1 - \gamma) \Delta t
\end{aligned}
\end{equation}
$$ (intro-eq:interpolations-1)

于是

$$
\begin{equation}
\begin{aligned}
\mathbf{u}_{k+1} &= \tilde{\mathbf{u}}_{k+1} + \ddot{\mathbf{u}}_{k+1} \beta \Delta t^2 \\
\dot{\mathbf{u}}_{k+1} &= \dot{\tilde{\mathbf{u}}}_{k+1} + \ddot{\mathbf{u}}_{k+1} \gamma \Delta t
\end{aligned}
\end{equation}
$$ (intro-eq:interpolations-2)

将插值公式代入到 {eq}`intro-eq:equations`，得到

$$
\begin{equation}
\mathbf{M}{\color{red}\ddot{\mathbf{u}}_{k+1}} + \mathbf{C}(\dot{\tilde{\mathbf{u}}}_{k+1} + {\color{red}\ddot{\mathbf{u}}_{k+1}} \gamma \Delta t) + \mathbf{F}^{\text{int}}_{k+1} = \mathbf{F}^{\text{ext}}_{k+1}
\end{equation}
$$ (intro-eq:equations-1)

## 线弹性问题

对于线弹性问题，$\mathbf{F}^{\text{int}}$ 可以写为

$$
\begin{equation}
\mathbf{F}^{\text{int}} =\int_{E}\mathbf{B}^{T}\mathbb{C}\mathbf{B}\ \mathbf{d}E\cdot\mathbf{u}=\mathbf{K}\mathbf{u},
\end{equation}
$$

其中 $\mathbf{K}$ 是常量，于是，式 {eq}`intro-eq:equations-1` 可以写为

$$
\mathbf{M}{\color{red}\ddot{\mathbf{u}}_{k+1}} + \mathbf{C}(\dot{\tilde{\mathbf{u}}}_{k+1} + {\color{red}\ddot{\mathbf{u}}_{k+1}} \gamma \Delta t) + \mathbf{K}(\tilde{\mathbf{u}}_{k+1} + {\color{red}\ddot{\mathbf{u}}_{k+1}} \beta \Delta t^2) = \mathbf{F}^{\text{ext}}_{k+1}
$$

算法流程如下

**Step 1: 预测**

$$
\begin{equation}
\begin{aligned}
\tilde{\mathbf{u}}_{k+1} &= \mathbf{u}_k + \dot{\mathbf{u}}_k \Delta t + \ddot{\mathbf{u}}_k ( \frac{1}{2} - \beta ) \Delta t^2 \\
\dot{\tilde{\mathbf{u}}}_{k+1} &= \dot{\mathbf{u}}_k + \ddot{\mathbf{u}}_k (1 - \gamma) \Delta t
\end{aligned}
\end{equation}
$$

**Step 2: 求解**
$$
\ddot{\mathbf{u}}_{k+1} = \left( \mathbf{M} + \mathbf{C} \gamma \Delta t + \mathbf{K} \beta \Delta t^2 \right)^{-1}
\left( \mathbf{F}^{\text{ext}}_{k+1} - \mathbf{K} \tilde{\mathbf{u}}_{k+1} - \mathbf{C} \dot{\tilde{\mathbf{u}}}_{k+1} \right)
$$

**Step 3: 校正**
$$
\begin{equation}
\begin{aligned}
\mathbf{u}_{k+1} &= \tilde{\mathbf{u}}_{k+1} + \ddot{\mathbf{u}}_{k+1} \beta \Delta t^2 \\
\dot{\mathbf{u}}_{k+1} &= \dot{\tilde{\mathbf{u}}}_{k+1} + \ddot{\mathbf{u}}_{k+1} \gamma \Delta t
\end{aligned}
\end{equation}
$$

其中
$$
\begin{aligned}
    \beta& = 0 : \text{explicit algorithm}\\
    \beta& \neq 0 : \text{implicit algorithm} \rightarrow \text{inversion of } \mathbf{K}
\end{aligned}
$$

## 弹塑性问题

对于弹塑性问题，$\mathbf{F}^{\text{int}}_{k+1}$ 是非线性的，因此需要使用 Newton-Raphson 法迭代计算，将式 {eq}`intro-eq:equations` 记为

$$
\begin{equation}
\begin{cases}
\mathbf{M} \ddot{\mathbf{u}}_{k+1} + \mathbf{C} \dot{\mathbf{u}}_{k+1} + \mathbf{F}^{\text{int}}(\mathbf{u}_{k+1}) = \mathbf{F}^{\text{ext}}_{k+1} \\
\mathbf{u}(t_0) = \mathbf{u}_0, \quad \dot{\mathbf{u}}(t_0) = \dot{\mathbf{u}}_0
\end{cases}
\end{equation}
$$

代入插值公式，得到

$$
\mathbf{M}{\color{red}\ddot{\mathbf{u}}_{k+1}} + \mathbf{C}\cdot(\dot{\tilde{\mathbf{u}}}_{k+1} + {\color{red}\ddot{\mathbf{u}}_{k+1}} \gamma \Delta t) + \mathbf{F}^{\text{int}}(\tilde{\mathbf{u}}_{k+1} + {\color{red}\ddot{\mathbf{u}}_{k+1}} \beta \Delta t^2) = \mathbf{F}^{\text{ext}}_{k+1}
$$

其中，**质量项**

$$
\begin{equation}
\frac{\partial }{\partial \ddot{\mathbf{u}}_{k+1}}\left(\mathbf{M}\ddot{\mathbf{u}}_{k+1}\right) = \mathbf{M},
\end{equation}
$$

**阻尼项**

$$
\begin{equation}
\begin{aligned}
\frac{\partial }{\partial \ddot{\mathbf{u}}_{k+1}}\left(\mathbf{C}\cdot(\dot{\tilde{\mathbf{u}}}_{k+1} + \ddot{\mathbf{u}}_{k+1} \gamma \Delta t)\right)=\mathbf{C}\gamma\Delta t,
\end{aligned}
\end{equation}
$$

**内力项**

算法流程如下

1. $\ddot{\mathbf{u}}_{k+1} \leftarrow 0$
2. $\mathbf{u}_{k+1} \leftarrow \mathbf{u}_k + \dot{\mathbf{u}}_k \Delta t + \ddot{\mathbf{u}}_k \left(\frac{1}{2} - \beta \right) \Delta t^2 + \ddot{\mathbf{u}}_{k+1} \beta \Delta t^2$
3. $\dot{\mathbf{u}}_{k+1} \leftarrow \dot{\mathbf{u}}_k + \ddot{\mathbf{u}}_k (1-\gamma)\Delta t + \ddot{\mathbf{u}}_{k+1} \gamma \Delta t$
4. &nbsp;$\varepsilon \leftarrow \mathbf{f}(t_{k+1}) - \mathbf{r}(\mathbf{u}_{k+1}, \dot{\mathbf{u}}_{k+1}) - \mathbf{M}\ddot{\mathbf{u}}_{k+1}$
5. **while** $\|\varepsilon\| \geq \text{tol}$ **do**
6. &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $\Delta\ddot{\mathbf{u}}_{k+1} \leftarrow \left(\mathbf{M} + \mathbf{C}\gamma\Delta t + \mathbf{K}\beta\Delta t^2\right)^{-1} \varepsilon$
7. &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $\ddot{\mathbf{u}}_{k+1} \leftarrow \ddot{\mathbf{u}}_{k+1} + \Delta\ddot{\mathbf{u}}_{k+1}$
8. &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $\dot{\mathbf{u}}_{k+1} \leftarrow \dot{\mathbf{u}}_{k+1} + \Delta\ddot{\mathbf{u}}_{k+1} \gamma \Delta t$
9. &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $\mathbf{u}_{k+1} \leftarrow \mathbf{u}_{k+1} + \Delta\ddot{\mathbf{u}}_{k+1} \beta \Delta t^2$
10. &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $\varepsilon \leftarrow \mathbf{f}(t_{k+1}) - \mathbf{r}(\mathbf{u}_{k+1}, \dot{\mathbf{u}}_{k+1}) - \mathbf{M}\ddot{\mathbf{u}}_{k+1}$
11. **end while**