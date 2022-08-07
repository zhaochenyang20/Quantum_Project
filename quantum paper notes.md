## Shor algorithm

Shor 纠错算法的本质是利用量子态的相长干涉特点将错误放大。

Bacon-Shor 算法是 Shor 算法的保护版本

2021年10月，门罗研究团队在实验室中实现了充分容错量子计算。

```mermaid
graph LR
	A[量子纠错,2021] --> |原始| O[1量子比特]
	A --> |纠错| C[9物理量子比特 + 4辅助量子比特]
```

**是什么使量子信息处理成为可能？是什么分离了量子世界与经典世界？量子计算中正在利用哪些经典世界中无法获得的资源？**

<img src="https://pic.imgdb.cn/item/62ea88c016f2c2beb18c567a.jpg" style="zoom:30%;" />

## subsystem code papers outline

### Operator quantum error-correcting subsystems for self-correcting quantum memories(2006)

编码量子信息重点：如何将信息编码至量子系统的子空间

**算子量子纠错**，更一般，但没有产生新的纠错编码，但提供量子纠错程序以及阈值的可能性

本文设计 $[n^2,1,n]$ 以及  $[n^3,1,n]$ 编码（使用 $n^2(n^3)$ 编码一个量子比特，编码距离为 $n$ ） 

特定自纠错量子存储器(selfcorrecting quantum memory)

将一量子比特编码到两个量子比特：

|                          子空间编码                          |                          子系统编码                          |
| :----------------------------------------------------------: | :----------------------------------------------------------: |
| $\alpha|0\rangle+\beta |1\rangle\longrightarrow \alpha\dfrac{|01\rangle-|10\rangle}{\sqrt{2}}+\beta|11\rangle$ | $\alpha|0\rangle+\beta |1\rangle\longrightarrow \forall \ |\psi\rangle,|\psi\rangle\otimes (\alpha|0\rangle+\beta |1\rangle) $ |

$$
\begin{gathered}
H_{\text {int }}=\sum_{\alpha}\left[\left(I_{d} \oplus D_{\alpha}\right) \oplus E_{\alpha}\right] \oplus B_{\alpha}
\\\quad\quad\quad\quad\quad\quad\ \begin{array}{llll}\Large\downarrow & \Large\downarrow & \quad\Large\downarrow\quad& \Large\downarrow \\\mathcal{C} \quad& \mathcal{D} & \quad\mathcal{E} & \mathcal{H}_{E}\end{array}
\end{gathered}
$$

不关心对 $\mathcal{D}$ 的作用，只关心子系统 $\mathcal{C}$ 的情况，令 $|i\rangle \otimes|k\rangle$ 为 $\mathcal{C}\otimes\mathcal{D}$ 的基，量子纠错理论改版：

| 经典量子纠错                                                 | 子系统量子纠错                                               |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| $\langle i |E_{a}^{\dagger} E_{b}| j \rangle=\delta_{i, j} c_{a, b}$ | $\langle i|\otimes\langle k|) E_{a}^{\dagger} E_{b}(|j\rangle \otimes|l\rangle)=\delta_{i, j} m_{a, b, k, l}$ |

子系统纠错不提供新的编码，但给出不同的错误恢复方式（不需要修复其他空间的错误）

**二维晶格算子量子纠错**，构造二维晶格上的算子集合 $\mathcal{T},\mathcal{S},\mathcal{L}$，构建 $[n^2,1,n]$ 编码

将二维坐标一一映射到泡利算符
$$
P(a, b)=\prod_{i, j=1}^{n} X_{i, j}^{a_{i, j}} Z_{i, j}^{b_{i, j}}=\prod_{i, j=1}^{n} \begin{cases}X_{i, j} & \text { if } a_{i, j}=1 \text { and } b_{i, j}=0 \\ Z_{i, j} & \text { if } a_{i, j}=0 \text { and } b_{i, j}=1 \\ -i Y_{i, j} & \text { if } a_{i, j}=1 \text { and } b_{i, j}=1\end{cases}
$$


二维晶格上的三种群

$$
\begin{cases}
\mathcal{T}=\left\{(-1)^{\phi} P(a, b) \mid \phi \in \mathbb{Z}_{2}, \displaystyle \scriptsize \bigoplus_{i=1}^{n}\normalsize  a_{i, j}=0,\displaystyle \scriptsize \bigoplus_{j=1}^{n} \normalsize b_{i, j}=0\right\},\left\langle X_{i, j} X_{i+1, j}, Z_{j, i} Z_{j, i+1}\right\rangle\\
\mathcal{S}=\left\{P(a,b)|\displaystyle \scriptsize \bigoplus_{i=1}^{n}\normalsize \left(\displaystyle \scriptsize \bigwedge_{j=1}^{n}\normalsize a_{i,j}\right)=0,\displaystyle \scriptsize \bigoplus_{i=1}^{n}\normalsize \left(\displaystyle \scriptsize \bigwedge_{j=1}^{n}\normalsize b_{i,j}\right)=0\right\},
\displaystyle \left\langle\prod_{i=1}^{n} X_{j, i} X_{j+1, i}, \prod_{i=1}^{n} Z_{i, j} Z_{i, j+1}\right\rangle\\
\mathcal{L}=\left\{(-1)^{\phi} P(a, b) \mid \phi \in \mathbb{Z}_{2}, \displaystyle \scriptsize \bigoplus_{i=1}^{n}\normalsize \left(\displaystyle \scriptsize \bigwedge_{j=1}^{n}\normalsize a_{i,j}\right)=1, \displaystyle \scriptsize \bigoplus_{i=1}^{n}\normalsize \left(\displaystyle \scriptsize \bigwedge_{j=1}^{n}\normalsize b_{i,j}\right)=1\right\}
\end{cases}
$$

<img src="https://pic.imgdb.cn/item/62ef28c516f2c2beb127ba3a.jpg" style="zoom:25%;" />

分解 $(\mathbb{C}^2)^{2^{n}}$ 希尔伯特空间 $\mathcal{H}=\underset{s^{X}, s^{Z}}{\oplus} \mathcal{H}_{s^{X}, s^{Z}}=\underset{s^{X}, s^{Z}}{\oplus} \mathcal{H}_{s^{X}, s^{Z}}^{\mathcal{T}} \otimes \mathcal{H}_{s^{X}, s^{Z}}^{\mathcal{L}}$，$\mathcal{D}$ 为前者

对所有 $P(a,b)$ 泡利错误，无错误时 $\in \mathcal{T}$，由此错误 $\in \mathcal{H}_{s^{X}, s^{Z}}^{\mathcal{T}}$，对 $ \mathcal{H}_{s^{X}, s^{Z}}^{\mathcal{L}}$ 无影响，无噪声系统

