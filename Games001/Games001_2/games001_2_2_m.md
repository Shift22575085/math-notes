# 利用矩阵微分求导

## 基本设定

**自变量**

$$f(X), \quad X_{m \times n} = (x_{ij})_{i=1, j=1}^{m, n}$$

- $`X`$ 是一个 $`m \times n`$ 的矩阵。
- $`f(X)`$ 是一个实值标量函数（输入矩阵，输出一个数）。

**自变量的微分**

$$\mathrm{d}X_{m \times n} =
\begin{pmatrix}
\mathrm{d}x_{11} & \mathrm{d}x_{12} & \dots & \mathrm{d}x_{1n} \\\\
\mathrm{d}x_{21} & \mathrm{d}x_{22} & \dots & \mathrm{d}x_{2n} \\\\
\vdots & \vdots & \ddots & \vdots \\\\
\mathrm{d}x_{m1} & \mathrm{d}x_{m2} & \dots & \mathrm{d}x_{mn}
\end{pmatrix}_{m \times n}$$

把 $`X`$ 中每个元素 $`x_{ij}`$ 换成它的微分 $`\mathrm{d}x_{ij}`$，保持矩阵形状不变。

**梯度矩阵（分子布局）**

$$\frac{\partial f(X)}{\partial X^T_{n \times m}} =
\begin{pmatrix}
\frac{\partial f}{\partial x_{11}} & \frac{\partial f}{\partial x_{21}} & \dots & \frac{\partial f}{\partial x_{m1}} \\\\
\frac{\partial f}{\partial x_{12}} & \frac{\partial f}{\partial x_{22}} & \dots & \frac{\partial f}{\partial x_{m2}} \\\\
\vdots & \vdots & \ddots & \vdots \\\\
\frac{\partial f}{\partial x_{1n}} & \frac{\partial f}{\partial x_{2n}} & \dots & \frac{\partial f}{\partial x_{mn}}
\end{pmatrix}_{n \times m}$$

关键点：
分母写的是 $`X^T`$，不是 $`X`$，这叫分子布局。
结果是 $`n \times m`$ 矩阵，元素是 $`\frac{\partial f}{\partial x_{ji}}`$（下标与 $`X`$ 相反）。
如果写成标准的 $`m \times n`$ 梯度矩阵 $`\frac{\partial f}{\partial X}`$，只需把上式转置即可。

**矩阵微分运算法则**

$$\mathrm{d}(AXB) = A(\mathrm{d}X)B$$

- $`A_{p \times m}`$、$`B_{n \times q}`$ 为常数矩阵。
- 常数矩阵在微分中像“透明”的，微分符号 $`\mathrm{d}`$ 直接作用在中间的 $`X`$ 上。
- 必须保持矩阵乘法顺序：$`A`$ 还在左边，$`B`$ 还在右边。
- 类比标量：$`\mathrm{d}(axb) = a \cdot \mathrm{d}x \cdot b`$。

**全微分公式（核心）**

$$\mathrm{d}f(X) = \mathrm{tr}\left[ \frac{\partial f(X)}{\partial X^T} \mathrm{d}X \right]$$

维度验证：
- $`\frac{\partial f(X)}{\partial X^T}`$ 是 $`n \times m`$ 矩阵。
- $`\mathrm{d}X`$ 是 $`m \times n`$ 矩阵。
- 相乘：$`(n \times m) \times (m \times n) = n \times n`$ 方阵。
- 取迹 $`\mathrm{tr}`$ 后变成标量，与 $`\mathrm{d}f(X)`$ 一致；$`f(X)`$ 为实值标量函数，微分为标量。

本质：
- 把所有偏导数与对应微分的加权和，用矩阵乘法加迹的形式统一表达。
- 即 $`\mathrm{d}f = \sum_{i=1}^m \sum_{j=1}^n \frac{\partial f}{\partial x_{ij}} \mathrm{d}x_{ij}`$。

