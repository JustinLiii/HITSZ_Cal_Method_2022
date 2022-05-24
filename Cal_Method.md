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
<br>
<br>

##### 2 范数
矩阵的2范数与向量不同（为保证从属）
$$
||A||_2 = \sqrt{\rho(A^HA)}
$$

其中 $\rho(A^HA)$ 为 $A^HA$ 的谱半径（最大特征值的绝对值）， $A^H$ 为A的共轭转置 
<br>
<br>

##### ∞范数（最大行和）
比较行和最大
<br>
<br>

##### F范数（平方和开平方）
<br>
<br>

#### 相关定理
##### 连续性定理（任意向量范数函数连续）
##### 范数等价定理（任意两个范数都 *同阶*）
##### 向量序列收敛于x 等价于 x_i - x的范数收敛于0
<br>
<br>


### Gauss消元法
#### 直接消元（消元，回代，求解）
总计算量约为
$$M \approx \frac{1}{3}n^3$$
<br>
<br>

#### Gauss-Jordan 消元法（只留下主元）
总计算量约为
$$M \approx \frac{1}{2}n^3$$
<br>
<br>

#### 列选主元素消元法（交换行获得这列最大的元素（列主元素）再消元）
<br>
<br>

#### 全主元素消元法（行列都比较得最大元素交换后消元）（会影响未知数顺序）

<br>
<br>

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
<br>
<br>

#### 三角分解（LU分解）
##### 若A为n阶方阵，且全部的顺序主子式不等于0，则LU分解唯一（L为单位下三角）
<br>
<br>

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
<br>
<br>

#### Crout分解方法
##### 将L单位下三角，U上三角换为L下三角，U单位上三角
##### 先算列，再算行
##### 书写时可写为 L_hat 和 U_hat
<br>
<br>

#### Cholesky分解方法 
##### 一般方法(平方根法)
###### A = LDD^-1U
###### 此方法需要开方，计算不方便
<br>
<br>

##### 改进方法（改进的平方根法）
###### A = LDU
###### 若A为正定矩阵，A=LDL^T = LL^^T
该方法的优点是不用选主元
<br>
<br>

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
<br>
<br>

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

<br>
<br>

### 线性方程组的迭代解法(x = Bx + k)
<br>
<br>

#### 分解矩阵Q=(I-B)A^-1：(I-B) = QA, k = Qb
##### 若分解矩阵Q使非奇异的，则称公式是相容的

<br>
<br>

#### 收敛性(以下三个命题等价—）
$\lim_{i \to \infty} B^i = 0$ 的充要条件为 $\rho(B) \lt 1$
##### x = Bx + k 收敛
##### rho(B) < 1
##### 至少存在一种从属范数|| · ||，使||B||<1
<br>
<br>

#### Jacobo迭代式
##### 分解为A=D+L+U, 迭代式为x = -D^-1 (L+U)x + D^-1b
$$x^{(i+1)} = -D^{-1}(L+U)x^{(i)} + D^{(-1)}b$$
$$B_J = -D^{-1}(L+U) = I - D^{-1}A$$
<br>
<br>

#### Gauss-Seidel迭代
##### 思想：基于Jacobi迭代，利用前次计算的i+1数值
##### x = -(D+L)^-1 Ux + (D+L)^-1 b
$$x^{(i+1)} = -(D+L)^{-1}Ux^{(i)} + (D+L)^{-1}b$$
$$B_G = -(D+L)^{-1}U$$
<br>
<br>

#### 超松弛迭代法（SOR）
##### 基于G-S法，但是提出x_i并给修正项乘以系数omega
$$x^{(i+1)} = -(D+\omega L)^{-1}[(1-\omega)D - \omega U]x^{(i)} + \omega(D+\omega L)^{-1}b$$
$$x_j^{(i+1)} = x_j^{(i)} + \frac{\omega}{a_{jj}}(b_j - \sum_{m=1}^{j-1}a_{jm}x_m^{(i+1)}-\sum_{(m=j)}^{n}a_{jm}x_m^{(i+1)})$$
<br>
<br>