对有噪声系统....

一些想法：**正方形晶格可不可以换成六边形晶格**？

Open questions:

+ 光学晶格和超冷原子物理实现以及在两个这样的编码格之间产生有效的受控NOT耦合
+ 三维量子系统是否实现自我纠错？符号问题 $\longrightarrow $ 量子蒙特卡洛模拟，密度矩阵重整化组。
+ 在二维系统中如何设计自我纠错量子系统
+ 算子量子纠错子系统在量子信息科学的作用，设计其余子系统，能否突破量子汉明码边界

### Subsystem Fault Tolerance with the Bacon-Shor Code(2007)

**摘要**：基于**子系统编码**在 Bacon-Shor 编码中的有效应用。FTEC 不需要纠缠附属态，实现最近两比特测量，找到**对抗随机噪声**下更低的量子准确极限 $1.94\times 10^{-4}$ 。

各种编码的性能，$\mbox{CNOT}$ 个数，理论下界，蒙特卡洛数值计算，吻合度高
$$
\begin{equation}
\begin{array}{llrcr}
\hline \hline {\text { Code }} & \text { FTEC } & \text { locs. } & \varepsilon_{0}\left(\times 10^{-4}\right) & \varepsilon_{0}^{\mathrm{MC}}\left(\times 10^{-4}\right) \\
\hline \text { Steane }[[7,1,3]] & \text { Steane } & 575 & 0.27 & \\
\mathcal{C}_{\mathrm{BS}}^{(3)}[[9,1,3]] & \text { Steane } & 297 & 1.21 & 1.21 \pm 0.06 \\
& \text { Knill } & 297 & 1.26 & 1.26 \pm 0.05 \\
\mathcal{C}_{\mathrm{BS}}^{(5)}[[25,1,5]] & \text { Steane } & 1185 & 1.94 & 1.92 \pm 0.02 \\
& \text { Knill } & 1185 & & 2.07 \pm 0.03 \\
\text { Golay }[[23,1,7]] & \text { Steane } & 7551 & & \approx 1 \\
\mathcal{C}_{\mathrm{BS}}^{(7)}[[49,1,7]] & \text { Steane } & 2681 & & 1.74 \pm 0.01 \\
& \text { Knill } & 2681 & & 1.91 \pm 0.01 \\
\hline \hline
\end{array}
\end{equation}
$$

### Optimal Bacon-shor codes(2012)

> **Bacon-Shor code:** A Bacon-Shor code is a subsystem quantum error-correcting code on an $L \times L$ lattice where the $2(L-1)$ weight-2L stabilizers are usually inferred from the measurements of $(L-1)^2$ weight-2 gauge operators.

Bacon-Shor 编码将翻转比特和相位翻转比特结合在一起

比特翻转概率 $p_{X}$、相位翻转概率 $p_{Z}$，按照**非随机噪声**是否有偏向，推导对应失败概率

$$
p_X=p_Z,BSFail (p)=\left(\frac{2}{\pi \ln 2}\right)^{1 / 2} \exp \left(\frac{\ln ^{2} 2}{8}\right) p^{1 / 2} \exp \left(-\frac{\ln ^{2} 2}{8 p}+O(p)\right)\\
p_X\ll p_Z,\ln \left[B S Fail\left(p_{Z}, b\right)\right]=-A(b) / p_{Z}-(0.5) \ln \left(1 / p_{Z}\right)+C(b)+O\left(p_{Z}\right.\  polylog \left.(b)\right)
\\
A(b)=\frac{1}{8}(W(\sqrt{b}))^{2}+O\left(b^{-1 / 2} \ln b\right)\\
W(\sqrt{b})=\ln \sqrt{b}-\ln \ln \sqrt{b}+\frac{\ln \ln \sqrt{b}}{\ln \sqrt{b}}+O\left(\frac{\ln \ln \sqrt{b}}{\ln ^{2} \sqrt{b}}\right)
$$
与当今经典计算机容错率 $10^{-17}$ 的对比，仅需要保证 $p_{Z}/p_{X}\approx 0.02$





### BCH线性编码

(63,51) BCH 码的生成多项式为: 
$$
G(x)=1+x^{2}+x^{4}+x^{7}+x^{8}+x^{9}+x^{12}\Longleftrightarrow (1010100111001)*2=(5433)*{10}
$$
利用系统码编码方程进行编码 
$$
\large \mbox{C}(x)=x^{n-k}\cdot {m}(x)+\mathrm{Rem} *{G(x)}\left[x^{n-k} \cdot m(x)\right]
$$
其中 $\operatorname{Rem}$ 表示在 $F_{p}[n](p=2, n=12)$ 伽罗瓦域上模 $G(x)$ 求同余

# 量子信息与量子计算习题（鲁睿）

## Chapter 1

### $1.1$

经典最好情形 $\mathbf{2}$ 次。当且仅当测量两次结果相同时无法确定平衡函数和常函数，其容错概率
$$
p=\frac{\left(\begin{array}{l}2^{n-1} \\ 2\end{array}\right)\cdot 2}{\left(\begin{array}{l}2^{n} \\ 2\end{array}\right)}=\dfrac{2^{n-1}-1}{2^n-1}<\dfrac{1}{2}
$$

而量子算法仅需 $\mathbf{1}$ 次完全确定结果（$\epsilon=0$），说明量子计算在该问题上的优越性。

### $1.2$

若状态可区分，发送的状态可以确定，设计合适的哈密顿设计器，在相同的状态下建立第二个系统；相反，准备量子态的多个副本，计算可观测值的平均值加以区分量子态。

## Chapter 2

### $2.1$

$$
\left[\begin{array}{c}1 \\ -1\end{array}\right]+\left[\begin{array}{l}1 \\ 2\end{array}\right]-\left[\begin{array}{l}2 \\ 1\end{array}\right]=\left[\begin{array}{l}0 \\ 0\end{array}\right]
$$

### $2.2$

$$
A=\left[\begin{array}{ll}0 & 1 \\ 1 & 0\end{array}\right],input: \{|0\rangle,|1\rangle\}, output: \{|1\rangle,|0\rangle\},A=\left[\begin{array}{ll}1 & 0 \\ 0 & 1\end{array}\right]
$$

### $2.3$

$$
B A\left|v_{i}\right\rangle =B\left(\sum_{j} A_{j i}\left|w_{j}\right\rangle\right) =\sum_{j} A_{j i} B\left|w_{j}\right\rangle =\sum_{j, k} A_{j i} B_{k j}\left|x_{k}\right\rangle \\ =\sum_{k}\left(\sum_{j} B_{k j} A_{j i}\right)\left|x_{k}\right\rangle =\sum_{k}(B A)_{k i}\left|x_{k}\right\rangle
$$