## 求导

### 代数余子式$`\frac{\partial |X|}{\partial x_{ij}} = A_{ij}`$

$`|X| = x_{i1}A_{i1} + x_{i2}A_{i2} + \dots + x_{in}A_{in}`$，因此 $`\frac{\partial |X|}{\partial x_{ij}} = A_{ij}`$。

$`x_{ij}`$：第 $`i`$ 行第 $`j`$ 列的元素。

$`A_{ij}`$：该元素的代数余子式，等于 $`(-1)^{i+j}`$ 乘以划掉第 $`i`$ 行第 $`j`$ 列后的行列式。

上面 $`|X|`$ 的公式是高阶矩阵求行列式的方法。

$`A_{i2} = (-1)^{i+2} M_{i2}`$，其中 $`M_{i2}`$ 是划掉第 $`i`$ 行第 2 列后剩下的行列式。

在按第 $`i`$ 行展开的公式

$$|X|=\sum_{j=1}^{n}x_{ij}A_{ij}$$

中，对于固定的 $`x_{ij}`$，只有一项显式含有 $`x_{ij}`$，就是

$$x_{ij}A_{ij},$$

这一项。所以求导结果是 $`A_{ij}`$,行列式作为函数，固定点作为变量，求导结果为这个点的余子式。

### 行列式对 $`X^T`$ 的梯度：$`\frac{\partial |X|}{\partial X^T} = X^\ast `$

**公式**

$${\frac{\partial |X|}{\partial X^T} = X^\ast }$$

$`|X|`$：矩阵 $`X`$ 的行列式（一个标量）
$`\frac{\partial |X|}{\partial X^T}`$：行列式对 $`X^T`$ 的梯度（分子布局，结果是一个矩阵）
$`X^\ast `$：$`X`$ 的伴随矩阵

一句话含义：行列式对 $`X^T`$ 的梯度，等于伴随矩阵。

**左边：$`\frac{\partial |X|}{\partial X^T}`$**

$`|X|`$ 是一个标量。对矩阵求导，结果是一个矩阵。

分母写的是 $`X^T`$，这是分子布局的写法。

在这种布局下，结果的第 $`(i,j)`$ 个元素是：

$$\left(\frac{\partial |X|}{\partial X^T}\right)_{ij} = \frac{\partial |X|}{\partial x_{ji}}$$

注意下标是反的：第 $`(i,j)`$ 个元素是 $`|X|`$ 对 $`x_{ji}`$ 的偏导。

行列式是函数，矩阵是变量。

**右边：$`X^\ast `$**

$`X^\ast `$ 是伴随矩阵。

伴随矩阵的定义是：代数余子式矩阵的转置。

设 $`A_{ij}`$ 是 $`X`$ 的第 $`(i,j)`$ 个元素的代数余子式。

代数余子式矩阵：

$$C = \begin{pmatrix} A_{11} & A_{12} & \dots \\\\ A_{21} & A_{22} & \dots \\\\ \vdots & \vdots & \ddots \end{pmatrix}$$

伴随矩阵：

$$X^\ast  = C^T$$

所以 $`X^\ast `$ 的第 $`(i,j)`$ 个元素是：

$$(X^\ast )_{ij} = A_{ji}$$

注意下标也是反的：伴随矩阵的第 $`(i,j)`$ 个元素，是 $`x_{ji}`$ 的代数余子式。

**为什么相等**

对比左右两边的第 $`(i,j)`$ 个元素：

左边：

$$\left(\frac{\partial |X|}{\partial X^T}\right)_{ij} = \frac{\partial |X|}{\partial x_{ji}}$$

右边：

$$(X^\ast )_{ij} = A_{ji}$$

需要证明：

$$\frac{\partial |X|}{\partial x_{ji}} = A_{ji}$$

行列式对某个元素的偏导，等于该元素的代数余子式，上文已经得到。

