
# $\VertA\Vert_1 = \max_{1\le j\le n}\sum_{i=1}^m |a_{ij}|$

$$\VertA\Vert_1 = \max_{1\le j\le n}\sum_{i=1}^{m}|a_{ij}| \quad(\boldsymbol A\text{ 的所有列向量的最大绝对值和})$$

迭代i->m,迭代行，迭代的是行，则获得所有列加起来的量，之后以列j为下标，得到最大值，找到列向量绝对值之和中最大的那一项

就是这些输入值与A的组合再除以输入值得到的值，不会大于最大列的和

证明：这个证明的其实就是矩阵变换后的最大L1，就是矩阵列最大绝对值之和

## 定义：最大拉伸比例，结论：最大列绝对值之和。

## 第一步：证明对向量的拉伸倍数 ≤ 最大列和

把矩阵 $A$ 写成列向量的形式：
$A = [c_1, c_2, \cdots, c_n]$
其中 $c_j$ 是第 $j$ 列。

那么
$Ax = x_1 c_1 + x_2 c_2 + \cdots + x_n c_n$

最终出来的结果是列向量$Ax$，X1，X2是向量第一，第二的值，c1,c2是矩阵的列

两边取 $L_1$ 范数（绝对值求和），根据三角不等式：

Ax列向量的L1范数一定小于A矩阵的列的L1范数乘X向量中对应的值的所有值之和

直线距离最短，中间的段加起来绝对比直线距离长，可得公式1：

公式1：

$\VertAx\Vert_1 \le |x_1| \Vertc_1\Vert_1 + |x_2| \Vertc_2\Vert_1 + \cdots + |x_n| \Vertc_n\Vert_1$

令$M = \max_{1\le j\le n} \Vertc_j\Vert_1$

$M  = \max_{1 \le j \le n} \sum_{i=1}^{m} |a_{ij}|$最大列和

则有所有的$\Vertc_j\Vert_1 \le M$，可以等于M

将公式1中所有的C项替换为M

$\VertAx\Vert_1 \le M \bigl( |x_1| + |x_2| + \cdots + |x_n| \bigr) = M \Vertx\Vert_1$

因此
$\frac{\VertAx\Vert_1}{\Vertx\Vert_1} \le M$
上界证完。

## 第二步：证明能达到这个上界

假设第 $k$ 列的列和 $M$ 最大。取向量 $x$ 为只在第 $k$ 个位置为 1、其余为 0 的单位向量（即 $x = e_k$）。

$e_k$：除了第 k 位是 1，其他全是 0 的向量

此时
$\Vertx\Vert_1 = 1$(只在k的位置有个1，其他位置是0)
而
$Ax = A e_k = c_k=$(最大列和的列本身，c是A的列)
即结果恰好是矩阵的第 $k$ 列。

所以比值
$\frac{\VertAx\Vert_1}{\Vertx\Vert_1} = \frac{\Vertc_k\Vert_1}{1} = M$

当变换的向量是在最大列处为1，其余为0的情况时，达到上界，矩阵对向量的拉伸最大。

结论：$\displaystyle \VertA\Vert_1 = \max_{1\le j\le n}\sum_{i=1}^m |a_{ij}|$ 证毕。


# 证明 $\VertA\Vert_\infty = \max_{1\le i\le m} \sum_{j=1}^n |a_{ij}|$

$$\VertA\Vert_\infty = \max_{1\le i\le m}\sum_{j=1}^{n}|a_{ij}| \quad(\boldsymbol A\text{ 的所有行向量的最大绝对值和})$$


## 第一步：证明放大倍数 ≤ 最大行和

把矩阵 $A$ 的行向量记为：
$$r_1, r_2, \cdots, r_m$$
（每一行是一个横向量）。那么 $Ax$ 的第 $i$ 个分量是点积：
$$(Ax)_i = r_i \cdot x$$
根据绝对值不等式（点积绝对值 ≤ 各分量绝对值乘积之和）：

把有负，有正的全部拉到正值，则乘积之和必定比有正有负的点积值大

$$|(Ax)_i| \le |a_{i1}||x_1| + |a_{i2}||x_2| + \cdots + |a_{in}||x_n|$$

$L_\infty$的定义就是向量中的值的绝对值的最大项

因为 $L_\infty$ 范数 $\Vertx\Vert_\infty = \max\limits_{1\le j\le n} |x_j|$，所以每个分量都满足：
$$|x_j| \le \Vertx\Vert_\infty$$

于是第 $i$ 行绝对值的和满足：

中间的求和逻辑是矩阵A的i不变，列向量(j)的绝对值求和