### $2.4$

$$
I_{ij}=\delta _{ij}
$$

### $2.5$

$$
\begin{aligned}
&(1)\left(\left(y_{1}, \cdots, y_{n}\right), \sum_{i} \lambda_{i}\left(z_{i 1}, \cdots, z_{i n}\right)\right)=\sum_{i, j} y_{i}^{*} \lambda_{j} z_{j i} 
=\sum_{j} \lambda_{j}\left(\sum_{i} y_{i}^{*} z_{j i}\right) 
\\
&\quad \ =\sum_{j} \lambda_{j}\left(\left(y_{1}, \cdots, y_{n}\right),\left(z_{j 1}, \cdots, z_{j n}\right)\right) =\sum_{i} \lambda_{i}\left(\left(y_{1}, \cdots, y_{n}\right),\left(z_{i 1}, \cdots, z_{i n}\right)\right)\\
&(2)\ \left(\left(y_{1}, \cdots, y_{n}\right),\left(z_{1}, \cdots, z_{n}\right)\right)^{*}=\left(\sum_{i} z_{i}^{*} y_{i}\right)=\left(\left(z_{1}, \cdots, z_{n}\right),\left(y_{1}, \cdots, y_{n}\right)\right)\\
&(3)\left(\left(y_{1}, \cdots, y_{n}\right),\left(y_{1}, \cdots, y_{n}\right)\right) =\sum_{i} y_{i}^{*} y_{i} =\sum_{i}\left|y_{i}\right|^{2}\geq 0\\
&\quad \ \left(\left(y_{1}, \cdots, y_{n}\right),\left(y_{1}, \cdots, y_{n}\right)\right)=0 \Longleftrightarrow  \left(y_{1}, \cdots, y_{n}\right)=0
\end{aligned}
$$

### $2.6$

$$
\begin{aligned}\left(\sum_{i} \lambda_{i}\left|w_{i}\right\rangle,|v\rangle\right) &=\left(|v\rangle, \sum_{i} \lambda_{i}\left|w_{i}\right\rangle\right)^{*} =\left(\sum_{i} \lambda_{i}\left(|v\rangle,\left|w_{i}\right\rangle\right)\right)^{*}  =\sum_{i} \lambda_{i}^{*}\left(\left|w_{i}\right\rangle,|v\rangle\right) \end{aligned}
$$

### $2.7$

$$
\begin{aligned}
&\langle w \mid v\rangle=\left[\begin{array}{ll} 1 & 1
\end{array}\right]\left[\begin{array}{c} 1 \\ -1
\end{array}\right]=0 
,\frac{|w\rangle}{\||w\rangle \|}=\frac{|w\rangle}{\sqrt{\langle w | w\rangle}}=\frac{1}{\sqrt{2}}\left[\begin{array}{l} 1 \\ 1
\end{array}\right],
\frac{|v\rangle}{\||v\rangle \|}=\frac{1}{\sqrt{2}}\left[\begin{array}{c}
1 \\
-1
\end{array}\right]
\end{aligned}
$$

### $2.8$

数学归纳法， $k=1$ 时 $\begin{aligned}
\left\langle v_{1} | v_{2}\right\rangle &=\left\langle v_{1}\right|\left(\frac{\left|w_{2}\right\rangle-\left\langle v_{1} | w_{2}\right\rangle\left|v_{1}\right\rangle}{\|\left|w_{2}\right\rangle-\left\langle v_{1} | w_{2}\right\rangle\left|v_{1}\right\rangle \|}\right)
=0
\end{aligned}$

$n=k$ 成立，对于 $n=k+1$ 有，$\forall \ 1\leq j\leq n$
$$
\begin{aligned}

\left\langle v_{j} | v_{n+1}\right\rangle &=\left\langle v_{j}\right|\left(\frac{\left|w_{n+1}\right\rangle-\displaystyle \sum_{i=1}^{n}\left\langle v_{i} | w_{n+1}\right\rangle\left|v_{i}\right\rangle}{\|\left|w_{n+1}\right\rangle-\displaystyle \sum_{i=1}^{n}\left\langle v_{i} | w_{n+1}\right\rangle\left|v_{i}\right\rangle \|}\right)\\&=
\frac{\left\langle v_{j} | w_{n+1}\right\rangle-\displaystyle \sum_{i=1}^{n}\left\langle v_{i} | w_{n+1}\right\rangle\left\langle v_{j} | v_{i}\right\rangle}{\|\left|w_{n+1}\right\rangle-\displaystyle \sum_{i=1}^{n}\left\langle v_{i} | w_{n+1}\right\rangle\left|v_{i}\right\rangle \|}=0
\end{aligned}
$$

### $2.9$

根据完备性关系，$A=I_{W}AI_{V}=\displaystyle \sum_{i,j}|\omega_j\rangle\langle\omega_j|A|v_i\rangle\langle v_i|=\sum_{i,j}\langle\omega_j|A|v_i\rangle|\omega_j\rangle\langle v_i|$
$$
\begin{aligned}
X=|0\rangle\langle 1|+| 1\rangle\langle 0|,Y=-i|0\rangle\langle 1|+i| 1\rangle\langle 0|,Z=|0\rangle\langle 0|-| 1\rangle\langle 1|
\end{aligned}
$$

### $2.10$

$$
\left(\left|v_{j}\right\rangle\left\langle v_{k}\right|\right)_{p q}=\delta_{p j} \delta_{k q}
$$

### $2.11$

$$
\lambda_{X,Y,Z}=\pm1,\begin{cases}X:|\lambda=1\rangle=\dfrac{1}{\sqrt{2}}\left[\begin{array}{c} 1 \\1\end{array}\right],|\lambda=-1\rangle=\dfrac{1}{\sqrt{2}}\left[\begin{array}{c} -1 \\1\end{array}\right]\\
Y:|\lambda=1\rangle=\dfrac{1}{\sqrt{2}}\left[\begin{array}{c} 1 \\i\end{array}\right],|\lambda=-1\rangle=\dfrac{1}{\sqrt{2}}\left[\begin{array}{c} i \\1\end{array}\right]
\\Z:|\lambda=1\rangle=\left[\begin{array}{c} 1 \\0\end{array}\right],|\lambda=-1\rangle=\left[\begin{array}{c} 0 \\1\end{array}\right]
\end{cases}
$$