$$\frac{\partial |X|}{\partial x_{ij}} = A_{ij}$$

把 $`i`$ 和 $`j`$ 互换：

$$\frac{\partial |X|}{\partial x_{ji}} = A_{ji}$$

所以左边第 $`(i,j)`$ 个元素 = 右边第 $`(i,j)`$ 个元素。

**对任意 $`(i,j)`$ 都成立，所以两个矩阵相等：**

$$\frac{\partial |X|}{\partial X^T} = X^\ast $$

### 逆矩阵公式：$`X^{-1} = \dfrac{X^\ast }{|X|}`$

$`\frac{\partial |X|}{\partial X^T} = X^\ast `$（$`X^\ast `$ 即伴随矩阵，$`X^{-1} = X^\ast  / |X|`$）。

**推导：**

$${X^{-1} = \frac{X^\ast }{|X|}}$$

**第一步：伴随矩阵的核心性质**

伴随矩阵满足：

$$X X^\ast  = |X| E$$

其中 $`E`$ 是单位矩阵。

**第二步：两边同时除以 $`|X|`$**

前提是 $`|X| \neq 0`$（行列式不为零，矩阵可逆）。

$$X \cdot \frac{X^\ast }{|X|} = E$$

**第三步：对照逆矩阵的定义**

逆矩阵的定义是：

如果 $`X Y = E`$，那么 $`Y = X^{-1}`$。

所以：

$$\frac{X^\ast }{|X|} = X^{-1}$$

即：

$$X^{-1} = \frac{X^\ast }{|X|}$$

**为什么 $`X X^\ast  = |X| E`$**

设：

$$X = \begin{pmatrix} a & b \\\\ c & d \end{pmatrix}$$

伴随矩阵：

$$X^\ast  = \begin{pmatrix} d & -b \\\\ -c & a \end{pmatrix}$$

计算 $`X X^\ast `$：

第一行第一列：

$$a \cdot d + b \cdot (-c) = ad - bc = |X|$$

第一行第二列：

$$a \cdot (-b) + b \cdot a = -ab + ab = 0$$

第二行第一列：

$$c \cdot d + d \cdot (-c) = cd - dc = 0$$

第二行第二列：

$$c \cdot (-b) + d \cdot a = -bc + ad = ad - bc = |X|$$

所以：

$$X X^\ast  = \begin{pmatrix} |X| & 0 \\\\ 0 & |X| \end{pmatrix} = |X| E$$

**一般情况**

对 $`n`$ 阶矩阵，$`X X^\ast `$ 的第 $`(i,j)`$ 个元素是：

$$(X X^\ast )_{ij} = \sum_{k=1}^n x_{ik} (X^\ast )_{kj} = \sum_{k=1}^n x_{ik} A_{jk}$$

其中 $`A_{jk}`$ 是 $`x_{jk}`$ 的代数余子式。

**当 $`i = j`$ 时**：

$$\sum_{k=1}^n x_{ik} A_{ik} = |X|$$

这正是行列式按第 $`i`$ 行展开的公式。

**当 $`i \neq j`$ 时**：

$$\sum_{k=1}^n x_{ik} A_{jk} = 0$$

因为这是“异行展开”：用第 $`i`$ 行的元素乘以第 $`j`$ 行的代数余子式，结果为零。

所以：

$$X X^\ast  = \begin{pmatrix} |X| & 0 & \dots \\\\ 0 & |X| & \dots \\\\ \vdots & \vdots & \ddots \end{pmatrix} = |X| E$$

### 行列式全微分公式$`|X| \mathrm{tr}(X^{-1} \mathrm{d}X)`$

$`\mathrm{d}|X| = \mathrm{tr}(|X| X^{-1} \mathrm{d}X) = |X| \mathrm{tr}(X^{-1} \mathrm{d}X)`$

其中 $`X`$ 为 $`n`$ 阶可逆矩阵，$`|X|=\det(X)`$。

