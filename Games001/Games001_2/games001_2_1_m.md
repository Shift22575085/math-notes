# 矩阵求导

### 分子布局：分母转置

$$\frac{\partial \boldsymbol{f}_{2\times1}(\boldsymbol{x})}{\partial \boldsymbol{x}^{T}_{3\times1}}
=
\begin{pmatrix}
\frac{\partial f_1}{\partial x_1} & \frac{\partial f_1}{\partial x_2} & \frac{\partial f_1}{\partial x_3} \\\\
\frac{\partial f_2}{\partial x_1} & \frac{\partial f_2}{\partial x_2} & \frac{\partial f_2}{\partial x_3}
\end{pmatrix}_{2\times3}$$

### 分母布局：分子转置

$$\frac{\partial \boldsymbol{f}^{T}_{2\times1}(\boldsymbol{x})}{\partial \boldsymbol{x}_{3\times1}}
=
\begin{pmatrix}
\frac{\partial f_1}{\partial x_1} & \frac{\partial f_2}{\partial x_1} \\\\
\frac{\partial f_1}{\partial x_2} & \frac{\partial f_2}{\partial x_2} \\\\
\frac{\partial f_1}{\partial x_3} & \frac{\partial f_2}{\partial x_3}
\end{pmatrix}_{3\times2}$$

## 雅可比矩阵

### 线性变化

变换后的笛卡尔坐标系的轴还是直线

$$L(a \vec{v}) = a L(\vec{v})$$

$$L(\vec{v} + \vec{w}) = L(\vec{v}) + L(\vec{w})$$

$$L\left(\begin{bmatrix} x \\\\ y \end{bmatrix}\right) = L\left(x \begin{bmatrix} 1 \\\\ 0 \end{bmatrix} + y \begin{bmatrix} 0 \\\\ 1 \end{bmatrix}\right)$$

### 多元函数的局部线性属性

$$f\left(\begin{bmatrix} x \\\\ y \end{bmatrix}\right) = \begin{bmatrix} x + \sin(y) \\\\ y + \sin(x) \end{bmatrix}$$

$$\begin{bmatrix} \pi/2 \\\\ 0 \end{bmatrix} = \begin{bmatrix} \pi/2 \\\\ 0 + \sin(\pi/2) \end{bmatrix}$$

将图像的某个点无限放大，会看到图像类似线性变换了，可以用其他函数表示

要找到的就是这种极小的局部如何表示的函数

### 雅可比矩阵
$$f\left(\begin{bmatrix} x \\\\ y \end{bmatrix}\right) = \begin{bmatrix} x + \sin(y) \\\\ y + \sin(x) \end{bmatrix}$$

$$J = \begin{bmatrix} 
\frac{\partial f_1}{\partial x} & \frac{\partial f_1}{\partial y} \\\\ 
\frac{\partial f_2}{\partial x} & \frac{\partial f_2}{\partial y} 
\end{bmatrix} = \begin{bmatrix} 
1 & \cos(y) \\\\ 
\cos(x) & 1 
\end{bmatrix}$$

$$J = \begin{bmatrix}
\frac{\partial f_1}{\partial x_1} & \cdots & \frac{\partial f_1}{\partial x_n} \\\\
\vdots & \ddots & \vdots \\\\
\frac{\partial f_m}{\partial x_1} & \cdots & \frac{\partial f_m}{\partial x_n}
\end{bmatrix}$$

*   **第一列** 

$$\begin{bmatrix} 1 \\\\ \cos(x) \end{bmatrix}$$

：表示在输入空间只沿着 x 方向走一小步，输出空间会怎么变。它的水平分量固定是 1，垂直分量取决于当前位置的 $\cos(x)$。
*   **第二列** 

$$\begin{bmatrix} \cos(y) \\\\ 1 \end{bmatrix}$$

：表示在输入空间只沿着 y 方向走一小步，输出空间会怎么变。它的垂直分量固定是 1，水平分量取决于当前位置的 $\cos(y)$。

### 雅可比矩阵行列式

和普通矩阵行列式相同，行列式代表矩阵变化后的空间或者平面的面积

# 向量变元的实值标量函数(梯度方向)

输入（列向量）：
$$x_{n \times 1} = (x_1, x_2, \dots, x_n)^T$$

求导结果（梯度，转置为列向量）：
$$\nabla_x f(x) = \left( \frac{\partial f}{\partial x_1}, \frac{\partial f}{\partial x_2}, \dots, \frac{\partial f}{\partial x_n} \right)^T$$

