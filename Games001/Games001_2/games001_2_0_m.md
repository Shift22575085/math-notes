# 矩阵分解

$$A=
\begin{pmatrix}
9&6&0\\\\
6&5&4\\\\
3&4&10
\end{pmatrix}$$

第一步：得到 $`A_0`$ $`E_0`$

这三步都用到了高斯消元

$$A_0=\begin{pmatrix}9&6&0\\\\0&1&4\\\\3&4&10\end{pmatrix}=\begin{pmatrix}1&0&0\\\\-\frac23&1&0\\\\0&0&1\end{pmatrix}A$$

$$E_0=
\begin{pmatrix}
1&0&0\\\\
-\frac23&1&0\\\\
0&0&1
\end{pmatrix}$$

$$A_0=E_0A$$

第二步：得到 $`A_1`$ $`E_1`$

$$A_1=\begin{pmatrix}9&6&0\\\\0&1&4\\\\0&2&10\end{pmatrix}=\begin{pmatrix}1&0&0\\\\0&1&0\\\\-\frac13&0&1\end{pmatrix}A_0$$

$$E_1=
\begin{pmatrix}
1&0&0\\\\
0&1&0\\\\
-\frac13&0&1
\end{pmatrix}$$

$$A_1=E_1A_0$$

第三步：得到 $`A_2`$(上三角) $`E_2`$

$$A_2=\begin{pmatrix}9&6&0\\\\0&1&4\\\\0&0&10\end{pmatrix}=\begin{pmatrix}1&0&0\\\\0&1&0\\\\0&-2&1\end{pmatrix}A_1$$

$$E_2=
\begin{pmatrix}
1&0&0\\\\
0&1&0\\\\
0&-2&1
\end{pmatrix}$$

$`A_2=E_2A_1`$

得到上三角矩阵 $`U`$

$$U=A_2=E_2E_1E_0A=
\begin{pmatrix}
9&6&0\\\\
0&1&4\\\\
0&0&2
\end{pmatrix}$$

求L(下三角)

$`U=E_2E_1E_0A`$

两边左乘 $`(E_2E_1E_0)^{-1}`$：

$$(E_2E_1E_0)^{-1}U
=
(E_2E_1E_0)^{-1}E_2E_1E_0A$$

$$A=(E_2E_1E_0)^{-1}U$$

$$L=(E_2E_1E_0)^{-1}=E_0^{-1}E_1^{-1}E_2^{-1}$$

$${
L=E_0^{-1}E_1^{-1}E_2^{-1}
}$$

$$L=
\begin{pmatrix}
1&0&0\\\\
2/3&1&0\\\\
1/3&2&1
\end{pmatrix}$$

PLU分解(P为初等变换矩阵)：

$$A=PLU$$

# 实对称正定矩阵 $`U=L^T`$

## 1. 从 LU 分解开始

已知：

$$A=LU$$

$$(AB)^T=B^TA^T$$

$`A`$ 是实对称矩阵可得：

$$A=A^T$$

$$A^T=(LU)^T$$

$$A^T=U^TL^T$$

$$A=U^TL^T$$

## 2. 得到两个 LU 形式的分解

现在我们有：

$${A=LU}$$

$${A=U^TL^T}$$

观察矩阵的结构：

$$L：\text{下三角矩阵}$$

$$U：\text{上三角矩阵}$$

$$U^T：\text{下三角矩阵}$$

$$L^T：\text{上三角矩阵}$$

因此，这两个实际上都是：

$`{\text{下三角}\times\text{上三角}}`$

形式的分解。

## 3. 利用 LU 分解的唯一性

如果规定 $`L`$ 的对角线元素为正数，那么这种规范化的 LU 分解具有唯一性。

因此：

$$A=LU$$

$$A=U^TL^T$$

既然都是满足规定条件的 LU 分解，那么根据唯一性，两者必须相同。

$${U=L^T}$$

# 乔里斯基分解

给定矩阵：

$$A=
\begin{pmatrix}
4&2&2\\\\
2&5&1\\\\
2&1&6
\end{pmatrix}$$