## 插值法与数值逼近
### Lagrange插值多项式
#### 在（n+1）个点上满足插值条件式的多项式是唯一的
##### （次数不超过n）
##### （可用n次多项式零点的数量证明）
插值条件
$$y(x_i) = f(x_i)$$
要求
$$
l_j(x_i) =
    \begin{cases}
        0, \ i \neq j, \\
        1, \ i = j,
    \end{cases} , \ \ j,=0,1,\cdots,n.
$$
<br>
<br>

#### 插值多项式的形式
$$
l_j(x) = \frac{(x-x_0)(x-x_1)\cdots(x-x_{j-1})(x-x_{j+1})\cdots (x-x_n)}{(x_j-x_0)(x_j-x_1)\cdots(x_j-x_{j-1})(x_j-x_{j+1})\cdots(x_j-x_n)}
$$
<br>
<br>

#### 线性插值（2点，n=1）
#### 多项式插值（二次/抛物插值）（2点，n=2）
<br>
<br>

#### 插值函数的余项
##### 满足[a,b]上存在n阶连续导数，(a,b)上存在n+1阶导数
$$
E(x) = \frac{f^{(n+1)(\xi)}}{(n+1)!}p_{n+1}(x)
$$
其中
$$
p_{n+1}(x) = (x-x_0)(x-x_1)\cdots(x-x_n)
$$
##### 余项表达式是n+1次导数，故对n次以下原函数f(x)，插值函数l(x)恒等于f(x)
<br>
<br>

### Newton插值
#### 差商
##### 差商与x0 x1 x2 ... xn的排列顺序无关
$$
f[x_0 \ x_k] = \frac{f_k - f_0}{x_k - x_0} \\
f[x_0 \ x_1 \ \cdots \ x_{k-1} \ x_k] = \frac{f[x_0 \ x_1 \ \cdots \ x_{k-2} \ x_k] - f[x_0 \ x_1 \ \cdots \ x_{k-1}]}{x_k - x_{k-1}}
$$
可以认为，要获得包括$x_a,x_b$的差商，需要一个只包含$x_a$的差商和一个只包含$x_b$的差商（其他x相同）做计算
<br>
<br>

#### Newton插值公式
##### 升幂形式排列
$$
y(x) = a_0 + a_i(x-x_0) + a_2(x-x_0)(x-x_1) + \cdots + a_n(x-x_0)(x-x_1)\cdots(x-x_{n-1})\\
a_k = f[x_0 \ x_1 \ \cdots \ x_k]
$$
<br>
<br>

#### 余项
##### 由多项式唯一性，Newton和lagrange多项式等价，余项也等价
##### 故有差商和导数的关系（见正文）
##### 同样地，k阶差商近似某个常数，k+1阶差商近似为0时，可以近似地认为插值式N(x)恒等于f(x)
$$
E(x) = f[x_0x_1\cdots x_n x]p_{n+1}(x)
$$
故可以得到差商与导数的关系
$$
f[x_0x_1 \cdots x_j] = \frac{f^{(j)}(\xi_j)}{(n+1)!}
$$
##### 使用差商可以估计n+1阶导数不存在时插值多项式的余项
<br>
<br>

### 插值公式的运用及其收敛性与数值计算稳定性
#### 龙格（Runge）现象
![龙格现象示意图](/image/p1.png)
过高的次数可能降低精度
<br>
<br>

### 最佳平方逼近
#### 正交多项式
##### 权函数rho(x)
###### 非负
###### 在[a,b]上与多项式相乘可积分
###### 在[a,b]上与函数相乘积分为0，等价于函数恒等于0
<br>
<br>

##### 函数在[a,b]上的内积(f,g)
$$
(f,g) = \int_a^b \rho(x)f(x)g(x)dx
$$
<br>
<br>

##### 当(f,g) = 0时，两函数在[a,b]上带权rho(x)正交，记为$f \perp g$
<br>

