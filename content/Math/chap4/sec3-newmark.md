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

其中，$\beta$ 和 $\gamma$ 是积分算法的参数，下面给出了一些重要的特例

- $\beta = 0,\gamma = \frac{1}{2}$：中心差分方法，$\Delta t_{cr} = \frac{2}{\omega}$
- $\beta = \frac{1}{4}, \gamma = \frac{1}{2}$：梯形法则，具有常平均加速，无条件稳定
- $\gamma = \frac{1}{2}, \beta = \frac{1}{6}$：具有线性加速，$\Delta t_{cr} = \frac{3.464}{\omega}$
- $\beta\geq\frac{\gamma}{2}\geq\frac{1}{4}$：无条件稳定

此外，当 $\beta=0$ 时，是显式方法，$\beta > 0$ 时，为隐式方法；$\gamma$ 控制了人工粘度，在计算中引入了阻尼，被用来抑制解中的噪声，当 $\gamma = \frac{1}{2}$ 时，没有阻尼，当 $\gamma>\frac{1}{2}$ 时，人造阻尼正比于 $\gamma - \frac{1}{2}$，

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

## 加速度形式

加速度形式的主求解变量是加速度，即先求解加速度，再求解速度和位移
，将插值公式代入到 {eq}`intro-eq:equations`，得到

$$
\begin{equation}
\mathbf{M}{\color{red}\ddot{\mathbf{u}}_{k+1}} + \mathbf{C}(\dot{\tilde{\mathbf{u}}}_{k+1} + {\color{red}\ddot{\mathbf{u}}_{k+1}} \gamma \Delta t) + \mathbf{F}^{\text{int}}_{k+1} = \mathbf{F}^{\text{ext}}_{k+1}
\end{equation}
$$ (intro-eq:equations-1)

### 线弹性问题

对于线弹性问题，有

$$
\begin{equation}
\mathbf{F}^{\text{int}} =\int_{E}\mathbf{B}^{T}\mathbb{C}\mathbf{B}\ \mathbf{d}E\cdot\mathbf{u}=\mathbf{K}\mathbf{u},
\end{equation}
$$

其中 $\mathbf{K}$ 是常量，于是，式 {eq}`intro-eq:equations-1` 可以写为

$$
\mathbf{M}{\color{red}\ddot{\mathbf{u}}_{k+1}} + \mathbf{C}(\dot{\tilde{\mathbf{u}}}_{k+1} + {\color{red}\ddot{\mathbf{u}}_{k+1}} \gamma \Delta t) + \mathbf{K}(\tilde{\mathbf{u}}_{k+1} + {\color{red}\ddot{\mathbf{u}}_{k+1}} \beta \Delta t^2) = \mathbf{F}^{\text{ext}}_{k+1}
$$

该方程关于 $\ddot{\mathbf{u}}_{k+1}$ 是线性的

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
\begin{equation}
\begin{aligned}
\ddot{\mathbf{u}}_{k+1} &= \left( \mathbf{M} + \mathbf{C} \gamma \Delta t + \mathbf{K} \beta \Delta t^2 \right)^{-1}
\left( \mathbf{F}^{\text{ext}}_{k+1} - \mathbf{K} \tilde{\mathbf{u}}_{k+1} - \mathbf{C} \dot{\tilde{\mathbf{u}}}_{k+1} \right)\\
&=\left( \mathbf{M} + \mathbf{C} \gamma \Delta t + \mathbf{K} \beta \Delta t^2 \right)^{-1}
\left( \mathbf{F}^{\text{ext}}_{k+1} - \mathbf{F}^{\text{int}}(\tilde{\mathbf{u}}_{k+1}) - \mathbf{C} \dot{\tilde{\mathbf{u}}}_{k+1} \right)
\end{aligned}
\end{equation}
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
    \beta& \neq 0 : \text{implicit algorithm}
\end{aligned}
$$

### 弹塑性问题

对于弹塑性问题，将式 {eq}`intro-eq:equations` 记为

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

**若 $\beta = 0$，则 $\mathbf{F}^{\text{int}}\equiv\mathbf{F}^{\text{int}}(\tilde{\mathbf{u}}_{k+1})$ 是常量，因此方程关于 $\ddot{\mathbf{u}}_{k+1}$ 仍然是线性的，求解流程同上；而当 $\beta>0$ 时，方程关于 $\ddot{\mathbf{u}}_{k+1}$ 是非线性的，需要进行非线性迭代，求解流程如下。因此，$\beta$ 既决定了方程了显/隐性，又决定了方程的线性/非线性：$\beta=0$，显式/线性；$\beta>0$，隐式/非线性**