这个矩阵是实对称正定矩阵，所以可以进行乔里斯基分解：

$$A=LU$$

$${U=L^T}$$

$${A=LL^T}$$

求 $`L`$； 因为 $`L`$ 是下三角矩阵，设：

$$L=
\begin{pmatrix}
l_{11}&0&0\\\\
l_{21}&l_{22}&0\\\\
l_{31}&l_{32}&l_{33}
\end{pmatrix}$$

$$L^T=
\begin{pmatrix}
l_{11}&l_{21}&l_{31}\\\\
0&l_{22}&l_{32}\\\\
0&0&l_{33}
\end{pmatrix}$$

## 计算 $`LL^T`$

$$LL^T=
\begin{pmatrix}
l_{11}^2&
l_{11}l_{21}&
l_{11}l_{31}\\\\
l_{11}l_{21}&
l_{21}^2+l_{22}^2&
l_{21}l_{31}+l_{22}l_{32}\\\\
l_{11}l_{31}&
l_{21}l_{31}+l_{22}l_{32}&
l_{31}^2+l_{32}^2+l_{33}^2
\end{pmatrix}$$

$$LL^T=A$$

$$\begin{pmatrix}
l_{11}^2&
l_{11}l_{21}&
l_{11}l_{31}\\\\
l_{11}l_{21}&
l_{21}^2+l_{22}^2&
l_{21}l_{31}+l_{22}l_{32}\\\\
l_{11}l_{31}&
l_{21}l_{31}+l_{22}l_{32}&
l_{31}^2+l_{32}^2+l_{33}^2
\end{pmatrix}
=
\begin{pmatrix}
4&2&2\\\\
2&5&1\\\\
2&1&6
\end{pmatrix}$$

然后逐个求 $`l_{ij}`$。

## 1. 求第一行

求 $`l_{11}`$

$$l_{11}^2=4$$

$${l_{11}=2}$$

求 $`l_{21}`$

$$l_{11}l_{21}=2$$

$$2l_{21}=2$$

$${l_{21}=1}$$

求 $`l_{31}`$

$$l_{11}l_{31}=2$$

$$2l_{31}=2$$

$${l_{31}=1}$$

## 2. 求第二行

求 $`l_{22}`$

$$l_{21}^2+l_{22}^2=5$$

$$1+l_{22}^2=5$$

$$l_{22}^2=4$$

$${l_{22}=2}$$

求 $`l_{32}`$

$$l_{21}l_{31}+l_{22}l_{32}=1$$

$$1\times1+2l_{32}=1$$

$$2l_{32}=0$$

$${l_{32}=0}$$

## 3. 求第三行 $`l_{33}`$

$$l_{31}^2+l_{32}^2+l_{33}^2=6$$

$$1^2+0^2+l_{33}^2=6$$

$$l_{33}^2=5$$

$${l_{33}=\sqrt5}$$

## 4. 最终得到 $`L`$

$${
L=
\begin{pmatrix}
2&0&0\\\\
1&2&0\\\\
1&0&\sqrt5
\end{pmatrix}
}$$

$`L^T=`$：

$${
L^T=
\begin{pmatrix}
2&1&1\\\\
0&2&0\\\\
0&0&\sqrt5
\end{pmatrix}
}$$

最终乔里斯基分解：

$${
A=
\begin{pmatrix}
2&0&0\\\\
1&2&0\\\\
1&0&\sqrt5
\end{pmatrix}
\begin{pmatrix}
2&1&1\\\\
0&2&0\\\\
0&0&\sqrt5
\end{pmatrix}
}$$

## 5. 验证

$$LL^T=
\begin{pmatrix}
2&0&0\\\\
1&2&0\\\\
1&0&\sqrt5
\end{pmatrix}
\begin{pmatrix}
2&1&1\\\\
0&2&0\\\\
0&0&\sqrt5
\end{pmatrix}$$

$$LL^T=
\begin{pmatrix}
4&2&2\\\\
2&5&1\\\\
2&1&6
\end{pmatrix}
=A$$

