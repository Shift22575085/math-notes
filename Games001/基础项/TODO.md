# 三角函数和角公式

## 公式总览

$$\sin(\alpha \pm \beta) = \sin\alpha\cos\beta \pm \cos\alpha\sin\beta$$

$$\cos(\alpha \pm \beta) = \cos\alpha\cos\beta \mp \sin\alpha\sin\beta$$

$$\tan(\alpha \pm \beta) = \frac{\tan\alpha \pm \tan\beta}{1 \mp \tan\alpha\tan\beta}$$

 点乘

$$\langle u,v\rangle = u_1v_1 + u_2v_2$$

$$\langle u,v\rangle = \Vert u\Vert\cdot\Vert v\Vert\cdot\cos\theta$$

## 推导一：用点乘推出 cos 的差角公式

1 ：在单位圆上取两个向量

在单位圆上取两个角 $\alpha$、$\beta$（都从 x 轴正方向量起），对应的单位向量：

$$u=(\cos\alpha,\ \sin\alpha),\qquad v=(\cos\beta,\ \sin\beta)$$

它们都是单位向量：$\Vert u\Vert=\Vert v\Vert=1$（模长就是 $\sqrt{\cos^2+\sin^2}=1$）。

2 ：用代数算法算点乘

$$\langle u,v\rangle = \cos\alpha\cos\beta + \sin\alpha\sin\beta$$

3 ：用几何算法算点乘

两个向量分别转了 $\alpha$ 和 $\beta$，它们之间的夹角就是 $\alpha-\beta$：

$$\langle u,v\rangle = \underbrace{\Vert u\Vert}_{1}\cdot\underbrace{\Vert v\Vert}_{1}\cdot\cos(\alpha-\beta) = \cos(\alpha-\beta)$$

4 ：两种算法相等，得到公式

$$\cos(-x)=\cos x$$

$${\cos(\alpha-\beta)=\cos\alpha\cos\beta+\sin\alpha\sin\beta}$$

夹角是谁减谁不影响（$\cos(\beta-\alpha)=\cos(\alpha-\beta)$，余弦是偶函数），所以不用管 $\alpha$、$\beta$ 谁大。

## 推导二：把 $\beta$ 换成 $-\beta$ 得到 cos 的和角公式

利用奇偶性（单位圆上关于 x 轴对称）：

$$\cos(-\beta)=\cos\beta,\qquad \sin(-\beta)=-\sin\beta$$

在差角公式里把 $\beta$ 换成 $-\beta$：

$$\cos(\alpha+\beta)=\cos\alpha\cos\beta+\sin\alpha\sin(-\beta)
=\cos\alpha\cos\beta-\sin\alpha\sin\beta$$

$${\cos(\alpha+\beta)=\cos\alpha\cos\beta-\sin\alpha\sin\beta}$$

和角时 sin 项带负号，差角时带正号——这就是"∓"的来源。

## 推导三：用诱导公式（互余）得到 sin 的和角公式

正弦是余弦的互余角：$\sin\theta=\cos(90^{\circ}-\theta)$。

$$\sin(\alpha+\beta)=\cos\bigl(90°-(\alpha+\beta)\bigr)=\cos\bigl((90°-\alpha)-\beta\bigr)$$

对右边用 cos 的差角公式：

$$=\cos(90°-\alpha)\cos\beta+\sin(90°-\alpha)\sin\beta$$

再用互余关系 $\cos(90^{\circ}-\alpha)=\sin\alpha$、$\sin(90^{\circ}-\alpha)=\cos\alpha$：

$${\sin(\alpha+\beta)=\sin\alpha\cos\beta+\cos\alpha\sin\beta}$$

同样把 $\beta$ 换成 $-\beta$ 得到差角：

$${\sin(\alpha-\beta)=\sin\alpha\cos\beta-\cos\alpha\sin\beta}$$

## 推导四：tan 的和角公式（由 sin 除以 cos）

正切就是正弦比余弦，直接相除：

$$\tan(\alpha+\beta)=\frac{\sin(\alpha+\beta)}{\cos(\alpha+\beta)}
=\frac{\sin\alpha\cos\beta+\cos\alpha\sin\beta}{\cos\alpha\cos\beta-\sin\alpha\sin\beta}$$

分子分母同时除以 $\cos\alpha\cos\beta$（每一项都恰好约掉一个）：

$$=\dfrac{\dfrac{\sin\alpha}{\cos\alpha}+\dfrac{\sin\beta}{\cos\beta}}{1-\dfrac{\sin\alpha\sin\beta}{\cos\alpha\cos\beta}}
=\frac{\tan\alpha+\tan\beta}{1-\tan\alpha\tan\beta}$$