分子布局：分母转置

### 运算法则

常数：

函数结果为常数，求导结果为0

$$\frac{\partial c}{\partial \boldsymbol{x}} = \boldsymbol{0}_{n \times 1}$$

线性法则：

导数是一个线性算子：常数系数可以穿透求导符号，求导对加法满足分配律。

$$\frac{\partial [c_1 f(\boldsymbol{x}) + c_2 g(\boldsymbol{x})]}{\partial \boldsymbol{x}} = c_1 \frac{\partial f(\boldsymbol{x})}{\partial \boldsymbol{x}} + c_2 \frac{\partial g(\boldsymbol{x})}{\partial \boldsymbol{x}}$$

乘积法则：

左乘右导，右乘左导

$$\frac{\partial [f(\boldsymbol{x}) g(\boldsymbol{x})]}{\partial \boldsymbol{x}} = \frac{\partial f(\boldsymbol{x})}{\partial \boldsymbol{x}} g(\boldsymbol{x}) + f(\boldsymbol{x}) \frac{\partial g(\boldsymbol{x})}{\partial \boldsymbol{x}}$$

商法则：
$$\frac{\partial \left[\frac{f(\boldsymbol{x})}{g(\boldsymbol{x})}\right]}{\partial \boldsymbol{x}} = \frac{1}{g^2(\boldsymbol{x})} \left[ \frac{\partial f(\boldsymbol{x})}{\partial \boldsymbol{x}} g(\boldsymbol{x}) - f(\boldsymbol{x}) \frac{\partial g(\boldsymbol{x})}{\partial \boldsymbol{x}} \right]$$

**函数相除 （商法则）**

**第一步：写出增量后的表达式**
设原比值为 $q = \frac{f}{g}$。给 $x$ 一个微小增量 $\Delta x$，分子变为 $f+\Delta f$，分母变为 $g+\Delta g$。
$$q + \Delta q = \frac{f + \Delta f}{g + \Delta g}$$

**第二步：求增量 $\Delta q$**

用新结果减去老结果：
$$\Delta q = \frac{f + \Delta f}{g + \Delta g} - \frac{f}{g}$$

$$\Delta q = \frac{g(f + \Delta f) - f(g + \Delta g)}{g(g + \Delta g)}$$

$$\text{分子} = gf + g\Delta f - fg - f\Delta g = g\Delta f - f\Delta g$$

$$\Delta q = \frac{g\Delta f - f\Delta g}{g(g + \Delta g)}$$

**第三步：除以 $\Delta x$ 并令 $\Delta x \to 0$**
$$\frac{\Delta q}{\Delta x} = \frac{g \frac{\Delta f}{\Delta x} - f \frac{\Delta g}{\Delta x}}{g(g + \Delta g)}
\quad \longrightarrow \quad
q' = \frac{g f' - f g'}{g^2}$$

### 常用公式（分母布局）

**前提定义**：

$x$：变量列向量（$n \times 1$）
$a, b$：常数向量（$n \times 1$）
$A$：常数矩阵（$n \times n$）
所有求导结果都对齐成 $n \times 1$ 的列向量。

**一次型求导**：
$$\frac{\partial(x^Ta)}{\partial x} = \frac{\partial(a^Tx)}{\partial x} = a$$

等同于标量函数 $ax$ 求导得到常数 $a$。

$x_1a_1+x_1a_1$的求偏导就是$a$

**平方和求导**：
$$\frac{\partial(x^Tx)}{\partial x} = 2x$$

等同于标量函数 $x^2$ 求导得到 $2x$。

**二次型求导**：
$$\frac{\partial(x^TAx)}{\partial x} = Ax + A^Tx$$

套用乘积法则 $(x^TA) \cdot (x)$。如果 $A$ 是对称矩阵，简化为 $2Ax$。完全类比标量 $ax^2$ 求导得到 $2ax$。

**二次型求导例子**：
TODO：这个是事后验证，没有公式来源的推导

$$x=
\begin{pmatrix}
x_1\\\\
x_2
\end{pmatrix},
\qquad
A=
\begin{pmatrix}
1&2\\\\
3&4
\end{pmatrix}$$

求：

$$\frac{\partial(x^TAx)}{\partial x}$$

展开二次型

$$x^TAx
=
\begin{pmatrix}
x_1&x_2
\end{pmatrix}
\begin{pmatrix}
1&2\\\\
3&4
\end{pmatrix}
\begin{pmatrix}
x_1\\\\
x_2
\end{pmatrix}$$