$${A=LL^T}$$

# 快速求解稀疏矩阵

## 例子

一个矩阵可以同时具有两个属性：稀疏 + 实对称正定。

$$A=
\begin{pmatrix}
4&2&0&0\\\\
2&5&1&0\\\\
0&1&6&2\\\\
0&0&2&7
\end{pmatrix}$$

它既是稀疏矩阵，又是实对称正定矩阵。

求$`{x}`$(求解矩阵方程)

$${Ax=b}$$

如果直接解：

我们可以进行普通的高斯消元。

但如果知道：

$$A=LL^T$$

$$Ax=b$$

$$LL^Tx=b$$

$${Ly=b}$$

$${L^Tx=y}$$

最后得到 $`x`$,这样更方便。

因为 $`L`$ 是下三角矩阵：

$$L=
\begin{pmatrix}
*&0&0\\\\
*&*&0\\\\
*&*&*
\end{pmatrix}$$

$`Ly=b`$ 非常容易求，可以直接从上往下计算。

$`L^T`$是上三角矩阵：

$$L^T=
\begin{pmatrix}
*&*&*\\\\
0&*&*\\\\
0&0&*
\end{pmatrix}$$

$`L^Tx=y`$可以直接从下往上计算。

## 为何更快

假设 $`A`$ 不变，但是有很多个 $`b`$：

$$Ax_1=b_1$$

$$Ax_2=b_2$$

$$Ax_3=b_3$$

$$\cdots$$

可以先做一次：

$${A=LL^T}$$

之后每次只需要：

$$Ly_i=b_i$$

$$L^Tx_i=y_i$$

### 稀疏如何发生作用：

$`A`$ 是一个 $`10000\times10000`$ 的矩阵。

理论上有$`100\thinspace000\thinspace000`$ 个元素。

但如果其中99.9% 都是 $`0`$，那么实际上只有很少的元素需要参与计算。

稀疏性:少存、少算

正定 + 对称:可以使用 Cholesky

稀疏 + 实对称正定:可以用稀疏 Cholesky 高效求解

# 矩阵分解

### 施密特正交化

#### TODO课程上有另一种解法

QR 分解: $`\boldsymbol A = \boldsymbol Q\boldsymbol R`$

要求: $`\boldsymbol A_{m\times n}`$ 列满秩，$`m \ge n`$

$`\boldsymbol Q_{m\times m}`$ 为幺正矩阵，$`\boldsymbol R_{m\times n}`$ 为上三角矩阵

分解矩阵：A

$$A=\begin{pmatrix}1&1\\\\1&0\\\\0&1\end{pmatrix}$$

$$a_1=\begin{pmatrix}1\\\\1\\\\0\end{pmatrix},\qquad a_2=\begin{pmatrix}1\\\\0\\\\1\end{pmatrix}$$

规范化$`a1`$
$`\Vert a_1\Vert=\sqrt{1^2+1^2}=\sqrt2`$

$$q_1=\frac{a_1}{\sqrt2}=\begin{pmatrix}1/\sqrt2\\\\1/\sqrt2\\\\0\end{pmatrix}$$

去掉$`a2`$ 上与$`a1`$平行的部分并规整化得到$`w2`$

$`\langle a_2,q_1\rangle=\frac{1}{\sqrt2}`$

得到投影长度:

$$\langle a_2,q_1\rangle q_1=\begin{pmatrix}1/2\\\\1/2\\\\0\end{pmatrix}$$

$`a2`$去掉$`a1`$在$`a2`$上的投影长度：

$$w_2=a_2-\begin{pmatrix}1/2\\\\1/2\\\\0\end{pmatrix}=\begin{pmatrix}1/2\\\\-1/2\\\\1\end{pmatrix}$$

规范化$`w2`$

$`\Vert w_2\Vert=\sqrt{\frac14+\frac14+1}=\frac{\sqrt6}{2}`$

