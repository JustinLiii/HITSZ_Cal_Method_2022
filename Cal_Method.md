#  计算方法
## 非线性方程迭代法求根
### 收敛阶
$$
\begin{align*}
    \lim_{i \to \infty} \frac{|\varepsilon_{i+1}|}{|\varepsilon_i|^p} = c \neq 0
\end{align*}
$$
$p = 1$时为线性收敛，$p \gt 1$时为超线性收敛，$p = 2$时为二次收敛<br>
<br>

### 二分法
$$
\begin{align*}
    x_{i+1} &= \frac{b-a}{2} \\
    ab &\lt 0 
\end{align*}
$$
<br>
<br>

### 单点迭代法
$$
\begin{align*}
    f(x) &= 0 \\
    \Rightarrow x &= \varphi(x)\\
    \Rightarrow x_{i+1} &= \varphi(x_i)    
\end{align*}
$$
要求
$$
|\varphi(x_1) - \varphi(x_2)| \leq L|x_1 - x_2|, \ \ \ \ \ \ L \lt 1
$$
有误差估计式
$$
\begin{align*}
    |\alpha - x_i| &\leq \frac{1}{1-L}|x_{i+1} - x_i| \\
    |\alpha - x_i| &\leq \frac{L^i}{1-L}|x_1 = x_0| 
\end{align*}
$$
实际计算中，由于 $L$ 不易求得，可以用 $|x_{i+1} - x_i| \lt \varepsilon$ 作为结束迭代的条件，注意此时不能有 $L \approx 1$
单点迭代收敛阶为 $p$ 的充要条件为
$$ \varphi^{(j)}(x) = 0, \ \ j = 1,2,\cdots,p-1$$
$$ \varphi^{(p)}(\alpha) \neq 0$$
通过在 $\alpha$ 附近做 $\varphi(x)$ 的泰勒展开来证明
<br>
<br>