$$\begin{pmatrix}
1&2\\\\
3&4
\end{pmatrix}
\begin{pmatrix}
x_1\\\\
x_2
\end{pmatrix}
=
\begin{pmatrix}
x_1+2x_2\\\\
3x_1+4x_2
\end{pmatrix}$$

$$\begin{pmatrix}
x_1&x_2
\end{pmatrix}
\begin{pmatrix}
x_1+2x_2\\\\
3x_1+4x_2
\end{pmatrix}
=
x_1^2+5x_1x_2+4x_2^2$$

$$x^TAx=x_1^2+5x_1x_2+4x_2^2$$

直接求偏导

对 $x_1$ 求偏导：

$$\frac{\partial}{\partial x_1}
\left(
x_1^2+5x_1x_2+4x_2^2
\right)
=
2x_1+5x_2$$

对 $x_2$ 求偏导：

$$\frac{\partial}{\partial x_2}
\left(
x_1^2+5x_1x_2+4x_2^2
\right)
=
5x_1+8x_2$$

所以：

$$\frac{\partial(x^TAx)}{\partial x}
=
\begin{pmatrix}
2x_1+5x_2\\\\
5x_1+8x_2
\end{pmatrix}$$

用公式验证

$$Ax=
\begin{pmatrix}
1&2\\\\
3&4
\end{pmatrix}
\begin{pmatrix}
x_1\\\\
x_2
\end{pmatrix}
=
\begin{pmatrix}
x_1+2x_2\\\\
3x_1+4x_2
\end{pmatrix}$$

$$A^Tx=
\begin{pmatrix}
1&3\\\\
2&4
\end{pmatrix}
\begin{pmatrix}
x_1\\\\
x_2
\end{pmatrix}
=
\begin{pmatrix}
x_1+3x_2\\\\
2x_1+4x_2
\end{pmatrix}$$

$$Ax+A^Tx
=
\begin{pmatrix}
x_1+2x_2\\\\
3x_1+4x_2
\end{pmatrix}
+
\begin{pmatrix}
x_1+3x_2\\\\
2x_1+4x_2
\end{pmatrix}
=
\begin{pmatrix}
2x_1+5x_2\\\\
5x_1+8x_2
\end{pmatrix}$$

结果一致：

$${
\frac{\partial(x^TAx)}{\partial x}
=
Ax+A^Tx
}$$

**双重乘积求导**：
$$\frac{\partial(a^T x x^T b)}{\partial x} = \frac{\partial(x^T a b^T x)}{\partial x} = ab^Tx + ba^Tx$$

a,b,x均为列向量，无矩阵，矩阵后面由$ab^T$得到

$$a^T x x^T b
=
x^T a b^T x
=
x^T(ab^T)x$$

令：

$$A=ab^T$$

则：

$$a^T x x^T b
=
x^T A x$$

可以直接套用二次型求导公式：

$$\frac{\partial(x^T A x)}{\partial x}
=
Ax+A^T x$$

所以：

$$\frac{\partial(a^T x x^T b)}{\partial x}
=
ab^T x+ba^T x$$

# 矩阵变元的实值标量函数(梯度方向)

$\boldsymbol{X}_{m \times n} = (x_{ij})_{i=1, j=1}^{m, n}$

$$\nabla_{\boldsymbol{X}} f(\boldsymbol{X}) = \frac{\partial f(\boldsymbol{X})}{\partial \boldsymbol{X}_{m \times n}} = \begin{pmatrix} \frac{\partial f}{\partial x_{11}} & \cdots & \frac{\partial f}{\partial x_{1n}} \\\\ \vdots & \ddots & \vdots \\\\ \frac{\partial f}{\partial x_{m1}} & \cdots & \frac{\partial f}{\partial x_{mn}} \end{pmatrix}$$

将输入和函数写在一起，结果和输入都是M*N矩阵

### 运算法则

$\frac{\partial [c_1 f(X) + c_2 g(X)]}{\partial X} = c_1 \frac{\partial f(X)}{\partial X} + c_2 \frac{\partial g(X)}{\partial X}$

和一阶求导一样可以把常数提取出来

$\frac{\partial [f(X)g(X)]}{\partial X} = \frac{\partial f(X)}{\partial X} g(X) + f(X) \frac{\partial g(X)}{\partial X}$

右乘左导+左乘右导