**推导**

行列式按第 $`i`$ 行展开：

$$|X| = \sum_{j=1}^n x_{ij} A_{ij}$$

其中 $`A_{ij}`$ 是元素 $`x_{ij}`$ 的代数余子式。因为 $`A_{ij}`$ 不包含 $`x_{ij}`$，所以

$$\frac{\partial |X|}{\partial x_{ij}} = A_{ij}$$

#### $`\mathrm{d}|X| = \sum_{i,j} A_{ij} \mathrm{d}x_{ij}= \operatorname{tr}(\operatorname{adj}(X) \mathrm{d}X)`$

因为 $`|X|`$ 是矩阵 $`X`$ 里所有 $`n \times n`$ 个元素的函数，所以它的全微分是：

$$\mathrm{d}|X| = \sum_{i=1}^n \sum_{j=1}^n \frac{\partial |X|}{\partial x_{ij}} \mathrm{d}x_{ij}$$

我们已经知道 $`\dfrac{\partial |X|}{\partial x_{ij}} = A_{ij}`$，代入：

$$\mathrm{d}|X| = \sum_{i=1}^n \sum_{j=1}^n A_{ij} \mathrm{d}x_{aij}$$

$`A_{ij}`$ 属于代数余子式矩阵（伴随矩阵的转置），$`\mathrm{d}x_{ij}`$ 属于微分矩阵 $`\mathrm{d}X`$。这种“对应位置相乘再相加”的操作，可以表示为矩阵乘法加迹的形式：

$$\sum_{i=1}^n \sum_{j=1}^n A_{ij} \mathrm{d}x_{ij} = \operatorname{tr}(C^T \mathrm{d}X)$$

其中 $`C`$ 是代数余子式矩阵，$`C^T`$ 正好是伴随矩阵 $`\operatorname{adj}(X)`$。所以：

$$\mathrm{d}|X| = \operatorname{tr}(\operatorname{adj}(X) \mathrm{d}X)$$

$$\mathrm{d}|X| = \sum_{i,j} A_{ij} \mathrm{d}x_{ij}
= \operatorname{tr}(\operatorname{adj}(X) \mathrm{d}X)$$

当 $`X`$ 可逆时，由 $`X X^\ast  = |X| E`$ 两边左乘 $`X^{-1}`$，得 $`X^\ast  = |X| X^{-1}`$，即 $`\operatorname{adj}(X) = |X| X^{-1}`$。

$$\mathrm{d}|X| = \operatorname{tr}(|X| X^{-1} \mathrm{d}X)
= |X| \operatorname{tr}(X^{-1} \mathrm{d}X)$$

### 逆矩阵的微分
由 $`X X^{-1} = E`$ 两边求微分：

$$(\mathrm{d}X)X^{-1} + X(\mathrm{d}(X^{-1})) = 0$$

$$\mathrm{d}(X^{-1}) = -X^{-1}(\mathrm{d}X)X^{-1}$$

## 经典证明案例
**题目**：证明 $`\frac{\partial \mathrm{tr}(X^T X)}{\partial X} = 2X`$

**证明**：
$`\mathrm{d}\thinspace\mathrm{tr}(X^T X) = \mathrm{tr}[\mathrm{d}(X^T)X] + \mathrm{tr}[X^T \mathrm{d}X]`$
右边公式对等于微分乘积法则中的左乘右导，右乘左导，并且d可以穿透tr直接作用在X上。

利用转置法则和迹的转置不变性（因为 $`\mathrm{tr}(A) = \mathrm{tr}(A^T)`$）：
外面带着tr，里面的利用$`(AB)^T = B^T A^T`$进行转置（第一项）。

$$= \mathrm{tr}[(\mathrm{d}X)^T X] + \mathrm{tr}[X^T \mathrm{d}X] = \mathrm{tr}[X^T \mathrm{d}X] + \mathrm{tr}[X^T \mathrm{d}X] = 2\mathrm{tr}[X^T \mathrm{d}X]$$