此时，Jacobia 矩阵的各项计算如下

**质量项**

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

$$
\begin{equation}
\begin{aligned}
\frac{\partial }{\partial \ddot{\mathbf{u}}_{k+1}}\mathbf{F}^{\text{int}}(\tilde{\mathbf{u}}_{k+1} + \ddot{\mathbf{u}}_{k+1} \beta \Delta t^2) = \frac{\partial \mathbf{F}^{\text{int}}}{\partial \mathbf{u}_{k+1}}\frac{\partial \mathbf{u}_{k+1}}{\partial \ddot{\mathbf{u}}_{k+1}}=\mathbf{K}\beta \Delta t^{2},
\end{aligned}
\end{equation}
$$

$\mathbf{K}$ 是一致刚度矩阵

算法流程如下

1. $\ddot{\mathbf{u}}_{k+1} \leftarrow \ddot{\mathbf{u}}_{k}$
2. $\dot{\mathbf{u}}_{k+1} \leftarrow \dot{\mathbf{u}}_k + \ddot{\mathbf{u}}_k (1-\gamma)\Delta t + \ddot{\mathbf{u}}_{k+1} \gamma \Delta t$
3. $\mathbf{u}_{k+1} \leftarrow \mathbf{u}_k + \dot{\mathbf{u}}_k \Delta t + \ddot{\mathbf{u}}_k \left(\frac{1}{2} - \beta \right) \Delta t^2 + \ddot{\mathbf{u}}_{k+1} \beta \Delta t^2$
4. &nbsp;$\varepsilon \leftarrow \mathbf{F}^{\text{ext}}_{k+1} - \mathbf{C} \dot{\mathbf{u}}_{k+1} - \mathbf{F}^{\text{int}}_{k+1} - \mathbf{M}\ddot{\mathbf{u}}_{k+1}$
5. **while** $\|\varepsilon\| \geq \text{tol}$ **do**
6. &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $\Delta\ddot{\mathbf{u}}_{k+1} \leftarrow \left(\mathbf{M} + \mathbf{C}\gamma\Delta t + \mathbf{K}\beta\Delta t^2\right)^{-1} \varepsilon$
7. &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $\ddot{\mathbf{u}}_{k+1} \leftarrow \ddot{\mathbf{u}}_{k+1} + \Delta\ddot{\mathbf{u}}_{k+1}$
8. &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $\dot{\mathbf{u}}_{k+1} \leftarrow \dot{\mathbf{u}}_{k+1} + \Delta\ddot{\mathbf{u}}_{k+1} \gamma \Delta t$
9. &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $\mathbf{u}_{k+1} \leftarrow \mathbf{u}_{k+1} + \Delta\ddot{\mathbf{u}}_{k+1} \beta \Delta t^2$
10. &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $\varepsilon \leftarrow \mathbf{F}^{\text{ext}}_{k+1} - \mathbf{C} \dot{\mathbf{u}}_{k+1} - \mathbf{F}^{\text{int}}_{k+1} - \mathbf{M}\ddot{\mathbf{u}}_{k+1}$
11. **end while**

**对于隐式方法，一般使用位移形式，它对边界条件的处理更加自然**

## 位移形式

位移形式以位移作为主求解变量，即先求解位移，再求解速度和加速度，使用位移来表示速度和加速度项

$$
\begin{equation}
\begin{aligned}
\ddot{\mathbf{u}}_{k+1} &= \frac{\mathbf{u}_{k+1} - \tilde{\mathbf{u}}_{k+1}}{\beta \Delta t^2},\\
\dot{\mathbf{u}}_{k+1}&=\dot{\mathbf{u}}_k + \ddot{\mathbf{u}}_k (1 - \gamma) \Delta t + \frac{\mathbf{u}_{k+1} - \tilde{\mathbf{u}}_{k+1}}{\beta \Delta t} \gamma
\end{aligned}
\end{equation}
$$



此时，方程 {eq}`intro-eq:equations` 写为