对角表示为 $\begin{cases}X=\begin{pmatrix}0 & 1\\1 & 0\end{pmatrix}=\dfrac{1}{2}\left(\begin{array}{l}1 \\ 1
\end{array}\right)\left(\begin{array}{ll} 1 & 1 \end{array}\right)-\dfrac{1}{2}\left(\begin{array}{l} 1 \\ -1 \end{array}\right)\left(\begin{array}{ll} 1 & -1 \end{array}\right)\\   Y=\begin{pmatrix}0 & -i\\i & 0\end{pmatrix}=\dfrac{1}{2}\left(\begin{array}{l}1 \\ i
\end{array}\right)\left(\begin{array}{ll} 1 & -i \end{array}\right)-\dfrac{1}{2}\left(\begin{array}{l} i \\ 1 \end{array}\right)\left(\begin{array}{ll} -i & 1 \end{array}\right)\\   Z=\begin{pmatrix}1 & 0\\0 & -1\end{pmatrix}=\left(\begin{array}{l}1 \\ 0
\end{array}\right)\left(\begin{array}{ll} 1 & 0 \end{array}\right)-\left(\begin{array}{l} 0 \\ 1 \end{array}\right)\left(\begin{array}{ll} 0 & 1 \end{array}\right)\end{cases}$

### $2.12$

$$
\lambda =1,|\lambda=1\rangle=\begin{bmatrix}0\\1\end{bmatrix},A\neq a\begin{bmatrix}0&0\\0&1\end{bmatrix}
$$

### $2.13$

> 伴随算子的抽象定义：$\forall \ |v\rangle ,|\omega\rangle,(|v\rangle,A|\omega\rangle)=(A^{\dagger}|v\rangle,|\omega\rangle)$
$$
\forall \ |x\rangle,|y\rangle,\langle x|(|\omega\rangle \langle v|)^{\dagger}|y\rangle =\left(|x\rangle,(|\omega\rangle \langle v|)^{\dagger}|y\rangle\right)=\left((|\omega\rangle \langle v|)^{\dagger}|y\rangle,|x\rangle\right)^{*}\\
=(|y\rangle,|\omega\rangle\langle v|x\rangle)^{*}=(\langle y|\omega\rangle\langle v|x\rangle)^{*}=\langle v|x\rangle ^{*}\langle y |\omega \rangle^{*}=\langle x|v\rangle\langle \omega|y\rangle
$$

$$
\langle x|(|\omega\rangle \langle v|)^{\dagger}|y\rangle=\langle x|v\rangle\langle \omega|y\rangle\Longrightarrow (|w\rangle\langle v|)^{\dagger}=|v\rangle\langle w|
$$

### $2.14$

$$
\left(a_{i} A_{i}\right)^{\dagger}=(a_iIA_i)^{\dagger}=A_{i}^{\dagger}(a_i I)^{\dagger}=a_i^{*}A^{\dagger}
$$

### $2.15$

$$
\begin{aligned}
\left(\left(A^{\dagger}\right)^{\dagger}|\psi\rangle,|\phi\rangle\right) &=\left(|\psi\rangle, A^{\dagger}|\phi\rangle\right) =\left(A^{\dagger}|\phi\rangle,|\psi\rangle\right)^{*} =(|\phi\rangle, A|\psi\rangle)^{*} =(A|\psi\rangle,|\phi\rangle)
\end{aligned}
$$

### $2.16$

$$
P=\sum_{i=1}^{k}|i\rangle\langle i|,P^2=\left(\sum_{i=1}^{k}|i\rangle\langle i|\right)^2=\sum_{i=1}^{k}|i\rangle\langle i|i\rangle|i\rangle+2\sum_{i<j}|i\rangle\langle i|j\rangle|j\rangle=\sum_{i=1}^{k}|i\rangle\langle i|=P
$$

### $2.17$

$$
\Longrightarrow:A|\lambda\rangle=\lambda|\lambda\rangle,\langle \lambda|A|\lambda\rangle=\lambda \langle \lambda|\lambda\rangle=\langle\lambda|A^{\dagger}|\lambda\rangle=(A|\lambda\rangle)^{\dagger}|\lambda\rangle=\lambda^* \langle \lambda|\lambda\rangle,\lambda=\lambda^*\\
\Longleftarrow:AA^{\dagger}=A^{\dagger}A,A=\displaystyle \sum_{i}\lambda_i|\lambda_i\rangle\langle\lambda_i|,A^{\dagger}=\sum_{i}\lambda_i^*|\lambda_i\rangle\langle\lambda_i|=A^{\dagger}
$$

### $2.18$

设 $\lambda$ 为 $U$ 特征值， $|\lambda\rangle$ 为 $U$ 在 $\lambda$ 本征空间的特征向量， $U|\lambda\rangle=\lambda|\lambda\rangle,\langle\lambda|U^{\dagger}=\langle\lambda|\lambda^*$

相乘得 $\langle\lambda|U^{\dagger}U|\lambda\rangle=\lambda\lambda^*\langle\lambda|\lambda\rangle=\|\lambda\|^2\langle\lambda|\lambda\rangle=\langle\lambda|\lambda\rangle\Longrightarrow \|\lambda\|=1$

### $2.19$

$$
X=X^{\dagger},Y=Y^{\dagger},Z=Z^{\dagger},XX^{\dagger}=X^2=I,YY^{\dagger}=Y^2=I,ZZ^{\dagger}=Z^2=I,
$$

### $2.20$

$$
\left\langle v_{i}|A| v_{j}\right\rangle=\sum_{k l}\left\langle v_{i} \mid w_{k}\right\rangle\left\langle w_{k}|A| w_{l}\right\rangle\left\langle w_{l} \mid v_{j}\right\rangle
$$

### $2.21$

厄米算子 $A$ 的对角化：与正规算子相似，其中 $QMQ$ 的正规性易得
$$
\begin{aligned}
A &=I A I 
=(P+Q) A(P+Q) 
=P A P+Q A P+P A Q+Q A Q=\lambda P+QAQ
\end{aligned}
$$

$$
\begin{aligned}
Q A Q(Q A Q)^{\dagger} &=Q A Q Q A^{\dagger} Q =Q A^{\dagger} Q Q A Q =\left(Q AQ\right)^{\dagger} Q A Q
\end{aligned}
$$

将 $A$ 的对角化化解为 $P$ 和 $Q$ 的，从而由归纳法，任何厄米算子在标准正交基下可对角化

### $2.22$

$$
A|\lambda_1\rangle=\lambda_1|\lambda_1\rangle,A|\lambda_2\rangle=\lambda_2|\lambda_2\rangle,\langle\lambda_2|A^{\dagger}=\langle\lambda_2|\lambda_2^*\Longrightarrow\langle\lambda_2|A=\langle\lambda_2|\lambda_2\\
\langle\lambda_2|A|\lambda_1\rangle=\lambda_2\langle\lambda_2|\lambda_1\rangle=\lambda_1\langle\lambda_2|\lambda_1\rangle,\lambda_1\neq\lambda_2\Longrightarrow\langle\lambda_2|\lambda_1\rangle=0
$$