$$q_2=\frac{w_2}{\Vert w_2\Vert}=\begin{pmatrix}1/\sqrt6\\\\-1/\sqrt6\\\\2/\sqrt6\end{pmatrix}$$

所以：

$$Q=\begin{pmatrix}1/\sqrt2&1/\sqrt6\\\\1/\sqrt2&-1/\sqrt6\\\\0&2/\sqrt6\end{pmatrix}$$

第 5 步：算 R

$$R=Q^T A=\begin{pmatrix}\langle q_1,a_1\rangle&\langle q_1,a_2\rangle\\\\0&\langle q_2,a_2\rangle\end{pmatrix}=\begin{pmatrix}\sqrt2&1/\sqrt2\\\\0&\sqrt6/2\end{pmatrix}$$

验证:

$$QR=\begin{pmatrix}1/\sqrt2&1/\sqrt6\\\\1/\sqrt2&-1/\sqrt6\\\\0&2/\sqrt6\end{pmatrix}\begin{pmatrix}\sqrt2&1/\sqrt2\\\\0&\sqrt6/2\end{pmatrix}=\begin{pmatrix}1&1\\\\1&0\\\\0&1\end{pmatrix}=A$$

最后结果:

$$A=\underbrace{\begin{pmatrix}1/\sqrt2&1/\sqrt6\\\\1/\sqrt2&-1/\sqrt6\\\\0&2/\sqrt6\end{pmatrix}}_{Q}\underbrace{\begin{pmatrix}\sqrt2&1/\sqrt2\\\\0&\sqrt6/2\end{pmatrix}}_{R}$$

TODO：当前的是经济型分解，这一步里的Q不算幺正矩阵，为Q再补上一个垂直的才算幺正矩阵

得到第三列：

由$`q3^Tq2=0,q3^Tq2=0`$计算

$$\begin{pmatrix} x & y & z \end{pmatrix} \begin{pmatrix} \dfrac{1}{\sqrt{2}} \\\\ \dfrac{1}{\sqrt{2}} \\\\ 0 \end{pmatrix} = 0$$

得到$`y=-x`$

$$\begin{pmatrix} x & y & z \end{pmatrix} \begin{pmatrix} \dfrac{1}{\sqrt{6}} \\\\ -\dfrac{1}{\sqrt{6}} \\\\ \dfrac{2}{\sqrt{6}} \end{pmatrix} = 0$$

代入$`y=-x`$

得$`x,y,z`$为$`1，-1，-1`$

规整向量长度为1

得$`x,y,z`$为$`√1，√-1，√-1`$

求U向量的公式(未规整化的Q)

$$u_k = a_k - \sum_{j=1}^{k-1} \frac{\langle a_k, u_j \rangle}{\langle u_j, u_j \rangle} u_j$$

K=1时，J>k-1,求和为0，uk=ak

K不为1时，后面算的就是投影，点乘完再除以u的模长再乘以u得到投影,多个向量时把前面几个的投影加起来，用A减去后就能得到与前面所有向量垂直的向量，不过未规范

### 吉文斯矩阵分解

#### TODO 例子值对吗

$$A= \begin{pmatrix} 3 & 2 & 1 \\\\ 4 & 6 & 5 \\\\ 0 & 7 & 8 \end{pmatrix}$$

消去第 2 行第 1 列的元素 4

$$\begin{pmatrix} 3 \\\\ 4 \end{pmatrix}$$

$`r_1=\sqrt{3^2+4^2}=5`$

$`c_1=\frac{3}{5},\quad s_1=\frac{4}{5}`$

吉文斯需要的是角度顺时针旋转让所需的角度在这个位置归零，所以负值在左下角

$$G_1= \begin{pmatrix} \frac{3}{5} & \frac{4}{5} & 0 \\\\ -\frac{4}{5} & \frac{3}{5} & 0 \\\\ 0 & 0 & 1 \end{pmatrix}$$