$\frac{\partial [\frac{f(X)}{g(X)}]}{\partial X} = \frac{1}{g^2(X)} \left[ \frac{\partial f(X)}{\partial X} g(X) - f(X) \frac{\partial g(X)}{\partial X} \right]$

上面这些通用于上面的笔记“向量变元的实值标量函数$f(x)$”的运算法则(仅是抄了笔记，未验证)

## 常用公式
### $\frac{\partial(a^T X b)}{\partial X} = ab^T$

$a_{m \times 1}, b_{n \times 1}$ 为常数向量

**推导**

**展开成双重求和**

TODO:展开玩的不熟，再找些类似的公式展开下

$$a^T X b = \sum_{i=1}^m \sum_{j=1}^n a_i x_{ij} b_j$$

求和中只有 $x_{ij}$ 这一项含 $x_{ij}$，其余视为常数：

$$\frac{\partial (a^T X b)}{\partial x_{ij}} = a_i b_j$$

**排成矩阵**

$$\frac{\partial (a^T X b)}{\partial X}
=
\begin{pmatrix}
a_1 b_1 & a_1 b_2 & \cdots & a_1 b_n \\\\
a_2 b_1 & a_2 b_2 & \cdots & a_2 b_n \\\\
\vdots & \vdots & \ddots & \vdots \\\\
a_m b_1 & a_m b_2 & \cdots & a_m b_n
\end{pmatrix}
=
\begin{pmatrix} a_1 \\\\ a_2 \\\\ \vdots \\\\ a_m \end{pmatrix}
\begin{pmatrix} b_1 & b_2 & \cdots & b_n \end{pmatrix}$$

**结论**

$${\frac{\partial(a^T X b)}{\partial X} = ab^T}$$

每个 $x_{ij}$ 的偏导为 $a_i b_j$，按 $(i,j)$ 排成矩阵，恰好是外积 $ab^T$

### $\frac{\partial(a^T X^T b)}{\partial X} = ba^T$

$a_{n \times 1}, b_{m \times 1}$ 为常数向量

**展开成双重求和**

$$(X^T)_{ij} = x_{ji}$$

转置后j代表行，i代表列。

其中 $i=1,\dots,n,\ j=1,\dots,m$。

因此

$$a^T X^T b
=
\sum_{i=1}^n \sum_{j=1}^m a_i (X^T)_{ij} b_j$$

$$a^T X^T b
=
\sum_{i=1}^n \sum_{j=1}^m a_i x_{ji} b_j$$

设

$$X=(x_{ij})_{m\times n},
\qquad i=1,\dots,m,\quad j=1,\dots,n.$$

$$(X^T)_{ji}=x_{ij}.$$

也就是说，$X^T$ 的第 $j$ 行第 $i$ 列元素是 $x_{ij}$。

**对 $x_{ij}$ 求偏导**

在

$$a^TX^Tb
=
\sum_{i=1}^m\sum_{j=1}^n b_i x_{ij} a_j$$

这个的x下标的ij和上面是反着，因为把i和j的指标换掉了，a和b也换了位置，相当于全部转置，因为这个的结果是标量，转置等于自身

中，只有含 $x_{ij}$ 的那一项是

$$b_i x_{ij} a_j.$$

其余项都不含 $x_{ij}$，对 $x_{ij}$ 求偏导时为 $0$。因此

$$\frac{\partial(a^TX^Tb)}{\partial x_{ij}}
=
b_i a_j.$$

注意这里结果是

$$b_i a_j,$$

不是 $a_i b_j$。原因是 $X^T$ 交换了指标：$X$ 的元素是 $x_{ij}$，而在 $X^T$ 中它位于第 $j$ 行第 $i$ 列，和 $a_j$、$b_i$ 配对。

**排成矩阵**

矩阵 $X$ 的第 $(i,j)$ 个元素是 $x_{ij}$。

因此

$$\frac{\partial(a^TX^Tb)}{\partial X}$$

的第 $(i,j)$ 个元素是

$$b_i a_j.$$

所以

$$\frac{\partial(a^TX^Tb)}{\partial X}
=
\begin{pmatrix}
b_1a_1 & b_1a_2 & \cdots & b_1a_n\\\\
b_2a_1 & b_2a_2 & \cdots & b_2a_n\\\\
\vdots & \vdots & \ddots & \vdots\\\\
b_ma_1 & b_ma_2 & \cdots & b_ma_n
\end{pmatrix}.$$

这正好是列向量 $b$ 和行向量 $a^T$ 的外积：