对照标准公式 $`\mathrm{d}f = \mathrm{tr}\left[\frac{\partial f}{\partial X^T} \mathrm{d}X\right]`$，可得 $`\frac{\partial f}{\partial X^T} = 2X^T`$，转置后得 $`\frac{\partial f}{\partial X} = 2X`$（因为分母是 $`X^T`$，提取出的是 $`\frac{\partial f}{\partial X^T}`$；若要分母布局的 $`\frac{\partial f}{\partial X}`$，转置即可）。

# 张量积分

### 外积

**核心定义与符号说明**

$`\boldsymbol{a} \otimes \boldsymbol{b} = A = \boldsymbol{a}\boldsymbol{b}^H`$
$`\boldsymbol{a}, \boldsymbol{b}`$：均为列向量。
$`\boldsymbol{a} \otimes \boldsymbol{b}`$：表示外积（张量积）。
$`\boldsymbol{a}\boldsymbol{b}^H`$：矩阵乘法，列向量乘以行向量。
$`H`$：表示共轭转置（Hermitian 转置）。
在复数域中，$`\boldsymbol{b}^H = (\boldsymbol{b}^\ast )^T`$（共轭并转置）。
在实数域中，$`\boldsymbol{b}^H = \boldsymbol{b}^T`$（直接转置），因此公式简化为 $`\boldsymbol{a}\boldsymbol{b}^T`$。

**实数域上的矩阵表示**

$$\begin{pmatrix} a_x \\\\ a_y \\\\ a_z \end{pmatrix} 
\begin{pmatrix} b_x & b_y & b_z \end{pmatrix} =
\begin{pmatrix}
a_x b_x & a_x b_y & a_x b_z \\\\
a_y b_x & a_y b_y & a_y b_z \\\\
a_z b_x & a_z b_y & a_z b_z
\end{pmatrix}$$

只要a,b非0，秩固定为1,结果矩阵的每一列都是a的倍数，必定降秩为1，三维空间缩小成一根线，缩小到a这一条线上。

**迹等于内积**

图片中给出了一个非常重要的性质：

$$\operatorname{tr}(\boldsymbol{a} \otimes \boldsymbol{b}) = \boldsymbol{a} \cdot \boldsymbol{b}$$

因为是$`ab^T`$，这个的对角线之后等于对应点相乘

### 克罗内克积（Kronecker Product）

**定义**
对矩阵 $`A_{m \times n}`$ 和 $`B_{p \times q}`$，克罗内克积 $`A \otimes B`$ 是一个 $`mp \times nq`$ 的分块矩阵：

$$A \otimes B = \begin{pmatrix} a_{11}B & \cdots & a_{1n}B \\\\ \vdots & \ddots & \vdots \\\\ a_{m1}B & \cdots & a_{mn}B \end{pmatrix}$$

设 

$$A = \begin{pmatrix} 1 & 2 \\\\ 3 & 4 \end{pmatrix}, \quad B = \begin{pmatrix} 0 & 5 \\\\ 6 & 7 \end{pmatrix}$$

则 

$$A \otimes B = \begin{pmatrix} 1B & 2B \\\\ 3B & 4B \end{pmatrix} = \begin{pmatrix} 0 & 5 & 0 & 10 \\\\ 6 & 7 & 12 & 14 \\\\ 0 & 15 & 0 & 20 \\\\ 18 & 21 & 24 & 28 \end{pmatrix}_{4 \times 4}$$

**与外积（并矢）的区别**

向量外积：$`\boldsymbol{a}_{m \times 1} \otimes \boldsymbol{b}_{n \times 1} = \boldsymbol{a}\boldsymbol{b}^T`$（结果 $`m \times n`$）

矩阵克罗内克积：$`A_{m \times n} \otimes B_{p \times q}`$（结果 $`mp \times nq`$，是分块矩阵）
两者都使用 $`\otimes`$，但克罗内克积更通用。