$$
\mathbf{M}\frac{{\color{red}\mathbf{u}_{k+1}} - \tilde{\mathbf{u}}_{k+1}}{\beta \Delta t^2} + \mathbf{C}\cdot(\dot{\mathbf{u}}_k + \ddot{\mathbf{u}}_k (1 - \gamma) \Delta t + \frac{{\color{red}\mathbf{u}_{k+1}} - \tilde{\mathbf{u}}_{k+1}}{\beta \Delta t} \gamma) + \mathbf{F}^{\text{int}}({\color{red}\mathbf{u}_{k+1}}) = \mathbf{F}^{\text{ext}}_{k+1}
$$

**注意到，上述形式中必须有 $\beta>0$，因此位移形式总是隐式求解的,而方程的线性/非线性由问题的自身特性决定（例如，$\mathbf{F}^{\text{int}}$）**

对于线弹性问题，$\mathbf{F}^{\text{int}}_{k+1} = \mathbf{K}\mathbf{u}_{k+1}$，因此上述方程是关于 $\mathbf{u}_{k+1}$ 的线性方程，不需要牛顿迭代；而对于弹塑性问题，上述方程是非线性的，需要牛顿迭代

此时，Jacobia 矩阵的各项计算如下

**质量项**

$$
\begin{equation}
\frac{\partial }{\partial \mathbf{u}_{k+1}}\left(\cdot\right) = \frac{\mathbf{M}}{\beta \Delta t^2},
\end{equation}
$$

**阻尼项**

$$
\begin{equation}
\begin{aligned}
\frac{\partial }{\partial \mathbf{u}_{k+1}}\left(\cdot\right)=\mathbf{C}\frac{\gamma}{\beta\Delta t},
\end{aligned}
\end{equation}
$$

**内力项**

$$
\begin{equation}
\begin{aligned}
\frac{\partial }{\partial \mathbf{u}_{k+1}}\mathbf{F}^{\text{int}}(\mathbf{u}_{k+1})=\mathbf{K},
\end{aligned}
\end{equation}
$$

$\mathbf{K}$ 是一致刚度矩阵

算法流程如下

1. $\tilde{\mathbf{u}}_{k+1} \leftarrow \mathbf{u}_k + \dot{\mathbf{u}}_k \Delta t + \ddot{\mathbf{u}}_k ( \frac{1}{2} - \beta ) \Delta t^2 $
2. $\dot{\tilde{\mathbf{u}}}_{k+1} = \dot{\mathbf{u}}_k + \ddot{\mathbf{u}}_k (1 - \gamma) \Delta t$
3. $\mathbf{u}_{k+1}=\mathbf{u}_{k},\dot{\mathbf{u}}_{k+1}=\dot{\mathbf{u}}_{k},\ddot{\mathbf{u}}_{k+1}=\ddot{\mathbf{u}}_{k},$
4. &nbsp;$\varepsilon \leftarrow \mathbf{F}^{\text{ext}}_{k+1} - \mathbf{C} \dot{\mathbf{u}}_{k+1} - \mathbf{F}^{\text{int}}_{k+1} - \mathbf{M}\ddot{\mathbf{u}}_{k+1}$
5. **while** $\|\varepsilon\| \geq \text{tol}$ **do**
6. &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $\Delta\mathbf{u}_{k+1} \leftarrow \left(\frac{\mathbf{M}}{\beta \Delta t^2} + \mathbf{C}\frac{\gamma}{\beta\Delta t} + \mathbf{K}\right)^{-1} \varepsilon$
7. &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $\mathbf{u}_{k+1} \leftarrow \mathbf{u}_{k+1} + \Delta\mathbf{u}_{k+1}$
8. &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $\ddot{\mathbf{u}}_{k+1} \leftarrow \frac{\mathbf{u}_{k+1} - \tilde{\mathbf{u}}_{k+1}}{\beta \Delta t^2}$
9. &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $\dot{\mathbf{u}}_{k+1} \leftarrow \dot{\tilde{\mathbf{u}}}_{k+1} + \ddot{\mathbf{u}}_{k+1} \gamma \Delta t$
10. &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; $\varepsilon \leftarrow \mathbf{F}^{\text{ext}}_{k+1} - \mathbf{C} \dot{\mathbf{u}}_{k+1} - \mathbf{F}^{\text{int}}_{k+1} - \mathbf{M}\ddot{\mathbf{u}}_{k+1}$
11. **end while**