##### 当函数序列在[a,b]上带权rho(x)两两正交时，称这些函数为[a,b]上带权rho(x)的正交函数族
<br>

##### 当最高项系数为1时，正交多项式序列是唯一的
递推式
$$
\varphi_{n+1}(x) = (x-a_n)\varphi_n(x) - \beta_n\varphi_{n-1}(x)
$$
其中
$$
\varphi_0(x) = 1,\varphi_{-1}(x) = 0 \\
a_n=\frac{(x\varphi_n,\varphi_n)}{(\varphi_n,\varphi_n)}\\
\beta_n = \frac{(\varphi_n,\varphi_n)}{(\varphi_{n-1},\varphi_{n-1})}
$$

##### 正交多项式序列的n个根都是单重实根，且都在区间(a,b)内
<br>
<br>

#### 常见正交多项式
##### Legrendre 多项式
区间[-1,1],$\rho(x) = 1$
$$
P_0(x) = 1 \\
P_n(x) = \frac{1}{2^nn!}\frac{d^n}{dx^n}\{(x^2-1)^n\}
$$
<br>

$$
(n+1)P_{n+1}(x) =(2n+1)xP_n(x) -nP_{n-1}(x)
$$

奇偶性：
$$
P_n(-x) = (-1)^nP_n(x)
$$

首项系数
$$
A_n = \frac{(2n)!}{2^n(n!)^2}
$$
<br>
<br>

##### Chebyshev多项式
在区间[-1,1]上，$\rho(x) = \frac{1}{\sqrt{1-x^2}}$
$$
T_n(x) = cos(n \ arccos \ x) \\
$$
<br>

$$
T_{n+1}(x) = 2xT_n(x) - T_{n-1}(x) \\
T_0(x) = 1, T_1(x) = x
$$

奇偶性：
$$
T_n(-x) = (-1)^nT_n(x)
$$
$$
A_n = 2^{n-1},A_0=1
$$
<br>
<br>

##### 第二类Chebyshev多项式
在区间[-1,1]上，带权函数$\rho(x)=\sqrt{1-x^2}$

$$
s_n = \frac{sin[(n+1)arccosx]}{\sqrt{1-x^2}}
$$
或
$$
x = cos\theta \\
s_n(x) = \frac{sin(n+1)\theta}{sin\theta}
$$
递推式
$$
s_{n+1}(x)=2xs_n(x)-s_{n-1}(x) \\
s_0(x) = 1, s_1(x) = 2x
$$
<br>
<br>

##### Laguerre多项式
在区间$[0,+\infty],\rho(x) = e^{-x}$
表达式
$$
L_n(x) = e^x\frac{d^n}{dx^n}(x^ne^{-x})
$$
递推公式
$$
L_{n+1}(x) = (2n+1-x)L_n(x)-n^2L_{n-1}(x)
$$
<br>
<br>

##### Hermite 多项式
在区间$(-\infty,+\infty), \rho(x) = e^{-x^2}$
表达式
$$
H_n(x) = (-1)^ne^{x^2}\frac{d^n}{dx^n}e^{-x^2}
$$
递推公式
$$
H_{n+1}(x) = 2xH_n(x)-2nH_{n-1}(x) \\
H_0(x) = 1, H_1(x) = 2x
$$
<br>
<br>

#### 最佳平方逼近问题及其解法
寻求线性无关函数集的线性组合
$$
\varphi(x) = \sum_{j=1}^{n}a_j\varphi_j(x)
$$
使
$$
||f-\varphi||_2^2 \overset{def}{=}\int_a^b\rho(x)[f(x)-\varphi(x)]^2dx
$$
最小

最佳平方逼近函数
$$
\begin{align*}
    \varphi^* &= \argmin_{\varphi} ||f-\varphi||_2^2 \\
    &= a_0^* + a_1^*x + \cdots + a_n^*x^n