### $2.23$

$$
P|\lambda\rangle=\lambda|\lambda\rangle=P^2|\lambda\rangle=P\lambda|\lambda\rangle=\lambda^2|\lambda\rangle,|\lambda\rangle\neq0,\lambda^2=\lambda,\lambda=0,1
$$

### $2.24$

仿造实矩阵可分解为实对称矩阵和实反对称矩阵，将 $A$ 拆解为
$$
A=\frac{A+A^{\dagger}}{2}+i \frac{A-A^{\dagger}}{2 i}=B+iC
$$
其中 $B$ 和 $C$ 都为厄米矩阵，则 $\langle v|A|v\rangle=\langle v|B|v\rangle+i\langle v|C|v\rangle\geq 0$

而由厄米矩阵可以谱分解为 $\displaystyle \sum_{i}\lambda_i|i\rangle\langle i|$，其中 $|i\rangle$ 为标准正交基，且 $\lambda_i$ 为实数

故 $i\langle v|C|v\rangle$ 为虚数，从而 $\langle v|C|v\rangle=0\Longrightarrow C=O$，故 $A=B=\dfrac{A+A^{\dagger}}{2}$ 为厄米算子

> 引理：$\forall \ |v\rangle,\langle v|C|v\rangle=0\Longleftrightarrow C=O$。
>
>  $\forall \ |u\rangle,|v\rangle$，可以构造出下列等式使得 $\langle u|C|v\rangle=0$：
> $$
> \begin{array}{r}
> (|u\rangle, C |v\rangle)=\dfrac{1}{4}\left[(|u+v\rangle, C|u+v\rangle)-(|u-v\rangle, C|u-v\rangle)+\dfrac{1}{i}(|u+i v\rangle, C|u+i v\rangle)\right. \\
> \left.-\dfrac{1}{i}(|u-i v\rangle, C|u-i v\rangle)\right]
> \end{array}
> $$
> > 上式右侧化简 $\dfrac{2(|v\rangle,C|u\rangle)+2(|u\rangle,C|v\rangle)}{4}+\dfrac{2(|iv\rangle,C|u\rangle)+2(|u\rangle,iC|v\rangle)}{4i}$
> >
> > 由复空间内积定义 $(|iv\rangle,C|u\rangle)=\overline{i}\langle v|C|u\rangle=-i\langle v|C|u\rangle,(|u\rangle,iC|u\rangle)=i\langle u|C|v\rangle$
> >
> > $RHS=\dfrac{(|v\rangle,C|u\rangle)+(|u\rangle,C|v\rangle)}{2}+\dfrac{-i(|v\rangle,C|u\rangle)+i(|u\rangle,C|v\rangle)}{2i}=(|u\rangle, C |v\rangle)$
> >
>
> 故 $\forall \ |v\rangle,\langle v|C|v\rangle=0\Longleftrightarrow \forall \ |u\rangle,|v\rangle,\langle u|C|v\rangle=0$，而取 $|u\rangle=C|v\rangle$ ，由内积正定性
>
> $(C|v\rangle,C|v\rangle)=0\Longrightarrow C|v\rangle=0, \forall \ |v\rangle\Longrightarrow C=O$

### $2.25$

$$
\forall \ |v\rangle,\langle v|A^{\dagger}A|v\rangle=(A|v\rangle,A|v\rangle)\geq 0
$$

### $2.26$

$$
\begin{aligned}|\psi\rangle^{\otimes 2} &=\frac{1}{\sqrt{2}}(|0\rangle+|1\rangle) \otimes \frac{1}{\sqrt{2}}(|0\rangle+|1\rangle)=\frac{1}{2}(|00\rangle+|01\rangle+|10\rangle+|11\rangle)\\
|\psi\rangle^{\otimes 3} &=\frac{1}{\sqrt{2}}(|0\rangle+|1\rangle) \otimes \frac{1}{\sqrt{2}}(|0\rangle+|1\rangle) \otimes \frac{1}{\sqrt{2}}(|0\rangle+|1\rangle)\\ &=\frac{\sqrt{2}}{4}(|000\rangle+|001\rangle+|010\rangle+|011\rangle+|100\rangle+|101\rangle+|110\rangle+|111\rangle)
\end{aligned}
$$

### $2.27$

$$
\begin{aligned} X \otimes Z &=\left[\begin{array}{ll}0 & 1 \\ 1 & 0\end{array}\right] \otimes\left[\begin{array}{cc}1 & 0 \\ 0 & -1\end{array}\right]=\left[\begin{array}{cccc}0 & 0 & 1 & 0 \\ 0 & 0 & 0 & -1 \\ 1 & 0 & 0 & 0 \\ 0 & -1 & 0 & 0\end{array}\right] \\ 
I \otimes X &=\left[\begin{array}{ll}1 & 0 \\ 0 & 1\end{array}\right] \otimes\left[\begin{array}{ll}0 & 1 \\ 1 & 0\end{array}\right] =\left[\begin{array}{llll}0 & 1 & 0 & 0 \\ 1 & 0 & 0 & 0 \\ 0 & 0 & 0 & 1 \\ 0 & 0 & 1 & 0\end{array}\right] \\
X \otimes I &=\left[\begin{array}{lll}0 & 1 \\ 1 & 0\end{array}\right] \otimes\left[\begin{array}{ll}1 & 0 \\ 0 & 1\end{array}\right] =\left[\begin{array}{llll}0 & 0 & 1 & 0 \\ 0 & 0 & 0 & 1 \\ 1 & 0 & 0 & 0 \\ 0 & 1 & 0 & 0\end{array}\right] \end{aligned}
$$

一般情形下，张量积不可交换。

### $2.28$

$$
\begin{aligned}(A \otimes B)^{*} &=\left[\begin{array}{ccc}A_{11} B & \cdots & A_{1 n} B \\ \vdots & \ddots & \vdots \\ A_{m 1} B & \cdots & A_{m n} B\end{array}\right]^{*} =\left[\begin{array}{ccc}A_{11}^{*} B^{*} & \cdots & A_{1 n}^{*} B^{*} \\ \vdots & \ddots & \vdots \\ A_{m 1}^{*} B^{*} & \cdots & A_{m n}^{*} B^{*}\end{array}\right] =A^{*} \otimes B^{*} \\
(A \otimes B)^{T}&=\left[\begin{array}{ccc}
A_{11} B & \cdots & A_{1 n} B \\
\vdots & \ddots & \vdots \\
A_{m 1} B & \cdots & A_{m n} B
\end{array}\right]^{T}=\left[\begin{array}{ccc}
A_{11} B^{T} & \cdots & A_{m 1} B^{T} \\
\vdots & \ddots & \vdots \\
A_{1 n} B^{T} & \cdots & A_{m n} B^{T}
\end{array}\right]=A^{T} \otimes B^{T}\\