$$\begin{pmatrix}
b_1\\\\
b_2\\\\
\vdots\\\\
b_m
\end{pmatrix}
\begin{pmatrix}
a_1 & a_2 & \cdots & a_n
\end{pmatrix}
=
ba^T.$$

**结论**

$${
\frac{\partial(a^TX^Tb)}{\partial X}=ba^T
}$$

其中 $b$ 是 $m$ 维列向量，$a$ 是 $n$ 维列向量，所以 $ba^T$ 是 $m\times n$ 矩阵，和 $X$ 的形状一致。

$\frac{\partial(a^T X X^T b)}{\partial X} = ab^T X + ba^T X$
$a_{m \times 1}, b_{m \times 1}$ 为常数向量
$\frac{\partial(a^T X^T X b)}{\partial X} = Xba^T + Xab^T$
$a_{n \times 1}, b_{n \times 1}$ 为常数向量

### $\frac{\partial(a^T X X^T b)}{\partial X} = ab^T X + ba^T X$

**已知条件：**
$X = (x_{ij})_{m \times n}$ 为矩阵变量
$a_{m \times 1}, b_{m \times 1}$ 为常数列向量
求导结果为 $m \times n$ 的矩阵

**将函数展开成求和形式**

原函数为：
$$f(X) = a^T X X^T b$$

由于 $a$ 是 $m \times 1$，$X$ 是 $m \times n$，$X^T b$ 是 $n \times 1$，因此 $f(X)$ 是一个标量。

展开：

$a^T X$ 是一个 $1 \times n$ 的行向量，它的第 $j$ 个分量是$\sum_{i=1}^m a_i x_{ij}$

$X^T b$ 是一个 $n \times 1$ 的列向量，它的第 $j$ 个分量是$\sum_{k=1}^m x_{kj} b_k$

手推能得到上面的，j都对应原矩阵的列

$f = \sum_{j=1}^n \left( \sum_{i=1}^m a_i x_{ij} \right) \left( \sum_{k=1}^m x_{kj} b_k \right) = \sum_{j=1}^n \sum_{i=1}^m \sum_{k=1}^m a_i b_k x_{ij} x_{kj}$

**求偏导数 $\frac{\partial f}{\partial x_{pq}}$**

固定 $p$（行号）和 $q$（列号），求 $f$ 对 $x_{pq}$ 的偏导数。

在矩阵求导中，只有行列完全对应，才算是变量，才需要求导

在求和式中，$x_{pq}$ 只出现在 $j=q$ 且（$i=p$ 或 $k=p$）的项中。因此，我们需要分两部分计算。

**第一部分：当 $i=p$ 时**
此部分包含 $x_{pq}$，对 $x_{pq}$ 求导后，留下 $a_p b_k x_{kq}$。再对 $k$ 求和：
$$\frac{\partial}{\partial x_{pq}} \left( \sum_{k=1}^m a_p b_k x_{pq} x_{kq} \right) = \sum_{k=1}^m a_p b_k x_{kq} = a_p \sum_{k=1}^m b_k x_{kq}$$
注意 $\sum_{k=1}^m b_k x_{kq}$ 恰好是行向量 $b^T X$ 的第 $q$ 个分量，即 $(b^T X)_q$。所以这部分结果为：
$$a_p (b^T X)_q$$

向量的迭代和矩阵列不变，行迭代的迭代对应相乘，结果就是向量转置乘以矩阵，因为默认是左行右列，而这个乘法中是左列右行，所以向量转置

**第二部分：当 $k=p$ 时**
此部分包含 $x_{pq}$，对 $x_{pq}$ 求导后，留下 $a_i b_p x_{iq}$。再对 $i$ 求和：
$$\frac{\partial}{\partial x_{pq}} \left( \sum_{i=1}^m a_i b_p x_{iq} x_{pq} \right) = \sum_{i=1}^m a_i b_p x_{iq} = b_p \sum_{i=1}^m a_i x_{iq}$$
注意 $\sum_{i=1}^m a_i x_{iq}$ 恰好是行向量 $a^T X$ 的第 $q$ 个分量，即 $(a^T X)_q$。所以这部分结果为：
$$b_p (a^T X)_q$$

合并两部分：
$$\frac{\partial f}{\partial x_{pq}} = a_p (b^T X)_q + b_p (a^T X)_q$$

**第三步：还原为矩阵形式**

我们需要找到两个矩阵，使得它们的第 $p$ 行第 $q$ 列元素分别为上述两项。