$$G_1A= \begin{pmatrix} \dfrac{3}{5} & \dfrac{4}{5} & 0 \\\\ -\dfrac{4}{5} & \dfrac{3}{5} & 0 \\\\ 0 & 0 & 1 \end{pmatrix} \begin{pmatrix} 3 & 2 & 1 \\\\ 4 & 6 & 5 \\\\ 0 & 7 & 8 \end{pmatrix}$$

$$G_1A= \begin{pmatrix} 5 & 6 & \frac{23}{5} \\\\ 0 & 2 & \frac{11}{5} \\\\ 0 & 7 & 8 \end{pmatrix}$$

消去第 3 行第 2 列的元素 7

$$\begin{pmatrix} 2 \\\\ 7 \end{pmatrix}$$

$`r_2=\sqrt{2^2+7^2}=\sqrt{53}`$

$`c_2=\frac{2}{\sqrt{53}},\quad s_2=\frac{7}{\sqrt{53}}`$

$$G_2= \begin{pmatrix} 1 & 0 & 0 \\\\ 0 & \dfrac{2}{\sqrt{53}} & \dfrac{7}{\sqrt{53}} \\\\ 0 & -\dfrac{7}{\sqrt{53}} & \dfrac{2}{\sqrt{53}} \end{pmatrix}$$

$$G_2(G_1A)= \begin{pmatrix} 1 & 0 & 0 \\\\ 0 & \dfrac{2}{\sqrt{53}} & \dfrac{7}{\sqrt{53}} \\\\ 0 & -\dfrac{7}{\sqrt{53}} & \dfrac{2}{\sqrt{53}} \end{pmatrix} \begin{pmatrix} 5 & 6 & \dfrac{23}{5} \\\\ 0 & 2 & \dfrac{11}{5} \\\\ 0 & 7 & 8 \end{pmatrix}$$

$$R= \begin{pmatrix} 5 & 6 & \dfrac{23}{5} \\\\ 0 & \sqrt{53} & \dfrac{302}{5\sqrt{53}} \\\\ 0 & 0 & \dfrac{3}{5\sqrt{53}} \end{pmatrix} =G_2(G_1A)$$

计算Q矩阵

$`G_2G_1A = R`$

$`A = (G_2G_1)^{-1}R = G_1^{-1}G_2^{-1}R`$

由于吉文斯矩阵是正交矩阵，$`G^{-1}=G^T`$，所以：
$`A = G_1^T G_2^T R`$

因此：
$`Q = G_1^T G_2^T`$

即：

$$Q= \begin{pmatrix} \dfrac{3}{5} & -\dfrac{4}{5} & 0 \\\\ \dfrac{4}{5} & \dfrac{3}{5} & 0 \\\\ 0 & 0 & 1 \end{pmatrix} \begin{pmatrix} 1 & 0 & 0 \\\\ 0 & \dfrac{2}{\sqrt{53}} & -\dfrac{7}{\sqrt{53}} \\\\ 0 & \dfrac{7}{\sqrt{53}} & \dfrac{2}{\sqrt{53}} \end{pmatrix}$$

### TODO 豪斯霍尔德变换

# 矩阵中负值出现的规律

旋转会先旋转矩阵的行，后面是列，后旋转的部分会出现负值(逆时针下)

xy平面下

$$\begin{pmatrix} \cos\theta & -\sin\theta \\\\ \sin\theta & \cos\theta \end{pmatrix}$$

3*3矩阵中zx平面

$$R_y(\theta)= \begin{pmatrix} \cos\theta & 0 & \sin\theta \\\\ 0 & 1 & 0 \\\\ -\sin\theta & 0 & \cos\theta \end{pmatrix}$$

yz平面

$$R_x(\theta)= \begin{pmatrix} 1 & 0 & 0 \\\\ 0 & \cos\theta & -\sin\theta \\\\ 0 & \sin\theta & \cos\theta \end{pmatrix}$$

# 奇异值分解

奇异值分解(Singular value decomposition, SVD)

<img src="./SVD.png" width="300"/>

$`U_{m\times m}`$ 为幺正矩阵，$`V_{n\times n}`$ 为幺正矩阵，$`\Sigma_{m\times n}`$ 为对角矩阵