(A \otimes B)^{\dagger} &=\left((A \otimes B)^{*}\right)^{T} =\left(A^{*} \otimes B^{*}\right)^{T} =\left(A^{*}\right)^{T} \otimes\left(B^{*}\right)^{T} =A^{\dagger} \otimes B^{\dagger}

\end{aligned}
$$

### $2.29$

$$
\begin{aligned}
\left(U_{1} \otimes U_{2}\right)\left(U_{1} \otimes U_{2}\right)^{\dagger} &=U_{1} U_{1}^{\dagger} \otimes U_{2} U_{2}^{\dagger} =I \otimes I=I
\end{aligned}
$$

### $2.30$

$$
(A \otimes B)^{\dagger}=A^{\dagger} \otimes B^{\dagger}=A \otimes B
$$

### $2.31$

$$
(\langle u|\otimes\langle v|)(A \otimes B)| (u\rangle \otimes| v\rangle)=\langle u|A| u\rangle\langle v|B| v\rangle\geq 0
$$

### $2.32$

$$
\begin{aligned}
\left(P_{1} \otimes P_{2}\right)^{2} &=P_{1}^{2} \otimes P_{2}^{2} =P_{1} \otimes P_{2}
\end{aligned}
$$

### $2.33$

$$
\begin{aligned}
H &=\frac{1}{\sqrt{2}}[|0\rangle\langle 0|+| 1\rangle\langle 0|+| 0\rangle\langle 1|-| 1\rangle\langle 1|] =\frac{1}{\sqrt{2}} \sum_{x, y}(-1)^{x \cdot y}|x\rangle\langle y|\\
H^{\otimes n} &=\frac{1}{\sqrt{2^{n}}} \sum_{x 1, y 1}(-1)^{x_{1} \cdot y_{1}}\left|x_{1}\right\rangle\langle y_{1}|\otimes \cdots\otimes \sum_{x_{n}, y_{n}}(-1)^{x_{n} \cdot y_{n}} |x_{n}\rangle\langle y_{n}| \\&=\frac{1}{\sqrt{2^{n}}} \sum_{\boldsymbol{x}, \boldsymbol{y}}(-1)^{\boldsymbol{x} \cdot \boldsymbol{y}}|\boldsymbol{x}\rangle\langle\boldsymbol{y}|\\

H^{\otimes 2}&=\frac{1}{\sqrt{2}}\left[\begin{array}{cc}
1 & 1 \\
1 & -1
\end{array}\right] \otimes \frac{1}{\sqrt{2}}\left[\begin{array}{cc}
1 & 1 \\
1 & -1
\end{array}\right]=\frac{1}{2}\left[\begin{array}{cccc}
1 & 1 & 1 & 1 \\
1 & -1 & 1 & -1 \\
1 & 1 & -1 & -1 \\
1 & -1 & -1 & 1
\end{array}\right]

\end{aligned}
$$

### $2.34$

> 正规算子 $A$ （正交）谱分解 $A=\displaystyle \sum_{i}a|a\rangle\langle a|$ ，定义算子函数 $f(A)=\displaystyle \sum_{i}f(a)|a\rangle\langle a|$

将 $A=\left[\begin{array}{ll}
4 & 3 \\
3 & 4
\end{array}\right]$ 谱分解 $A=1\cdot \dfrac{1}{2}\left[\begin{array}{c} 1 \\-1\end{array}\right] \left[\begin{array}{c} 1 &-1\end{array}\right]+7\cdot \dfrac{1}{2}\left[\begin{array}{c} 1 \\1\end{array}\right] \left[\begin{array}{c} 1 &1\end{array}\right]$，从而
$$
\sqrt{A}=1\cdot \dfrac{1}{2}\left[\begin{array}{c} 1 \\-1\end{array}\right] \left[\begin{array}{c} 1 &-1\end{array}\right]+\sqrt{7}\cdot \dfrac{1}{2}\left[\begin{array}{c} 1 \\1\end{array}\right] \left[\begin{array}{c} 1 &1\end{array}\right]=\frac{1}{2}\left[\begin{array}{cc}
1+\sqrt{7} & -1+\sqrt{7} \\
-1+\sqrt{7} & 1+\sqrt{7}
\end{array}\right]\\
\log(A)=0\cdot \dfrac{1}{2}\left[\begin{array}{c} 1 \\-1\end{array}\right] \left[\begin{array}{c} 1 &-1\end{array}\right]+\log 7\cdot \dfrac{1}{2}\left[\begin{array}{c} 1 \\1\end{array}\right] \left[\begin{array}{c} 1 &1\end{array}\right]=\frac{\log (7)}{2}\left[\begin{array}{ll}
1 & 1 \\
1 & 1
\end{array}\right]
$$

### $2.35$

$$
\begin{aligned}
\vec{v} \cdot \vec{\sigma} &=\sum_{i=1}^{3} v_{i} \sigma_{i} =v_{1}\left[\begin{array}{ll}
0 & 1 \\
1 & 0
\end{array}\right]+v_{2}\left[\begin{array}{cc}
0 & -i \\
i & 0
\end{array}\right]+v_{3}\left[\begin{array}{cc}
1 & 0 \\
0 & -1
\end{array}\right] =\left[\begin{array}{cc}
v_{3} & v_{1}-i v_{2} \\
v_{1}+i v_{2} & -v_{3}
\end{array}\right]
\end{aligned}
$$

计算特征值 $\begin{aligned}
\operatorname{det}(\vec{v} \cdot \vec{\sigma}-\lambda I) &=\left(v_{3}-\lambda\right)\left(-v_{3}-\lambda\right)-\left(v_{1}-i v_{2}\right)\left(v_{1}+i v_{2}\right) =\lambda^{2}-1 \quad
\end{aligned}$

由其为厄米矩阵，则可以（正交）谱分解 $\vec{v} \cdot \vec{\sigma}=\left|\lambda_{1}\right\rangle\left\langle\lambda_{1}|-| \lambda_{-1}\right\rangle\left\langle\lambda_{-1}\right|$