\end{align*}
$$
##### 可通过方程组求解
$$
\begin{pmatrix}
    (\varphi_0,\varphi_0) & (\varphi_1,\varphi_0) & \cdots & (\varphi_n,\varphi_0)\\
    (\varphi_0,\varphi_1) & (\varphi_1, \varphi_1) & & \vdots\\
    \vdots & & \ddots \\
    (\varphi_0, \varphi_n)& \cdots& & (\varphi_n, \varphi_n)
\end{pmatrix}
\begin{pmatrix}
    a_0 \\ a_1 \\ \vdots \\ a_n
\end{pmatrix}
=
\begin{pmatrix}
    (f,\varphi_0) \\ (f,\varphi_1) \\ \vdots \\ (f,\varphi_n)
\end{pmatrix}
$$

##### Hilbert矩阵
当选用的线性无关组为
$$
\Phi = M_n = Span\{1,x,\cdots,x^n\}
$$
对应的方程组的系数矩阵为Hilbert矩阵
$$
\begin{bmatrix}
    1 & 1/2 & \cdots & 1/(n+1) \\
    1/2 & 1/3 \cdots & 1/(n+2) \\
    \vdots & \vdots & \ddots & \vdots \\
    1/(n+1) & 1/(n+2) & \cdots & 1/(2n+1)
\end{bmatrix}
$$
<br>

##### 用正交函数族做平方逼近
$$
a_k^* = \frac{(f,\varphi_k)}{(\varphi_k,\varphi_k)} = \frac{(f,\varphi_k)}{||\varphi_k||_2^2}
$$
$$
\varphi^*(x) = \sum_{k=0}^n \frac{(f,\varphi_k)}{||\varphi_k||_2^2} \varphi_k(x)
$$
该式子又称广义Fourier展开，系数$a_k^*$称为广义Fourier系数
<br>
<br>

## 数值积分
### 机械求积公式
$$
Q(f) = \sum_{j=0}^nH_jf(x_j)
$$
其中 $x_j$ 成为求积节点

一般来说， $H_j$ 只依赖于 $x_j$ 的选取
#### 求积公式的阶r —— 对次数不超过r的多项式均能精确成立，对r+1次的多项式至少有一个不能精确成立
<br>

#### 开型求积公式、闭型求积公式、半开半闭
<br>

#### 对n+1个求积节点，总存在系数H0到Hn使求积公式至少具有n次代数精度
<br>
<br>

### 插值求积公式（属于机械求积公式）
$$
H_j = \int_a^bl_j(x)dx
$$

### 等距节点的Newton-Cotes公式
将区间划分为 $n$ 等分，步长为 $h = \frac{b-a}{n}$
$$
x_i = a+ ih
$$
$$
H_j = \int_a^b l_j(x)dx = \frac{(-1)^{n-j}h}{j!(n-j)!}\int_0^n \prod\limits_{i = 0 \atop i \neq j}^n(t-i)dt
$$
令
$$
C_j(f) = \frac{H_j}{b-a}
$$
称 $C_j$ 为Cotes系数

求积公式可改写为
$$
Q_n(f) = (b-a)\sum_{j=0}^nC_jf(x_j)
$$
或
$$
\int_a^bf(x)dx = Ah\sum_{j=0}^nW_jf(x_j) + E(f)
$$
其中
$$
H_j = W_jAh, C_j = \frac{W_jA}{n}
$$
<br>

#### 梯形公式 (n = 1)
$$
Q_1(f) = \frac{b-a}{2}[f(a) + f(b)]
$$
#### Simpson公式（抛物线公式） (n = 2)
$$
Q_2(f) = \frac{b-a}{6}[f(a) + 4f(\frac{a+b}{2}) + f(b)]
$$
#### Cotes公式 (n = 4)
$$
Q_4(f) = \frac{2h}{45}[7f(a)+ 32f(a+h) + 12f(a+2h) + 32f(a+3h) + 7f(b)]
$$
#### 开型N-C公式
n = 2时（中点公式）
$$
\int_a^b f(x)dx = (b-a)f(\frac{a+b}{2})+\frac{1}{24}(b-a)^3f''(\xi)
$$