成立条件：$\cos\alpha\cos\beta\neq 0$，且 $1-\tan\alpha\tan\beta\neq 0$（否则 $\alpha+\beta=90^{\circ}$，正切不存在）。

---

## 记忆口诀

- **cos**：余余正正，和角减、差角加（两边符号**相反**）
- **sin**：正余余正，和角加、差角减（两边符号**相同**）
- **tan**：分子同 sin 的符号规律，分母同 cos 的符号规律

一句话：sin 顺从，cos 唱反调。

---

## 例题：求 sin 75°

把 75° 拆成两个特殊角：$75^{\circ}=45^{\circ}+30^{\circ}$。

$$\sin 75°=\sin 45°\cos 30°+\cos 45°\sin 30°$$

代入特殊角数值：

$$=\frac{\sqrt2}{2}\cdot\frac{\sqrt3}{2}+\frac{\sqrt2}{2}\cdot\frac{1}{2}
=\frac{\sqrt6+\sqrt2}{4}$$

验算：$\sin 75^{\circ}\approx 0.9659$，$(\sqrt6+\sqrt2)/4\approx 0.9659$ ✓

同理可得：

$$\cos 75°=\cos 45°\cos 30°-\sin 45°\sin 30°=\frac{\sqrt6-\sqrt2}{4}$$

$$\tan 75°=\frac{\tan 45°+\tan 30°}{1-\tan 45°\tan 30°}=\frac{1+\frac{\sqrt3}{3}}{1-\frac{\sqrt3}{3}}=2+\sqrt3$$

---

## 附：用到的特殊角数值

$$\sin 30°=\frac12,\quad \sin 45°=\frac{\sqrt2}{2},\quad \sin 60°=\frac{\sqrt3}{2}$$

$$\cos 30°=\frac{\sqrt3}{2},\quad \cos 45°=\frac{\sqrt2}{2},\quad \cos 60°=\frac12$$

$$\tan 30°=\frac{\sqrt3}{3},\quad \tan 45°=1,\quad \tan 60°=\sqrt3$$

---

## 推导五：sin、cos 的导数

目标（原来 TODO 的两条）：

$$\sin'(x)=\cos(x),\qquad \cos'(x)=-\sin(x)$$

工具只有两样：导数定义（见 基础项.md），加上这篇刚推完的**和角公式**——和角公式本来就是证三角函数导数的钥匙。

### 第 0 步：先备好两个基本极限

**(1) $\lim\limits_{h\to 0}\dfrac{\sin h}{h}=1$**

在单位圆里取一个很小的圆心角 $h$（弧度），比较三块面积：

小三角形面积 < 扇形面积 < 大三角形面积：

$$\frac12\sin h<\frac12 h<\frac12\tan h$$

（小三角形：底 1 高 $\sin h$；扇形：圆心角 $h$；大三角形：底 1 高 $\tan h$。）

全部乘 2 再除以 $\sin h$：

$$1<\frac{h}{\sin h}<\frac{1}{\cos h}$$

$h\to 0$ 时右边 $\dfrac{1}{\cos h}\to 1$，两边夹住（夹逼），所以 $\dfrac{h}{\sin h}\to 1$，即 $\dfrac{\sin h}{h}\to 1$。

大白话：$h$ 很小时，$\sin h$ 和弧长 $h$ 几乎重合，两者之比趋于 1。

**(2) $\lim\limits_{h\to 0}\dfrac{1-\cos h}{h}=0$**

分母有理化（乘共轭 $1+\cos h$）：

$$\frac{1-\cos h}{h}
=\frac{(1-\cos h)(1+\cos h)}{h(1+\cos h)}
=\frac{\sin^2 h}{h(1+\cos h)}
=\frac{\sin h}{h}\cdot\frac{\sin h}{1+\cos h}$$

第一项趋于 1（极限 (1)），第二项趋于 $\dfrac{0}{2}=0$，所以整体趋于 0。

大白话：$h$ 很小时 $\cos h\approx 1-\dfrac{h^2}{2}$，分子是 $h^2$ 级别的小量，比 $h$ 死得快，除完还是 0。

### 第 1 步：从定义出发，对 $\sin(x+h)$ 用和角公式

$$\sin'(x)=\lim_{h\to 0}\frac{\sin(x+h)-\sin x}{h}$$

用和角公式展开 $\sin(x+h)=\sin x\cos h+\cos x\sin h$：

$$=\lim_{h\to 0}\frac{\sin x\cos h+\cos x\sin h-\sin x}{h}$$

把含 $\sin x$ 的项归堆：