$$A= \begin{pmatrix} 0 & 2 \\\\ 1 & 0 \end{pmatrix}$$

求V

A^(T)A的特征向量组成的矩阵为V

$$A^\mathrm{T}A=
\begin{pmatrix}
0 & 1 \\\\
2 & 0
\end{pmatrix}
\begin{pmatrix}
0 & 2 \\\\
1 & 0
\end{pmatrix}
=
\begin{pmatrix}
1 & 0 \\\\
0 & 4
\end{pmatrix}$$

约定特征值大的在前面，奇异值要按照降序排序

将得到的特征值 $`\lambda = 4, 1`$ 代入 $`A^{T}A - \lambda E`$，得到特征向量为 $`(0,1), (1,0)`$，将得到的特征向量列填入 $`V`$ 矩阵：

$$V = \begin{pmatrix} 0 & 1 \\\\ 1 & 0 \end{pmatrix}$$

求 $`\Sigma`$：

特征值：$`4, 1`$  
奇异值（根号下特征值）：$`2, 1`$

$$\Sigma = \begin{pmatrix} 2 & 0 \\\\ 0 & 1 \end{pmatrix}$$

$`A^TA`$的特征值的平方根，组成奇异值 $`\Sigma`$。

求 $`U`$：

$`A = U \Sigma V^{H}`$

$`V`$ 为幺正矩阵，取值范围为实数，$`V^{H} = V^{T} = V^{-1}`$。

$`AV = U \Sigma`$

$`AV \Sigma^{-1} = U`$

$$AV=
\begin{pmatrix}
0 & 2 \\\\
1 & 0
\end{pmatrix}
\begin{pmatrix}
0 & 1 \\\\
1 & 0
\end{pmatrix}
=
\begin{pmatrix}
2 & 0 \\\\
0 & 1
\end{pmatrix}$$

$$\Sigma^{-1}=
\begin{pmatrix}
\dfrac12 & 0 \\\\
0 & 1
\end{pmatrix}$$

$$U=
\begin{pmatrix}
2 & 0 \\\\
0 & 1
\end{pmatrix}
\begin{pmatrix}
\dfrac12 & 0 \\\\
0 & 1
\end{pmatrix}
=
\begin{pmatrix}
1 & 0 \\\\
0 & 1
\end{pmatrix}$$

验证：

$$U\Sigma V^\mathrm{T}=
\begin{pmatrix}
1 & 0 \\\\
0 & 1
\end{pmatrix}
\begin{pmatrix}
2 & 0 \\\\
0 & 1
\end{pmatrix}
\begin{pmatrix}
0 & 1 \\\\
1 & 0
\end{pmatrix}
=
\begin{pmatrix}
0 & 2 \\\\
1 & 0
\end{pmatrix}
=A$$

奇异三元组

每个奇异值 $`\sigma_i`$ 同时对应一个左奇异向量 $`u_i`$ 和一个右奇异向量 $`v_i`$，它们三者共同组成一个

$$A = \sum_{i} \sigma_i u_i v_i^H$$

$$A v_i = \sigma_i u_i$$

所有的奇异三元组组合起来，组成了奇异值分解的公式$`A = U \Sigma V^{H}`$

#### TODO推广到3*3矩阵

### 公式推导
奇异值分解的推导，几何意义
A矩阵
奇异值分解中，V是$`A^TA`$矩阵的拉伸方向，是原矩阵的特征向量组成的矩阵，最终公式中取V转置原因
:
A^TA的特征向量组成的矩阵，是矩阵A的输入旋转方向的逆，是奇异值中的V，最终公式中取转置的原因是，旋转矩阵的转置和逆相等

西格玛是原矩阵A^TA的特征值的根号下，代表A矩阵的拉伸长度
U是由原矩阵，V矩阵，西格玛矩阵求出的

右奇异向量 **$`V`$** 是 **$`A^T A`$** 的特征向量，对应输入空间（行空间）的自相关。
左奇异向量 **$`U`$** 是 **$`A A^T`$** 的特征向量，对应输出空间（列空间）的自相关。