其中 $\left|\lambda_{1}\right\rangle\left\langle\lambda_{1}|+| \lambda_{-1}\right\rangle\left\langle\lambda_{-1}\right|=I$，而代入指数函数分别作用在 $\pm i\theta$ 上，展开得到
$$
\begin{aligned}
e ^{i \theta \vec{v} \cdot \vec{\sigma}} &=e^{i \theta}\left|\lambda_{1}\right\rangle\left\langle\lambda_{1}\left|+e^{-i \theta}\right| \lambda_{-1}\right\rangle\left\langle\lambda_{-1}\right| \\
&=(\cos \theta+i \sin \theta)\left|\lambda_{1}\right\rangle\left\langle\lambda_{1}|+(\cos \theta-i \sin \theta)| \lambda_{-1}\right\rangle\left\langle\lambda_{-1}\right| \\
&=\cos \theta\left(\left|\lambda_{1}\right\rangle\left\langle\lambda_{1}|+| \lambda_{-1}\right\rangle\left\langle\lambda_{-1}\right|\right)+i \sin \theta\left(\left|\lambda_{1}\right\rangle\left\langle\lambda_{1}|-| \lambda_{-1}\right\rangle\left\langle\lambda_{-1}\right|\right) \\
&=\cos (\theta) I+i \sin (\theta) \vec{v} \cdot \vec{\sigma}
\end{aligned}
$$

### $2.36$

$$
\begin{aligned}
&\operatorname{Tr}\left(\sigma_{1}\right)=0+0=\operatorname{Tr}\left(\sigma_{2}\right)=0+0=\operatorname{Tr}\left(\sigma_{3}\right)=1+(-1)=0 
\end{aligned}
$$

### $2.37$

$$
\begin{aligned}
\operatorname{Tr}(A B) &=\sum_{i}\langle i|A B| i\rangle 
=\sum_{i, j}\langle i|A| j\rangle\langle j|B| i\rangle =\sum_{i, j}\langle j|B| i\rangle\langle i|A| j\rangle \\
&=\sum_{j}\langle j|B A| j\rangle =\operatorname{Tr}(B A)
\end{aligned}
$$

### $2.38$

$$
\begin{aligned}
\operatorname{Tr}(A+B) &=\sum_{i}\langle i|A+B| i\rangle =\sum_{i}(\langle i|A| i\rangle+\langle i|B| i\rangle)=\operatorname{Tr}(A)+\operatorname{Tr}(B) \\

\operatorname{Tr}(z A) &=\sum_{i}\langle i|z A| i\rangle 
=z \sum_{i}\langle i|A| i\rangle=z \operatorname{Tr}(A)

\end{aligned}
$$

### $2.39$

$(1)$ 分别验证对第二个参数线性、交换共轭、自身正定性：
$$
\begin{aligned}
(i)\ &\left(A, \sum_{i} \lambda_{i} B_{i}\right) =\operatorname{Tr}\left[A^{\dagger}\left(\sum_{i} \lambda_{i} B_{i}\right)\right] =\sum_{j}\langle j|A^{\dagger}\left(\sum_{i} \lambda_{i} B_{i}\right)|j\rangle\\
&\quad=\sum_{i}\lambda_{i} \sum_{j}\langle j|A^{\dagger} B_{i}|j\rangle
=\sum_{i} \lambda_{i} \operatorname{Tr}\left(A^{\dagger} B_{i}\right)\\
(ii)\ & (A,B)^*=\left(\sum _{j}\langle j|A^{\dagger}B|j\rangle\right)^*=\left(\sum _{j}\langle j|A^{\dagger}B|j\rangle\right)^{\dagger}=\sum _{j}\langle j|B^{\dagger}A|j\rangle=(B,A)\\
(iii)\ &(A, A) =\operatorname{tr}\left(A^{\dagger} A\right) =\sum_{j}\langle j|A^{\dagger}A|j\rangle\geq 0,(A,A)=0\Longleftrightarrow \forall \ |j\rangle,A|j\rangle=0,A=O
\end{aligned}
$$

$(2)$ $V\longmapsto V$ 中所有算子都可以用矩阵表示，维数为 $d\times d$，即 $ \dim(L_V)=d^2$

$(3)$ 对所有算子 $A$ 的标准正交基为 $A_{ij}=|v_i⟩⟨v_j|$，$|v_i⟩$ 为标准正交基

由于对所有厄米算子 $B$ 都可表为 $\dfrac{A+A^{\dagger}}{2}$，则构造正交基 
$$
A_{ij}=\dfrac{A_{ij}+A_{ij}^†}{2}=\dfrac{|v_i⟩⟨v_j|+|v_j⟩⟨v_i|}{2}
$$
对 $i=j$ 时为实数，$i\neq j$ 时可为虚数，两项相差负号，共 $d+2\cdot \dfrac{d(d-1)}{2}=d^2$ 项 

### $2.40$

$$
\begin{aligned}
&{[X, Y]=X Y-Y X=\left[\begin{array}{cc}
0 & 1 \\
1 & 0
\end{array}\right]\left[\begin{array}{cc}
0 & -i \\
i & 0
\end{array}\right]-\left[\begin{array}{cc}
0 & -i \\
i & 0
\end{array}\right]\left[\begin{array}{cc}
0 & 1 \\
1 & 0
\end{array}\right]=\left[\begin{array}{cc}
2 i & 0 \\
0 & -2 i
\end{array}\right]=2 i Z} \\
&{[Y, Z]=\left[\begin{array}{cc}
0 & -i \\
i & 0
\end{array}\right]\left[\begin{array}{cc}
1 & 0 \\
0 & -1
\end{array}\right]-\left[\begin{array}{cc}
1 & 0 \\
0 & -1
\end{array}\right]\left[\begin{array}{cc}
0 & -i \\
i & 0
\end{array}\right]=\left[\begin{array}{cc}
0 & 2 i \\
2 i & 0
\end{array}\right]=2 i X} \\
&{[Z, X]=\left[\begin{array}{cc}
1 & 0 \\
0 & -1
\end{array}\right]\left[\begin{array}{ll}
0 & 1 \\
1 & 0
\end{array}\right]-\left[\begin{array}{cc}
0 & 1 \\
1 & 0
\end{array}\right]\left[\begin{array}{cc}
1 & 0 \\
0 & -1
\end{array}\right]=2 i\left[\begin{array}{cc}
0 & -i \\
i & 0
\end{array}\right]=2 i Y}
\end{aligned}
$$

可简写为 $[\sigma_j,\sigma_k]=2i\displaystyle \sum_{l=1}^3\epsilon_{jkl}\sigma_l$ 

### $2.41$