$|(Ax)_i| \le \left( \sum_{j=1}^n |a_{ij}| \right) \cdot \Vertx\Vert_\infty \le M \cdot \Vertx\Vert_\infty$

其中：

$M = \max_{1\le i\le m} \sum_{j=1}^n |a_{ij}|$即最大的绝对行和。

将等式右边规整为绝对行和$M$和$L_\infty$范数，右边公式的上界可以达到这个值。

既然每一个分量都满足 $|(Ax)_i| \le M \cdot \Vertx\Vert_\infty$，那么它们当中的最大值也满足：

$\VertAx\Vert_\infty \le M \cdot \Vertx\Vert_\infty$

因此放大倍数：
$$\frac{\VertAx\Vert_\infty}{\Vertx\Vert_\infty} \le M$$

上界证完。

## 第二步：证明能达到这个上界

假设第 $k$ 行的行和 $M$ 最大。我们构造一个特殊的向量 $x$：

取 $x_j$ 的符号（正负号）与第 $k$ 行的元素 $a_{kj}$ 完全一致，并且让每个分量的模长都取最大值1,为了让对应的点乘值绝对不为负值：

$$|x_j| = 1$$

于是：
$$\Vertx\Vert_\infty = 1$$

此时第 $k$ 行的点积为：
$$|(Ax)_k| = |a_{k1}x_1 + a_{k2}x_2 + \cdots + a_{kn}x_n|$$
由于每个 $x_j$ 的符号与 $a_{kj}$ 一致，所以每一项的乘积 $a_{kj}x_j$ 都等于 $|a_{kj}|$，因此：

$$|(Ax)_k| = |a_{k1}| + |a_{k2}| + \cdots + |a_{kn}| = M$$

因为其他任何一行的点积绝对值都不会超过该行的行和，而行和最大也才 $M$，所以整个向量 $Ax$ 的 $L_\infty$ 范数（所有分量绝对值的最大值）正好就是：
$$\VertAx\Vert_\infty = M$$

因此：
$$\frac{\VertAx\Vert_\infty}{\Vertx\Vert_\infty} = \frac{M}{1} = M$$

等号可以取到，证毕。


## 结论

综上两步，矩阵的 $L_\infty$ 诱导范数等于其所有行向量的绝对值和的最大值：
${\VertA\Vert_\infty = \max_{1\le i\le m} \sum_{j=1}^n |a_{ij}|}$

# TODO 证明 $\VertA\Vert_2 = \sigma_{\max}(A)$（谱范数 / 最大奇异值）

$$\VertA\Vert_2 = \sigma_{\max}(A) \quad(\boldsymbol A\text{ 的最大奇异值，故该范数又称为谱范数})$$


## 目标

证明矩阵的 $L_2$ 诱导范数等于其最大奇异值（即 $A^T A$ 的最大特征值开根号）。

## 证明过程

我们要最大化放大倍数：
$$\frac{\VertAx\Vert_2}{\Vertx\Vert_2}$$

因为开根号是单调递增的，可以先最大化它的平方，这样能避免根号带来的计算麻烦：
$$\max_{x \neq 0} \frac{\VertAx\Vert_2^2}{\Vertx\Vert_2^2}
= \max_{x \neq 0} \frac{x^T A^T A x}{x^T x}$$

设
$$B = A^T A$$
这是一个对称半正定矩阵（必然满足）。

根据线性代数中的**瑞利商（Rayleigh quotient）定理**：对于一个对称矩阵，
$$\max_{x \neq 0} \frac{x^T B x}{x^T x}$$
恰好等于矩阵 $B$ 的最大特征值 $\lambda_{\max}(B)$。

因此：
$$\max_{x \neq 0} \frac{\VertAx\Vert_2^2}{\Vertx\Vert_2^2}
= \lambda_{\max}(A^T A)$$

两边同时开平方（因为范数是非负的，且特征值非负）：
$$\VertA\Vert_2 = \sqrt{\lambda_{\max}(A^T A)}$$

而矩阵 $A$ 的**最大奇异值** $\sigma_{\max}(A)$ 的定义正是：
$$\sigma_{\max}(A) = \sqrt{\lambda_{\max}(A^T A)}$$

所以最终得到：
$$\boxed{\VertA\Vert_2 = \sigma_{\max}(A)}$$

## 补充说明（等号成立条件）
同样地，当向量 $x$ 取为最大特征值 $\lambda_{\max}(A^T A)$ 对应的特征向量时，上述瑞利商取到最大值，即放大倍数达到上限，等号成立。这也意味着，谱范数对应的“最拉伸方向”是最大奇异值对应的右奇异向量方向。