**核心性质**

**TODO这段没推导**

混合乘积：$`(A \otimes B)(C \otimes D) = (AC) \otimes (BD)`$
转置：$`(A \otimes B)^T = A^T \otimes B^T`$
逆：$`(A \otimes B)^{-1} = A^{-1} \otimes B^{-1}`$
向量化应用：$`AXB = C \iff (B^T \otimes A)\text{vec}(X) = \text{vec}(C)`$

### 协变 (covariant) 与逆变 (contravariant)

在向量空间中，基底是人为给定的，本质的东西是向量本身；协/逆变是对分量而言的
例：三维欧氏空间中的位移 $`\boldsymbol{x} = x^1\boldsymbol{e}_1 + x^2\boldsymbol{e}_2 + x^3\boldsymbol{e}_3`$

设 $`\boldsymbol{x}=(2,1)`$，$`\boldsymbol{e}_1=(1,0)`$，$`\boldsymbol{e}_2=(1,1)`$

**逆变分量**

如果 $`\boldsymbol{e}_i`$ 的模长增大，则坐标 $`x^i`$ 将相应减小，因此称 $`x^i`$ 是“逆变”的

逆变是达到这个向量，用了多少把尺子（基底）

逆变分量：$`a\boldsymbol{e}_1+b\boldsymbol{e}_2=\boldsymbol{x}`$，即 $`a(1,0)+b(1,1)=(2,1)`$，得 $`a=1,\ b=1`$

**协变分量**

如果 $`\boldsymbol{e}_i`$ 的模长增大，则 $`\boldsymbol{x} \cdot \boldsymbol{e}_i`$ 的模长也会增大，因此 $`x_i = \boldsymbol{x} \cdot \boldsymbol{e}_i`$ 是“协变”的

协变是将向量投影到基底上，长度是多少

协变分量：$`x_1=\boldsymbol{x}\cdot\boldsymbol{e}_1=(2,1)\cdot(1,0)=2`$，$`x_2=\boldsymbol{x}\cdot\boldsymbol{e}_2=(2,1)\cdot(1,1)=3`$

**克罗内克符号 $`\delta_i^j`$**

 在一般情况下 $`x_i \neq x^i`$，可以定义一组新的基底 $`\lbrace\boldsymbol{e}^1, \boldsymbol{e}^2, \boldsymbol{e}^3\rbrace`$ 使得 $`\boldsymbol{e}_i \cdot \boldsymbol{e}^j = \delta_i^j`$
拼凑用的数量 → 逆变分量（上标 $`x^i`$）
点乘的投影读数 → 协变分量（下标 $`x_i`$）

克罗内克符号 

$$\delta_i^j = \begin{cases} 0, & i \neq j \\\\ 1, & i = j \end{cases}$$

$`\delta_i^j`$ 比较的是基向量 $`\boldsymbol{e}_i`$ 和 $`\boldsymbol{e}^j`$ 的指标。

$$\boldsymbol{e}_i \cdot \boldsymbol{e}^j = \delta_i^j$$

$`i=j`$ 时，$`\boldsymbol{e}_i`$ 和 $`\boldsymbol{e}^j`$ 点乘为 1
$`i \neq j`$ 时，$`\boldsymbol{e}_i`$ 和 $`\boldsymbol{e}^j`$ 点乘为 0

#### $`\delta_i^j`$计算例子

设 $`\boldsymbol{x}=(2,1)`$，原基底 $`\boldsymbol{e}_1=(1,0)`$，$`\boldsymbol{e}_2=(1,1)`$

**逆变分量（解方程）**：
$`a\boldsymbol{e}_1+b\boldsymbol{e}_2=\boldsymbol{x}`$，即 $`a(1,0)+b(1,1)=(2,1)`$，得 $`a=1,\ b=1`$，所以 $`x^1=1,\ x^2=1`$。