### 牛顿法
#### 牛顿法
通过反函数泰勒展开构造
$$x_{i+1} = x_i - \frac{f(x)}{f'(x)}$$
收敛阶 $p = 2$
$$\lim_{i \to \infty}\frac{|\varepsilon_{i+1}|}{|\varepsilon_i|^2} = \frac{|f''(\alpha)|}{2|f'(\alpha)|}$$
要求
$$
\begin{align}
    f(a)f(b) \lt 0& \\
    f'(x) \neq 0&, \ \ x \in [a,b] \\
    f''(x)不变号&,  \ \ x \in [a,b] \\
    x_0 \in [a,b]&,  \ \ f''(x_0)f(x_0) \ge 0
\end{align}
$$
式（1）保证有根，式（2）保证函数单调，式（3）保证凹凸向不变，式（4）保证迭代不会到[a,b]外面
<br>
<br>
#### 简化牛顿法
$$x_{i+1} = x_i - \frac{f(x)}{C} $$
收敛阶为一阶
<br>
<br>
#### 牛顿下山法
$$x_{i+1} = x_i - \lambda\frac{f(x)}{f'(x)}$$
其中 $\lambda$ 为下山因子，这是因为实际计算时，其选择应使
$$|f(x_{i+1})|\lt|f(x_i)|$$
保证迭代过程不超出[a,b]，放宽初值的选择范围<br>
$\varphi'(x) = 1-\lambda$, 当 $\lambda \neq 1$ 时，一阶收敛
<br>
<br>

### 多点迭代法
<br>

#### <b>割线法</b>
<br>
<br>

将牛顿法公式中的导数用 $(f(x_i) - f(x_{i-1})/(x_i - x_{i-1}))$ 代替，即
$$x_{i+1} = x_i - \frac{x_i - x_{i-1}}{f(x_i)-f(x_{i-1})}f(x_i) $$或
$$x_{i+1} = \frac{f(x_i)}{f(x_i) - f(x_{i-1})}x_{i-1} + \frac{f(x_{i-1})}{f(x_{i-1}) - f(x_i)}x_i$$
收敛阶为
$$p = \frac{1+\sqrt{5}}{2}$$
$$\lim_{i \to \infty}\frac{|\varepsilon_{i+1}|}{|\varepsilon_i|^2} = |\frac{f''(\alpha)}{2f'(\alpha)}|^{p-1}$$
此方法可不用计算函数的导数值，实际计算是可以基于计算导数的复杂的在牛顿法和此割线发之间权衡
<br>
<br>
#### <b>虚位法/试位法</b>
<br>
<br>

割线法仅具有局部收敛性，在实际计算过程中若初值选得不好，可能不收敛。故在每次迭代前，先判断出新的有根区间再代入割线法计算，成为虚位法。

也可以认为是将二分法的等分点换成割线的零点

当函数为凸函数时，每次选择区间的一个端点都是 $x_1$，为单点定常迭代，收敛阶 $p = 1$。由于几乎所有函数在根附近都是凹或凸函数，所以虚位法几乎对所有函数都是线性收敛的

### 重根上的迭代法
<br>
#### <b> 重数 r 已知时的重根上的迭代法 </b>
<br>
<br>

虽然有重根时建立在反函数上的推导无效，但牛顿法仍然可以被证明是线性收敛的

可以证明（通过泰勒展开牛顿法分子分母，代入$\varphi'(\alpha) = \lim_{x \to \alpha} \frac{\varphi(x) - \varphi(\alpha)}{x-\alpha}$）
$$\varphi'(\alpha) = 1-\frac{1}{r}$$

可以对其进行修正
$$x_{i+1} = x_i - r\frac{f(x)}{f'(x)}$$
使方法对 $r$ 重根二阶收敛
<br>
<br>
#### <b>未知根的重数时的迭代法</b>
<br>
<br>

迭代式可修正为
$$
x_{i+1} = x_i - \frac{u(x_i)}{u'(x_i)}
$$
其中
$$u(x) = \frac{f(x)}{f'(x)} = \frac{1}{r}\frac{f^{(r)}(\xi_1)}{f^{(r)}(\xi_2)}(x-\alpha)$$
$u(x)$ 的零点符合 $x = \alpha$，也就是 $f(x)$ 的零点

对其他方法，也可将求 $f(x)$ 的零点转化为求 $u(x)$ 的零点，但由于需要计算一阶导数，计算效率可能不高，且 $f'(x)$ 可能不连续

## 线性方程组数值解

### 范数

#### 条件
##### 非负
##### 齐次
$$||\alpha x|| = |\alpha| ||x||$$
##### 三角不等式
##### 乘法不等式（矩阵）

#### 范数的相容性
$$||AX|| \leq ||A|| ||x||$$
#### 从属范数

#### 向量范数

##### 1 范数
##### 2 范数
##### n 范数
##### ∞范数

#### 矩阵范数
##### 1 范数（最大列和）
比较列和最大
##### 2 范数
矩阵的2范数与向量不同（为保证从属）
$$
||A||_2 = \sqrt{\rho(A^HA)}
$$

其中 $\rho(A^HA)$ 为 $A^HA$ 的谱半径（最大特征值的绝对值）， $A^H$ 为A的共轭转置 
##### ∞范数（最大行和）
比较行和最大
##### F范数（平方和开平方）

#### 相关定理
##### 连续性定理（任意向量范数函数连续）
##### 范数等价定理（任意两个范数都 *同阶*）
##### 向量序列收敛于x 等价于 x_i - x的范数收敛于0


### Gauss消元法
#### 直接消元（消元，回代，求解）
总计算量约为
$$M \approx \frac{1}{3}n^3$$

#### Gauss-Jordan 消元法（只留下主元）
总计算量约为
$$M \approx \frac{1}{2}n^3$$

#### 列选主元素消元法（交换行获得这列最大的元素（列主元素）再消元）

#### 全主元素消元法（行列都比较得最大元素交换后消元）（会影响未知数顺序）


### 三角分解法
Gauss消元时相当于用一系列下三角阵与原矩阵相乘
$$
U = L_1^{-1}L_2^{-1} \dots L_{n-1}^{-1} A\\
A = LU
$$

$$
\begin{align*}
l_{ij} &= m_{ij} (i \gt j) \\
l_{kk} &= 1\\
l_{ij} &= 0 (i \lt j)
\end{align*}
$$
#### 三角分解（LU分解）
##### 若A为n阶方阵，且全部的顺序主子式不等于0，则LU分解唯一（L为单位下三角）

#### 三角分解法
##### 若不要求顺序主子式不为零，则可能需要交换行（排列矩阵P）PA = LU
此时原方程等价于$PAx = Pb$ 即 $LUx = Pb$
可顺序求解
$$
\begin{align*}
    Ly &= Pb \\ 
    Ux &= y
\end{align*}
$$

#### Doolittle 分解法
##### 本质上就是看LU = A的逐项式倒退如何计算各项
##### 先算行，再算列
##### 计算机处理时可将U矩阵的对角线元覆写在L矩阵对角线 1 的位置，节省空间
##### 不考虑交换

#### Crout分解方法
##### 将L单位下三角，U上三角换为L下三角，U单位上三角
##### 先算列，再算行
##### 书写时可写为 L_hat 和 U_hat

#### Cholesky分解方法 
##### 一般方法(平方根法)
###### A = LDD^-1U
###### 此方法需要开方，计算不方便
##### 改进方法（改进的平方根法）
###### A = LDU
###### 若A为正定矩阵，A=LDL^T = LL^^T
该方法的优点是不用选主元

#### 三对角方程组的追赶法
$$
\begin{pmatrix}
    b_1 & c_1 \\
    a_2 & b_2 & c_2\\
    & \ddots & \ddots & \ddots\\
    & & a_{n-1} & b_{n-1} & c_{n-1} \\
    & & & a_n & b_n
\end{pmatrix}
\\=
\begin{pmatrix}
    \alpha_1 \\
    \gamma_2 & \alpha_2 \\ 
    & \ddots & \ddots \\
    & & \gamma_n & \alpha_n
\end{pmatrix}
\begin{pmatrix}
    1 & \beta_1 \\
    & 1 & \beta_2 \\
    & & \ddots \ddots \\
    & & & 1 & \beta_{n-1} \\
    & & & & 1
\end{pmatrix}
$$
条件
$$
\begin{align*}
    \begin{cases}
        |b_1| \gt |c_1| \gt 0 \\
        |b_i| \geq |a_i| + |c_i| \\
        |b_n| \gt |a_n| \gt 0 
    \end{cases}    
\end{align*}
$$
分解法
$$
\begin{align*}
    \begin{cases}
        \gamma_i = a_i \\
        \alpha_1 = b_1 \\
        \alpha_i = b_i - a_i\beta_{i-1} \\
        \beta_i = c_i / (b_i - a_i\beta_{i-1})
    \end{cases}
\end{align*}
$$
##### 使用Crout方法分解
##### “追” beta1 -> beta2 ->...-> beta n
##### “追” y1 -> y2-> ... -> yn
##### “赶” x_n -> x_n-1 -> ... -> x2 -> x1

### 矩阵条件数和误差分析
#### 条件数
$$
Cond(A) = \begin{Vmatrix}
    A
\end{Vmatrix}
\begin{Vmatrix}
    A^{-1}
\end{Vmatrix}
$$
#### A精确，b有小扰动（条件数限制了相对误差的上界&下界）
$$A(x + \delta x) = b + \delta b$$
计算$\delta b$，取范数，得
$$\frac{||\delta x||}{||x||} \leq ||A||\cdot ||A^{-1}|| \cdot \frac{||\delta b||}{||b||} = Cond(A)\frac{||\delta b||}{||b||}$$
$$\frac{||\delta x||}{||x||} \geq \frac{1}{Cond(A)}\frac{||\delta b||}{||b||}$$
#### A有小扰动，b精确（条件数限制相对误差上界）
要分析，需要先假设$A+\delta A$是非奇异
需要条件 $||A^{-1}\delta A|| \lt 1$

或更强的条件$||A^{-1}|| \ ||\delta A|| \lt 1$

得到相对误差上界
$$
\begin{align*}
    \frac{||\delta x||}{x} &\leq \frac{||A|| \ ||A^{-1}|| \ ||\delta A||}{(1-||A^{-1}|| \ ||\delta A||) ||A||} \\ 
    &= \frac{Cond(A)\frac{||\delta A||}{||A||}}{1-Cond(A)\frac{||\delta A||}{||A||}}
\end{align*}
$$


### 线性方程组的迭代解法(x = Bx + k)
#### 分解矩阵Q=(I-B)A^-1：(I-B) = QA, k = Qb
##### 若分解矩阵Q使非奇异的，则称公式是相容的
#### 收敛性(以下三个命题等价—）
$\lim_{i \to \infty} B^i = 0$ 的充要条件为 $\rho(B) \lt 1$
##### x = Bx + k 收敛
##### rho(B) < 1
##### 至少存在一种从属范数|| · ||，使||B||<1

#### Jacobo迭代式
##### 分解为A=D+L+U, 迭代式为x = -D^-1 (L+U)x + D^-1b
$$x^{(i+1)} = -D^{-1}(L+U)x^{(i)} + D^{(-1)}b$$
$$B_J = -D^{-1}(L+U) = I - D^{-1}A$$

#### Gauss-Seidel迭代
##### 思想：基于Jacobi迭代，利用前次计算的i+1数值
##### x = -(D+L)^-1 Ux + (D+L)^-1 b
$$x^{(i+1)} = -(D+L)^{-1}Ux^{(i)} + (D+L)^{-1}b$$
$$B_G = -(D+L)^{-1}U$$

#### 超松弛迭代法（SOR）
##### 基于G-S法，但是提出x_i并给修正项乘以系数omega
$$x^{(i+1)} = -(D+\omega L)^{-1}[(1-\omega)D - \omega U]x^{(i)} + \omega(D+\omega L)^{-1}b$$
$$x_j^{(i+1)} = x_j^{(i)} + \frac{\omega}{a_{jj}}(b_j - \sum_{m=1}^{j-1}a_{jm}x_m^{(i+1)}-\sum_{(m=j)}^{n}a_{jm}x_m^{(i+1)})$$

## 插值法与数值逼近
### Lagrange插值多项式
#### 满足插值条件式的多项式是唯一的
插值条件
$$y(x_i) = f(x_i)$$