1. 对于第一项 $a_p (b^T X)_q$：
   - $a_p$ 是列向量 $a$ 的第 $p$ 个元素。
   - $(b^T X)_q$ 是行向量 $b^T X$ 的第 $q$ 个元素。
   - 因此，第一项正好是外积矩阵 $a (b^T X)$ 的第 $p$ 行第 $q$ 列元素。

2. 对于第二项 $b_p (a^T X)_q$：
   - $b_p$ 是列向量 $b$ 的第 $p$ 个元素。
   - $(a^T X)_q$ 是行向量 $a^T X$ 的第 $q$ 个元素。
   - 因此，第二项正好是外积矩阵 $b (a^T X)$ 的第 $p$ 行第 $q$ 列元素。

将两者拼合，得到最终的矩阵导数：
$$\frac{\partial(a^T X X^T b)}{\partial X} = a (b^T X) + b (a^T X) = a b^T X + b a^T X$$

**维度验证（防止出错）**

- $a_{m \times 1} \cdot (b^T_{1 \times m} X_{m \times n}) = a_{m \times 1} \cdot (1 \times n) = m \times n$
- $b_{m \times 1} \cdot (a^T_{1 \times m} X_{m \times n}) = b_{m \times 1} \cdot (1 \times n) = m \times n$

结果均为 $m \times n$，与分母 $X$ 的维度完全一致。

# 全微分

在原函数上，让输入走一小段 $d\boldsymbol{x}$，求函数值的变化量 $df$，这个过程叫全微分。

全微分 $df$ 就是函数 $f$ 因为自变量 $\boldsymbol{x}$ 发生微小变化 $\mathrm{d}\boldsymbol{x}$ 而产生的标量增量。

公式为：

$$df = \frac{\partial f}{\partial x_1}dx_1 + \cdots + \frac{\partial f}{\partial x_n}dx_n$$

写成向量形式：

$$df = \nabla f(\boldsymbol{x})^T d\boldsymbol{x}$$

新函数值近似为：

$$f(\boldsymbol{x}+d\boldsymbol{x}) \approx f(\boldsymbol{x}) + df$$

所以关键是：

- $d\boldsymbol{x}$：输入走一小步
- $df$：函数值变化量
- 全微分：用梯度估计这个变化量

## 向量变元的实值标量函数（全微分）

$$\text{d}f(\boldsymbol{x}) = \left(\frac{\partial f}{\partial x_1}, \frac{\partial f}{\partial x_2}, \dots, \frac{\partial f}{\partial x_n}\right) \begin{pmatrix} \text{d}x_1 \\\\ \text{d}x_2 \\\\ \vdots \\\\ \text{d}x_n \end{pmatrix} = \text{tr} \left[ \left(\frac{\partial f}{\partial x_1}, \frac{\partial f}{\partial x_2}, \dots, \frac{\partial f}{\partial x_n}\right) \begin{pmatrix} \text{d}x_1 \\\\ \text{d}x_2 \\\\ \vdots \\\\ \text{d}x_n \end{pmatrix} \right]$$

**左侧**：$\text{d}f(\boldsymbol{x})$ 是标量函数的全微分。

**右侧（加tr）**：由于标量的迹就是它本身（$\text{tr}(a) = a$），这里加上 $\text{tr}[\cdot]$ 是为了与矩阵变元的情况保持形式上的统一。

## 矩阵变元的实值标量函数（全微分）

**2. 公式解析**

$$\text{d}f(\boldsymbol{X}) = \text{tr} \left[ \begin{pmatrix} \frac{\partial f}{\partial x_{11}} & \frac{\partial f}{\partial x_{21}} & \dots & \frac{\partial f}{\partial x_{m1}} \\\\ \frac{\partial f}{\partial x_{12}} & \frac{\partial f}{\partial x_{22}} & \dots & \frac{\partial f}{\partial x_{m2}} \\\\ \vdots & \vdots & \ddots & \vdots \\\\ \frac{\partial f}{\partial x_{1n}} & \frac{\partial f}{\partial x_{2n}} & \dots & \frac{\partial f}{\partial x_{mn}} \end{pmatrix}_{n \times m} \begin{pmatrix} \text{d}x_{11} & \text{d}x_{12} & \dots & \text{d}x_{1n} \\\\ \text{d}x_{21} & \text{d}x_{22} & \dots & \text{d}x_{2n} \\\\ \vdots & \vdots & \ddots & \vdots \\\\ \text{d}x_{m1} & \text{d}x_{m2} & \dots & \text{d}x_{mn} \end{pmatrix}_{m \times n} \right]$$