V将单位向量转到拉伸方向
西格玛拉伸矩阵
将拉伸后的矩阵转到和A一样
U和V没有数值上的关系

特征分解
拿到特征值组成的矩阵V，先通过V^(-1)将矩阵转到标准正交基，再拉伸，拉伸完成后通过V将矩阵变换回原来的方向

拉伸长度的平方是AA^T和A^TA的特征值
特征值有两个而矩阵是3*3的情况下，得到0特征值

#### TODO：若 $`m = n`$

则有 $`\sqrt{A^\mathrm{H}A} = \sqrt{V\Sigma^2 V^\mathrm{H}} = V|\Sigma|V^\mathrm{H}`$

# 向量范数

正定性：

$$\Vert u\Vert\ge0,\quad \Vert u\Vert=0 \iff u=0$$

正齐次性：

$$\Vert au\Vert=|a|\Vert u\Vert,\quad a\in\mathbb{R}$$

三角不等式：

$$\Vert u+v\Vert\le\Vert u\Vert+\Vert v\Vert$$

$`L_0`$ 范数：非零元素的个数(伪范数，不满足正齐次性)
不能构成度量函数；本质上不是范数
不可导；作为优化目标时性能非常低下
$`\Vert\boldsymbol x\Vert_0 = 2`$（因为 3 和 $`-4`$ 非零，$`0`$ 是零）
$`\Vert\boldsymbol{x}\Vert_0 = \sum_{i=1}^{n}[x_i \neq 0]`$

$`L_1`$ 范数：绝对值之和
$`\Vert\boldsymbol x\Vert_1 = |3| + |-4| + |0| = 3 + 4 + 0 = 7`$
$`\Vert\boldsymbol{x}\Vert_1 = \sum_{i=1}^{n}|x_i| = |x_1| + |x_2| + \dots + |x_n|`$

$`L_2`$ 范数：平方和开根号
$`\Vert\boldsymbol x\Vert_2 = \sqrt{3^2 + (-4)^2 + 0^2} = \sqrt{9 + 16} = 5`$
$`\Vert\boldsymbol{x}\Vert_2 = \sqrt{\sum_{i=1}^{n}x_i^2} = \left(x_1^2 + x_2^2 + \dots + x_n^2\right)^{\frac12}`$

$`L_p`$ 范数：如果取 $`p=3`$，则
$`L_3 = \big(|3|^3 + |-4|^3 + 0\big)^{1/3} = (27 + 64)^{1/3} \approx 4.5`$
$`\Vert\boldsymbol{x}\Vert_p = \left(|x_1|^p + |x_2|^p + \dots + |x_n|^p\right)^{\frac1p} \quad (p \ge 1)`$

$`L_\infty`$ 范数：绝对值最大分量
$`\Vert\boldsymbol x\Vert_\infty = \max\lbrace3,4,0\rbrace = 4`$
$`\Vert\boldsymbol{x}\Vert_\infty = \max\lbrace|x_1|,|x_2|,\dots,|x_n|\rbrace`$

# 矩阵范数

诱导范数

$`\Vert A\Vert = \max\lbrace\Vert Ax\Vert: x \in \mathbb R^n,\Vert x\Vert = 1\rbrace = \max\left\lbrace\frac{\Vert Ax\Vert}{\Vert x\Vert}: x \in \mathbb R^n,\Vert x\Vert \neq 0\right\rbrace`$

前一个公式说的是，模长为1的x向量，被A变换后最大长度
后一个公式说的是，模长不为0的向量，被A变换后再除以x的模长，之后再找到最大的长度
二者等价，都是找到最大长度的向量与矩阵
直接去拿到奇异值分解中西格玛矩阵的左上角的值，就是诱导范数(求$`L_2`$时可用)

由向量的Lp范数可以得到矩阵的诱导Lp范数
先有“向量尺子”，才有“矩阵大小”，矩阵的尺子完全听命于向量的尺子，所以叫“诱导”。