$$
\left\{\sigma_{1}, \sigma_{2}\right\}=\left\{\sigma_{2}, \sigma_{3}\right\}=\left\{\sigma_{3}, \sigma_{1}\right\}=0,\sigma_{0}^{2}=\sigma_{1}^{2}=\sigma_{2}^{2}=\sigma_{3}^{2}=I
$$

### $2.42$

$$
\frac{[A, B]+\{A, B\}}{2}=\frac{A B-B A+A B+B A}{2}=A B
$$

### $2.43$

结合 $2.40-2.41$ 的计算结果可得
$$
\begin{aligned}
\sigma_{j} \sigma_{k} &=\frac{\left[\sigma_{j}, \sigma_{k}\right]+\left\{\sigma_{j}, \sigma_{k}\right\}}{2} =\frac{2 i \sum_{l=1}^{3} \epsilon_{j k l} \sigma_{l}+2 \delta_{j k} I}{2} =\delta_{j k} I+i \sum_{l=1}^{3} \epsilon_{j k l} \sigma_{l}
\end{aligned}
$$

### $2.44$

$$
[A, B]=0,\{A, B\}=0 \Longrightarrow  A B=0,A^{-1}AB=0=B
$$

### $2.45$

$$
\begin{aligned}
{[A, B]^{\dagger} } &=(A B-B A)^{\dagger} =B^{\dagger} A^{\dagger}-A^{\dagger} B^{\dagger} =\left[B^{\dagger}, A^{\dagger}\right]
\end{aligned}
$$

### $2.46$

$$
\begin{aligned}
{[A, B] } &=A B-B A =-(B A-A B) =-[B, A]
\end{aligned}
$$

### $2.47$

$$
(i(BA-AB))^{\dagger}=-iA^{\dagger}B^{\dagger}+iB^{\dagger}A^{\dagger}=i(BA-AB)
$$

### $2.48$

$$
P=UDU^{\dagger}(\lambda_i\geq 0),U=UII,H=U_1\sqrt{H^2},\sqrt{H^2}=U_2DU_2^{\dagger},H=U_1U_2DU_2^{\dagger}
$$

### $2.49$

$$
A=\sum_{i} \lambda_{i}|i\rangle\langle i|,\sqrt{A^{\dagger}A}=\sqrt{\sum_{i}|i\rangle\langle i|\lambda_i^*\sum_{j} \lambda_{j}|j\rangle\langle j|}=\sqrt{\sum _{i}\|\lambda_i\|^2|i\rangle\langle i|}=\sum _{i}\|\lambda_i\||i\rangle\langle i|
$$

构造标准正交基 $|e_i\rangle$，对 $\lambda\neq 0$ 的所有 $\lambda_i$ 取为 $\dfrac{\lambda_i|i\rangle}{\|\lambda_i\|}$，满足正交性，对 $\lambda=0$ 扩充至全空间

令 $U=\displaystyle \sum_{i}|e_i\rangle\langle i|$，故 $A=U\sqrt{A^{\dagger}A}=\displaystyle \sum_{i}\dfrac{\lambda_i}{\|\lambda_i\|}\|\lambda_i\||e_i\rangle\langle i|=A$

### $2.50$

$$
A=\left[\begin{array}{ll}
1 & 0 \\
1 & 1
\end{array}\right] , A^{\dagger} A=\left[\begin{array}{ll}
2 & 1 \\
1 & 1
\end{array}\right]
$$

而对 $\left[\begin{array}{ll}
2 & 1 \\
1 & 1
\end{array}\right]$ 计算特征值为 $\lambda_{1,2}=\dfrac{3\pm \sqrt{5}}{2}=\left(\dfrac{\sqrt{5}\pm 1}{2}\right)^2$ ，对应特征向量为
$$
|\lambda=\dfrac{3+\sqrt{5}}{2}\rangle=\frac{1}{\sqrt{10-2 \sqrt{5}}}\left[\begin{array}{c}
2 \\
-1+\sqrt{5}
\end{array}\right],
|\lambda=\dfrac{3-\sqrt{5}}{2}\rangle=\frac{1}{\sqrt{10+2 \sqrt{5}}}\left[\begin{array}{c}
2 \\
-1-\sqrt{5}
\end{array}\right]
$$

$$
J=\sqrt{A^{\dagger} A}=\sqrt{\lambda_{+}}| \lambda_{+}\rangle\left\langle\lambda_{+}\right|+\sqrt{\lambda_{-}}|\lambda_{-}\rangle\langle\lambda_{-}|
\\=\dfrac{\sqrt{5}+1}{2(10-2\sqrt{5})}\left[\begin{array}{c}
2 \\
-1+\sqrt{5}
\end{array}\right]\left[\begin{array}{c}
2 &
-1+\sqrt{5}
\end{array}\right]+\dfrac{\sqrt{5}-1}{2(10+2\sqrt{5})}\left[\begin{array}{c}
2 \\
-1-\sqrt{5}
\end{array}\right]\left[\begin{array}{c}
2 &
-1-\sqrt{5}
\end{array}\right]\\
=\dfrac{1}{\sqrt{5}}\left[\begin{array}{ll}
3 & 1 \\
1 & 2
\end{array}\right]
$$

从而 $J^{-1}=\frac{1}{\sqrt{5}}\left[\begin{array}{cc}
2 & -1 \\
-1 & 3
\end{array}\right]$，计算 $U=AJ^{-1}=\frac{1}{\sqrt{5}}\left[\begin{array}{cc}
2& -1 \\
1 & 2
\end{array}\right]$，则左极式分解为
$$
A=U\sqrt{A^{\dagger}A}=\frac{1}{\sqrt{5}}\left[\begin{array}{cc}
2 & -1 \\
1 & 2
\end{array}\right]\sqrt{A^{\dagger}A},\sqrt{A^{\dagger}A}=\dfrac{1}{\sqrt{5}}\left[\begin{array}{ll}
3 & 1 \\
1 & 2
\end{array}\right]
$$
 而 $AA^{\dagger}=\left[\begin{array}{ll}
1 & 1 \\
1 & 2
\end{array}\right]$，同样经过繁杂计算后得到 $\sqrt{AA^{\dagger}}=\dfrac{1}{\sqrt{5}}\left[\begin{array}{ll}
2 & 1 \\
1 & 3
\end{array}\right]$，则右极式分解为
$$
A=\sqrt{AA^{\dagger}}U=\sqrt{AA^{\dagger}}\frac{1}{\sqrt{5}}\left[\begin{array}{cc}
2 & -1 \\
1 & 2
\end{array}\right],\sqrt{A^{\dagger}A}=\dfrac{1}{\sqrt{5}}\left[\begin{array}{ll}
2 & 1 \\
1 & 3
\end{array}\right]
$$