**协变分量（点乘原基底）**：
$`x_1=\boldsymbol{x}\cdot\boldsymbol{e}_1=(2,1)\cdot(1,0)=2`$，
$`x_2=\boldsymbol{x}\cdot\boldsymbol{e}_2=(2,1)\cdot(1,1)=3`$。

**对偶基底**：
设 $`\boldsymbol{e}^1=(p,q)`$，由 $`\boldsymbol{e}_1\cdot\boldsymbol{e}^1=1`$，$`\boldsymbol{e}_2\cdot\boldsymbol{e}^1=0`$，解得 $`\boldsymbol{e}^1=(1,-1)`$；
设 $`\boldsymbol{e}^2=(r,s)`$，由 $`\boldsymbol{e}_1\cdot\boldsymbol{e}^2=0`$，$`\boldsymbol{e}_2\cdot\boldsymbol{e}^2=1`$，解得 $`\boldsymbol{e}^2=(0,1)`$。

**用对偶基底求逆变分量**：
$`x^1=\boldsymbol{x}\cdot\boldsymbol{e}^1=(2,1)\cdot(1,-1)=1`$，
$`x^2=\boldsymbol{x}\cdot\boldsymbol{e}^2=(2,1)\cdot(0,1)=1`$。

**则协变与逆变都可以写成**

$$x_i = \boldsymbol{x} \cdot \boldsymbol{e}_i,\qquad x^i = \boldsymbol{x} \cdot \boldsymbol{e}^i$$

向量点乘原基底得到协变向量，向量点乘对偶基底得到逆变向量

在不引入克罗内克符号的情况下，逆变向量使用的上标和下标的符号是反的，是解方程才能得到的

### 位移用逆变基底展开

位移也可以用逆变基底展开(协变量乘对偶空间基底得到原向量)：$`\boldsymbol{x} = x_1\boldsymbol{e}^1 + x_2\boldsymbol{e}^2 + x_3\boldsymbol{e}^3`$

设 $`\boldsymbol{x}=(2,1),\boldsymbol{e}_1=(1,0),\boldsymbol{e}_2=(1,1)`$
得 $`\boldsymbol{e}^1=(1,-1),\boldsymbol{e}^2=(0,1)`$
协变分量 $`x_1=2,x_2=3`$
则 $`x_1\boldsymbol{e}^1+x_2\boldsymbol{e}^2=2(1,-1)+3(0,1)=(2,1)=\boldsymbol{x}`$

### 爱因斯坦求和

爱因斯坦求和记号：$`\boldsymbol{x} = x_i\boldsymbol{e}^i = x^i\boldsymbol{e}_i`$

省略了求和符号 $`\sum`$，完整展开为：

$$\boldsymbol{x} = \sum_{i=1}^{n} x_i \boldsymbol{e}^i = \sum_{i=1}^{n} x^i \boldsymbol{e}_i$$

**逆变分量原基底得到x**
逆变分量：$`x^1\boldsymbol{e}_1+x^2\boldsymbol{e}_2=\boldsymbol{x}`$，即 $`x^1(1,0)+x^2(1,1)=(2,1)`$，解得 $`x^1=1,\ x^2=1`$

则：

$$\boldsymbol{x}=x^1\boldsymbol{e}_1+x^2\boldsymbol{e}_2=1(1,0)+1(1,1)=(2,1)$$

在三维空间中（$`n=3`$）：

$$\boldsymbol{x} = x_1 \boldsymbol{e}^1 + x_2 \boldsymbol{e}^2 + x_3 \boldsymbol{e}^3 = x^1 \boldsymbol{e}_1 + x^2 \boldsymbol{e}_2 + x^3 \boldsymbol{e}_3$$

### $`g_{ij} = \boldsymbol{e}_i \cdot \boldsymbol{e}_j`$ 度规张量