就是需要对应的dx与梯度相乘，之后把所有结果相加，这个公式就是写出这个结果如何用矩阵表示，迹，对角线之和

# 矩阵函数的微分

 **自变量**：矩阵 $\boldsymbol{X}_{m \times n} = (x_{ij})_{i=1, j=1}^{m, n}$
**函数**：矩阵 $\boldsymbol{F}_{p \times q}(X) = (f_{ij})_{i=1, j=1}^{p, q}$
也就是说，输入有 $m \times n$ 个元素，输出有 $p \times q$ 个元素。
这个f(x)是一堆标量函数组成矩阵形状。

### 微分 $\text{d}\boldsymbol{F}(X)$ 的本质
矩阵函数的微分，就是对矩阵里的每一个元素分别求全微分，然后按照原来的位置排成一个新的 $p \times q$ 矩阵。这个的每个子项是矩阵变元的实值标量函数的全微分。

$$\text{d}\boldsymbol{F}_{p \times q}(X) = 
\begin{pmatrix} 
\text{d}f_{11}(X) & \text{d}f_{12}(X) & \dots & \text{d}f_{1q}(X) \\\\ 
\text{d}f_{21}(X) & \text{d}f_{22}(X) & \dots & \text{d}f_{2q}(X) \\\\ 
\vdots & \vdots & \ddots & \vdots \\\\ 
\text{d}f_{p1}(X) & \text{d}f_{p2}(X) & \dots & \text{d}f_{pq}(X) 
\end{pmatrix}_{p \times q}$$

# 矩阵函数全微分举例：$\boldsymbol{F}(X) = X^2$

**设定原函数**

假设自变量是 $2 \times 2$ 矩阵：

$$X = \begin{pmatrix} x_{11} & x_{12} \\\\ x_{21} & x_{22} \end{pmatrix}$$

定义一个矩阵函数：输出也是 $2 \times 2$ 矩阵，设 $F(X) = X^2$：

$$F(X) = X \cdot X = 
\begin{pmatrix} x_{11} & x_{12} \\\\ x_{21} & x_{22} \end{pmatrix}
\begin{pmatrix} x_{11} & x_{12} \\\\ x_{21} & x_{22} \end{pmatrix}$$

乘开后得到四个标量函数：

这个就是F(x)

$$F(X) = 
\begin{pmatrix} 
f_{11}(X) & f_{12}(X) \\\\ 
f_{21}(X) & f_{22}(X) 
\end{pmatrix} = 
\begin{pmatrix} 
x_{11}^2 + x_{12}x_{21} & x_{11}x_{12} + x_{12}x_{22} \\\\ 
x_{21}x_{11} + x_{22}x_{21} & x_{21}x_{12} + x_{22}^2 
\end{pmatrix}$$

**求全微分 $\mathrm{d}\boldsymbol{F}(X)$**

全微分公式：
$$\mathrm{d}f = \sum \frac{\partial f}{\partial x_{ij}} \mathrm{d}x_{ij}$$

为了不晕，先把双下标换成普通变量：
$$x_{11} = a, \quad x_{12} = b, \quad x_{21} = c, \quad x_{22} = d$$

**左上角 $f_{11} = x_{11}^2 + x_{12}x_{21}$**

替换变量：
$$f_{11} = a^2 + bc$$

分别求偏导：
- 对 $a$ 求偏导：$2a$
- 对 $b$ 求偏导：$c$
- 对 $c$ 求偏导：$b$
- 对 $d$ 求偏导：$0$

根据全微分公式拼起来：
$$\mathrm{d}f_{11} = 2a \cdot \mathrm{d}a + c \cdot \mathrm{d}b + b \cdot \mathrm{d}c$$

换回双下标：
$$\mathrm{d}f_{11} = 2x_{11}\mathrm{d}x_{11} + x_{21}\mathrm{d}x_{12} + x_{12}\mathrm{d}x_{21}$$

**右上角 $f_{12} = x_{11}x_{12} + x_{12}x_{22}$**

替换变量：
$$f_{12} = ab + bd$$

分别求偏导：
- 对 $a$ 求偏导：$b$
- 对 $b$ 求偏导：$a + d$
- 对 $c$ 求偏导：$0$
- 对 $d$ 求偏导：$b$

拼起来：
$$\mathrm{d}f_{12} = b \cdot \mathrm{d}a + (a+d) \cdot \mathrm{d}b + b \cdot \mathrm{d}d$$