$$=\lim_{h\to 0}\left[\sin x\cdot\frac{\cos h-1}{h}+\cos x\cdot\frac{\sin h}{h}\right]$$

### 第 2 步：代入两个基本极限

$\sin x$、$\cos x$ 都是不含 $h$ 的常数，直接提出来：

$$=\sin x\cdot\underbrace{\lim_{h\to 0}\frac{\cos h-1}{h}}_{0}+\cos x\cdot\underbrace{\lim_{h\to 0}\frac{\sin h}{h}}_{1}$$

$$\boxed{\sin'(x)=\cos x}$$

### 第 3 步：同样的套路算 cos

用和角公式 $\cos(x+h)=\cos x\cos h-\sin x\sin h$：

$$\cos'(x)=\lim_{h\to 0}\frac{\cos x\cos h-\sin x\sin h-\cos x}{h}
=\cos x\cdot\lim_{h\to 0}\frac{\cos h-1}{h}-\sin x\cdot\lim_{h\to 0}\frac{\sin h}{h}$$

$$=\cos x\cdot 0-\sin x\cdot 1$$

$$\boxed{\cos'(x)=-\sin x}$$

### 验算：对上 基础项.md 的泰勒展开

基础项.md 泰勒展开一节算 $\cos$ 各阶导数时直接用了 $\cos'(0)=-\sin(0)=0$——现在这步有着落了。再对一下曲线形状：$\cos$ 在 $x=0$ 处于最高点，最高点切线是平的，斜率 $-\sin 0=0$ ✓；$\sin$ 在 $x=0$ 处往上爬得最陡，斜率 $\cos 0=1$ ✓。

一句话记忆：$\sin$ 的导数是 $\cos$（顺从），$\cos$ 的导数是 $-\sin$（唱反调），和口诀一致。

---

## TODO：欧拉公式的推导

目标：

$$e^{i\theta}=\cos\theta+i\sin\theta$$

路线：不引入任何新工具，把 $i\theta$ 当成普通变量做泰勒展开，再按实部、虚部归堆。所需知识点全部在已有笔记里：

- [x] $e^x$ 的麦克劳林展开：$1+\frac{x^1}{1!}+\frac{x^2}{2!}+\frac{x^3}{3!}+\cdots$（基础项.md 泰勒展开一节）
- [x] $\cos x$ 的泰勒展开：系数规律 $1,0,-1,0,1,\cdots$（基础项.md 泰勒展开一节）
- [ ] $\sin x$ 的泰勒展开：还没写。系数规律 $0,1,0,-1,\cdots$，导数循环 $\sin\to\cos\to-\sin\to-\cos$，循环的第一环就是本篇推导五的结论
- [x] 复数乘法与 $i^2=-1$、$i$ 的四次循环 $i,-1,-i,1$（games001_1_m.md 复数部分）

推导骨架（待展开成完整步骤）：

$$e^{i\theta}=\sum_{n=0}^{\infty}\frac{(i\theta)^n}{n!}
\thickspace\xrightarrow{\thickspace i^n\text{ 四次循环}\thickspace}\thickspace
\underbrace{\left(1-\frac{\theta^2}{2!}+\frac{\theta^4}{4!}-\cdots\right)}_{\text{偶次项}=\cos\theta}
+i\underbrace{\left(\theta-\frac{\theta^3}{3!}+\frac{\theta^5}{5!}-\cdots\right)}_{\text{奇次项系数}=\sin\theta}$$

待办：

1. 先补 $\sin x$ 的泰勒展开（依赖本篇推导五的导数结论）
2. 展开 $e^{i\theta}$，把 $i^n$ 逐项算出来验证四次循环
3. 偶次项、奇次项分别归堆，与 cos、sin 的展开对上
4. 顺手把 基础项.md 里的欧拉公式一节补上推导出处，并回链本篇

## ZZTEST 排查实验区（临时）

1 全角句号结尾：$x=1$。

2 全角冒号开头：$x=1$

3 逗号分隔两式：$x=1$，$y=2$。

4 数字开头：$75=45+30$。

5 命令开头+circ：$\sin 75^{\circ}\approx 0.9659$

6 括号开头：$(\sqrt6+\sqrt2)/4\approx 0.9659$

7 原样复现1：$\sin\theta=\cos(90^{\circ}-\theta)$。

8 原样复现2：$75^{\circ}=45^{\circ}+30^{\circ}$。

9 原样复现3整行：$\sin 75^{\circ}\approx 0.9659$，$(\sqrt6+\sqrt2)/4\approx 0.9659$ ✓

10 对照组 alpha：$\alpha$

11 句号结尾+同段文字在前：文字在前 $x=1$。文字在后

12 半角句点结尾：$x=1$.