逆变与协变分量的关系
$`x_i = \boldsymbol{x} \cdot \boldsymbol{e}_i, \ x^j = \boldsymbol{x} \cdot \boldsymbol{e}^j \Rightarrow x_i = (x^j\boldsymbol{e}_j) \cdot \boldsymbol{e}_i = x^j(\boldsymbol{e}_j \cdot \boldsymbol{e}_i) = x^j g_{ij}`$
$`g_{ij} = \boldsymbol{e}_i \cdot \boldsymbol{e}_j`$ 称为度规张量

上面代入x的公式是使用了爱因斯坦求和的逆变分量点乘原基底得到的x,这个j是求和指标，后面将$`X_j`$提取了

# 从标量、矢量到张量

### 核心前提
**协变/逆变的概念是由于基底的选取而产生的。**
基底（尺子）可以任意改变，为了抵消基底变化带来的影响，分量的标号（上标/下标）必须相应变化。

### 各阶张量的定义与指标

**标量（0 阶张量）**
特征：没有“分量”的概念，只是一个纯数字。
协变/逆变：因为不需要基底，所以无所谓协变/逆变。

**矢量（1 阶张量）**
特征：是协变/逆变基底的线性组合。
协变/逆变：只有一个指标决定它的性质。
逆变矢量：$`v^i`$（上标），配原基底 $`\boldsymbol{e}_i`$。
协变矢量：$`v_i`$（下标），配对偶基底 $`\boldsymbol{e}^i`$。
配对是：$`\boldsymbol{x} = x_i\boldsymbol{e}^i = x^i\boldsymbol{e}_i`$
爱因斯坦求和，从输入和输出看，与点乘一致，但是一个拼出向量，另一个是提取分量

**张量（2 阶张量）**
特征：有两个指标。(逆变，协变或混合)
类型：根据上下标的数量，分为不同(p,q)(p个逆变指标，q个协变指标) 型的张量，其中上下标都有者称混合张量。

# 看到这了

**常见2阶张量类型**
克罗内克符号 $`\delta^j_i`$
是 2 阶张量，1 阶逆变（上标 $`j`$），1 阶协变（下标 $`i`$）。
又称为$`(1,1)`$ 阶混合张量。

$`(2,0)`$ 阶张量（两个指标都是上标）
坐标变换满足：$`T^{\mu\nu} = \frac{\partial x^\mu}{\partial \bar{x}^\alpha} \frac{\partial x^\nu}{\partial \bar{x}^\beta} \bar{T}^{\alpha\beta}`$

$`(1,1)`$ 阶张量（一个上标，一个下标）
 坐标变换满足：$`T^\mu_\nu = \frac{\partial x^\mu}{\partial \bar{x}^\alpha} \frac{\partial \bar{x}^\beta}{\partial x^\nu} \bar{T}^\alpha_\beta`$

## 3. 核心问题：矩阵是如何表示线性变换的？

矩阵可以表示线性变换，但其张量属性取决于**“变什么”**：

- **基底不变，更改坐标**：
  - 矩阵元构成 **$`(2,0)`$ 阶张量**（两个上标）。
  - 因为坐标变了，但基底没变，变换矩阵需要两个逆变指标来适应坐标的变换。
- **坐标不变，更改基底**：
  - 矩阵元构成 **$`(0,2)`$ 阶张量**（两个下标）。
  - 因为基底变了，变换矩阵需要两个协变指标来适应基底的变换。典型例子是度规张量 $`g_{ij}`$。

## 4. 总结
| 张量类型 | 阶数 | 指标数量 | 协变/逆变属性 | 典型例子 |
| :--- | :--- | :--- | :--- | :--- |
| 标量 | 0阶 | 0 | 无 | 温度、质量 |
| 矢量 | 1阶 | 1 | 1个指标 | 位移、速度 |
| 张量 | 2阶 | 2 | 2个指标 | 应力、度规、线性变换矩阵 |