换回双下标：
$$\mathrm{d}f_{12} = x_{12}\mathrm{d}x_{11} + (x_{11}+x_{22})\mathrm{d}x_{12} + x_{12}\mathrm{d}x_{22}$$

**左下角 $f_{21} = x_{21}x_{11} + x_{22}x_{21}$**

替换变量：
$$f_{21} = ca + dc$$

分别求偏导：
- 对 $a$ 求偏导：$c$
- 对 $b$ 求偏导：$0$
- 对 $c$ 求偏导：$a + d$
- 对 $d$ 求偏导：$c$

拼起来：
$$\mathrm{d}f_{21} = c \cdot \mathrm{d}a + (a+d) \cdot \mathrm{d}c + c \cdot \mathrm{d}d$$

换回双下标：
$$\mathrm{d}f_{21} = x_{21}\mathrm{d}x_{11} + (x_{11}+x_{22})\mathrm{d}x_{21} + x_{21}\mathrm{d}x_{22}$$

**右下角 $f_{22} = x_{21}x_{12} + x_{22}^2$**

替换变量：
$$f_{22} = cb + d^2$$

分别求偏导：
- 对 $a$ 求偏导：$0$
- 对 $b$ 求偏导：$c$
- 对 $c$ 求偏导：$b$
- 对 $d$ 求偏导：$2d$

拼起来：
$$\mathrm{d}f_{22} = c \cdot \mathrm{d}b + b \cdot \mathrm{d}c + 2d \cdot \mathrm{d}d$$

换回双下标：
$$\mathrm{d}f_{22} = x_{12}\mathrm{d}x_{21} + x_{21}\mathrm{d}x_{12} + 2x_{22}\mathrm{d}x_{22}$$

**拼成矩阵**

$$\mathrm{d}\boldsymbol{F}(X) = 
\begin{pmatrix} 
\mathrm{d}f_{11} & \mathrm{d}f_{12} \\\\ 
\mathrm{d}f_{21} & \mathrm{d}f_{22} 
\end{pmatrix}$$

它依然是一个 $2 \times 2$ 的矩阵，只是每个元素变成了标量全微分。

### 四条微分运算法则解析

todo 不算难，练习不够不熟悉

**常数微分法则**
$$\text{d}\boldsymbol{A}_{m \times n} = \boldsymbol{0}_{m \times n}$$
*   **解释**：常数矩阵对任何自变量都没有变化率，其微分为全零矩阵。

**微分线性法则**
$$\text{d}(c_1 \boldsymbol{F}(X) + c_2 \boldsymbol{G}(X)) = c_1 \text{d}\boldsymbol{F}(X) + c_2 \text{d}\boldsymbol{G}(X)$$
*   **解释**：和普通标量微积分一样，常数系数可以提出来，加法可以拆开。求微分是一个线性算子。

**微分乘积法则（重要）**
$$\text{d}[\boldsymbol{F}(X)\boldsymbol{G}(X)] = [\text{d}\boldsymbol{F}(X)]\boldsymbol{G}(X) + \boldsymbol{F}(X)[\text{d}\boldsymbol{G}(X)]$$
*   **解释**：形式上和标量的“左乘右导，右乘左导”一模一样，但必须严格保持矩阵乘法的顺序！
*   你不能写成 $\boldsymbol{G}(X)[\text{d}\boldsymbol{F}(X)]$。因为矩阵乘法不满足交换律（$\boldsymbol{A}\boldsymbol{B} \neq \boldsymbol{B}\boldsymbol{A}$）。
*   **三阶推广**：
$$\text{d}[\boldsymbol{F}(X)\boldsymbol{G}(X)\boldsymbol{H}(X)] = [\text{d}\boldsymbol{F}(X)]\boldsymbol{G}(X)\boldsymbol{H}(X) + \boldsymbol{F}(X)[\text{d}\boldsymbol{G}(X)]\boldsymbol{H}(X) + \boldsymbol{F}(X)\boldsymbol{G}(X)[\text{d}\boldsymbol{H}(X)]$$

**微分转置法则**
$$\text{d}\boldsymbol{F}^{T}_{p \times q}(X) = [\text{d}\boldsymbol{F}_{p \times q}(X)]^{T}$$
 **解释**：微分的转置 = 转置的微分。先转置再求微分，或者先求微分再转置，结果一样。注意维度变化：$p \times q$ 变成 $q \times p$。