A作为线性变换所产生的对向量模长的的最大放大倍数。
不同于物理中的模长，数学中的模长是范数，对除了$`L_0`$外的所有矩阵都成立

## 作业

$$\Vert A\Vert_1 = \max_{1\le j\le n}\sum_{i=1}^{m}|a_{ij}| \quad(\boldsymbol A\text{ 的所有列向量的最大绝对值和})$$

$$\Vert A\Vert_2 = \sigma_{\max}(A) \quad(\boldsymbol A\text{ 的最大奇异值，故该范数又称为谱范数})$$

$$\Vert A\Vert_\infty = \max_{1\le i\le m}\sum_{j=1}^{n}|a_{ij}| \quad(\boldsymbol A\text{ 的所有行向量的最大绝对值和})$$

$`\displaystyle \Vert A\Vert_p = \max\left\lbrace\frac{\Vert Ax\Vert_p}{\Vert x\Vert_p}: x \in \mathbb R^n,\Vert x\Vert \neq 0\right\rbrace`$

所有x分量被A变换后的$`\Vert \cdot \Vert_p`$的除以X向量所有分量的$`\Vert \cdot \Vert_p`$，公式上是省略了西格玛符号

完整公式(不同L的展开形式将不同)：

$`\Vert A\Vert_p = \max \left\lbrace \frac{ \left( \sum_{i=1}^{m} |(Ax)_i|^p \right)^{1/p} }{ \left( \sum_{j=1}^{n} |x_j|^p \right)^{1/p} } : x \in \mathbb{R}^n, x \neq 0 \right\rbrace`$

#### TODO不同展开什么样子,上面公式看不懂

## 谱半径VS谱范数
#### TODO作用是什么

谱范数
$`\Vert A\Vert_2=`$最大奇异值$`A^TA`$的特征值开根号

谱半径
$`\rho(A)=`$最大特征值

# 向量与矩阵的范数

## 元素形式范数

把矩阵展平成向量 → 得到逐元素范数；把矩阵看成线性算子 → 得到诱导算子范数

### 和范数，$`L_1`$范数

$`\Vert A\Vert_{1,\mathrm{entry}} = \Vert\operatorname{vec}(A)\Vert_1 = \sum_{i=1}^{m}\sum_{j=1}^{n}|a_{ij}|`$

矩阵中所有绝对值之和,和向量L1一样

### Frobenius 范数(Schur 范数)

$`\Vert A\Vert_F=\left(\sum_{i=1}^m\sum_{j=1}^n a_{ij}^2\right)^{1/2}`$

$`\Vert A\Vert_F^2=\operatorname{tr}(A^\mathrm{T}A)`$

矩阵的所有值的平方的开根号，或者是$`A^TA`$的迹(这个等于Frobenius 范数的平方)，手推下就能发现这两个算的东西一样

### Euclidean 范数(欧几里得范数)

$`\Vert x\Vert_2 = \sqrt{\sum_{i=1}^n x_i^2}`$

向量每个值的平方的和的开方，向量长度。

如果将矩阵展开成一个向量，那么Euclidean 范数=Frobenius 范数

### $`L_2,`$ $`L_\infty`$ 

欧几里得范数，$`L_\infty`$ 范数和向量一致

## 沙滕 (Schatten) 范数

不随幺正变换而改变的范数

$$\Vert\boldsymbol{A}\Vert_p
=
\left(
\sum_{i=1}^{\max\lbrace m,n\rbrace}
\sigma_i^p
\right)^{1/p}$$

（$`\sigma_i`$ 为奇异值）

直接将值代入p,可以得到不同的范数，$`p_1`$核范数，$`p_2`$Frobenius范数，$`p_2`$Schatten3范数

p为无限的时候，这个取极限值

$$\Vert\boldsymbol{A}\Vert_\infty
=
\lim_{p \to \infty}
\left(
\sum_{i=1}^{\max\lbrace m,n\rbrace} \sigma_i^p
\right)^{1/p}
=
\max_{1 \le i \le \max\lbrace m,n\rbrace} \sigma_i
= 3$$