# Subsystem code

[TOC]

## 简介

基于上述提到的**稳定子编码**，可以扩展到一种更一般的形式——**子系统编码**，形式化地来说，将量子系统的希尔伯特空间加以分解
$$
\mathcal{H}=C\oplus C^{\perp}=A \otimes B \oplus C^{\perp}
$$
其中将信息存储在 $A$ 上，而 $B$ 上的错误则可以忽略，而 $C$ 的数学描述则与上述提到的稳定子描述完全相同，对应稳定子群 $\mathcal{S}$ 所有特征值为 $1$ 的特征向量集合，**稳定子编码的新颖性**在于 $A$ 和 $B$ 的分离能将信息存储和错误纠正**部分分解**，拓宽了量子纠错的研究。

子系统编码也可以用编码空间上的两种群导出，称为**逻辑群和测量群**，逻辑群由**稳定子形式**生成，分别由 $\mathcal{L}_b$ 以及 $\mathcal{G}$ 表示，且要求两者的算子组合是可交换的。在代数结构层面上，能够将张量结构加以分解。逻辑群和测量群中的算子分别只在 $A$ 和 $B$ 上具有非平凡作用，起到了**分割希尔伯特空间**的作用。

## 一般构造

定义作用在 $n$ 比特空间上的泡利算子集合为 $\mathcal{P}_n$ ，恰当地选择其中 $2n$ 个元素 $X_i,Z_i, i\in \underline{n}$，使其满足
$$
\left[X_{i}, Z_{j}\right]=2 X_{i} Z_{j} \delta_{i, j}
$$
接着构建稳定子群，选择 $r<n$，定义 $\mathcal{S}:=\{Z_1^{\prime},\cdots Z_r^{\prime}\}$，要求该群为阿贝尔群且不包含 $-I$，由稳定子编码理论，我们能定义一个 $k:=n-r$ 比特的编码空间，将其中角标小于等于 $r$ 的 $Z_{i}$ 用 $S_{i}$ 来代替，进而以 $\mathcal{S}$ 的元素生成 $\mathcal{C}$
$$
C(S)=\left\langle i I, S_{1}, \ldots, S_{r}, X_{r+1}^{\prime}, \ldots, X_{n}^{\prime}, Z_{r+1}, \ldots, Z_{n}\right\rangle
$$
再次选择 $q<n-r$ 将 $\mathcal{C}$ 加以分离，分别得到**逻辑群和测量群**
$$
\mathcal{L}_{b}:=\left\langle X_{r+q+1}^{\prime}, \ldots, X_{n}^{\prime}, Z_{r+q+1}^{\prime}, \ldots, Z_{n}^{\prime}\right\rangle\longrightarrow A
$$

$$
\mathcal{G}:=\left\langle i I, \mathcal{S}, X_{r+1}^{\prime}, \ldots, X_{r+q}^{\prime}, Z_{r+1}^{\prime}, \ldots, Z_{r+q}^{\prime}\right\rangle\longrightarrow B
$$

由构造前泡利算符的正交性条件，有 $\left[\mathcal{G}, \mathcal{L}_{b}\right]=0$，由此我们成功把 $C$ 分割成具有 $2^{k}$ 维数的空间 $A$ 以及具有 $2^{q}$ 维数的空间 $B$，且该分割完全由 $\mathcal{G}$ 决定。

## 纠错条件

由于不需要关心 $B$ 空间的错误，量子纠错条件需要加以修正，令 $|i\rangle \otimes|k\rangle$ 为 $A\otimes B$ 的基，其与经典量子纠错对比如下：

| 经典量子纠错                                                 | 子系统量子纠错                                               |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| $\langle i |E_{a}^{\dagger} E_{b}| j \rangle=\delta_{i, j} c_{a, b}$ | $\langle i|\otimes\langle k|) E_{a}^{\dagger} E_{b}(|j\rangle \otimes|l\rangle)=\delta_{i, j} m_{a, b, k, l}$ |

所有 $n$ 比特泡利错误 $E_a^{\dagger}E_b\in \mathcal{P}_n$ 可以分为以下三类：

+ $E_a^{\dagger}E_b\in \mathcal{P}_n/\mathcal{C}(\mathcal{S})$ 反交换，至少一个稳定子
+ $E_a^{\dagger}E_b\in \mathcal{C}(\mathcal{S})/\mathcal{G}$ 可交换，且对 $A$ 有影响 
+ $E_a^{\dagger}E_b\in \mathcal{G})$ 仅作用在测量转换

## 实例

以上从抽象的数学层面，基于稳定子编码的理论成果，对子系统编码的思想以及具体构造和纠错条件加以阐释。以下将从若干子系统量子纠错编码实例（均针对编码一个量子比特），体现更加具体的构造以及纠错能力。

### (伪)双比特子系统编码

>  该例子**只是为了更形象地说明**子系统量子纠错编码的思想，并没有成功达到纠错的目的（事实上，量子汉明界表明对于单比特量子至少需要 $5$ 个量子比特进行编码，而物理实验中一般使用 $7$ 个量子比特）

对于将单量子比特编码到双量子比特的情形，将希尔伯特空间 $\mathcal{H}$ 分解如下
$$
\begin{gathered}
H_{\text {int }}=\sum_{\alpha}\left[\left(I_{d} \oplus D_{\alpha}\right) \oplus E_{\alpha}\right] \oplus B_{\alpha}
\\\quad\quad\quad\quad\quad\quad\ \begin{array}{llll}\Large\downarrow & \Large\downarrow & \quad\Large\downarrow\quad& \Large\downarrow \\\mathcal{C} \quad& \mathcal{D} & \quad\mathcal{E} & \mathcal{H}_{E}\end{array}
\end{gathered}
$$
对于子空间编码而言，其编码方式作用在 $\alpha |0\rangle+\beta |1\rangle$ 上，本质上也是一种线性变换，形如 
$$
\alpha|0\rangle+\beta |1\rangle\longrightarrow \alpha\dfrac{|01\rangle-|10\rangle}{\sqrt{2}}+\beta|11\rangle
$$
而对于子系统编码而言，其增加了一个维度，且不关心该维度上的量子比特状态，形如
$$
\alpha|0\rangle+\beta |1\rangle\longrightarrow \forall \ |\psi\rangle,|\psi\rangle\otimes (\alpha|0\rangle+\beta |1\rangle)
$$

### shor 子系统纠错编码

重新回顾 Shor 纠错编码，其为 $[9,1]$ 编码，奇偶校验表示如下==（或见上）==
$$
\begin{gathered}
Z \otimes Z \otimes I \otimes I \otimes I \otimes I \otimes I \otimes I \otimes I \\
I \otimes Z \otimes Z \otimes I \otimes I \otimes I \otimes I \otimes I \otimes I \\
I \otimes I \otimes I \otimes Z \otimes Z \otimes I \otimes I \otimes I \otimes I \\
I \otimes I \otimes I \otimes I \otimes Z \otimes Z \otimes I \otimes I \otimes I \\
I \otimes I \otimes I \otimes I \otimes I \otimes I \otimes Z \otimes Z \otimes I \\
I \otimes I \otimes I \otimes I \otimes I \otimes I \otimes I \otimes Z \otimes Z \\
X \otimes X \otimes X \otimes X \otimes X \otimes X \otimes I \otimes I \otimes I \\
I \otimes I \otimes I \otimes X \otimes X \otimes X \otimes X \otimes X \otimes X
\end{gathered}
$$
该纠错编码中的**前 $6$ 个生成子可以调整为 $2$ 个**，由此总共简化为 $4$ 个稳定子，前两个生成子用于检验奇偶性，后两个生成子用于检验各三块之间的相位翻转性
$$
\begin{gathered}
&Z \otimes Z \otimes I \otimes Z \otimes Z \otimes I \otimes Z \otimes Z \otimes I \\
&I \otimes Z \otimes Z \otimes I \otimes Z \otimes Z \otimes I \otimes Z \otimes Z \\
&X \otimes X \otimes X \otimes X \otimes X \otimes X \otimes I \otimes I \otimes I \\
&I \otimes I \otimes I \otimes X \otimes X \otimes X \otimes X \otimes X \otimes X
\end{gathered}
$$
这样便可以同时检查六个物理比特的奇偶性，这样做之后我们的稳定子编码空间会更大，之前为 $2$ 维希尔伯特空间中的 $1$ 量子比特，减少 $4$ 个稳定子之后，稳定子编码空间为包含 $5$ 个虚拟比特的 $2^5$ 维空间。

随之而来的是，某些错误无法被探测到（例如同时在两份拷贝中发生比特翻转错误），但我们可以找到 **$4$ 对反对称算子**，这些算子能够生成当前无法被探测到的错误，这些算子只在**测量群**上工作，这 $4$ 对反对称算子的构造如下
$$
\begin{aligned}
&I \otimes Z \otimes Z \otimes I \otimes I \otimes I \otimes I \otimes I \otimes I \\
&I \otimes I \otimes X \otimes I \otimes I \otimes I \otimes I \otimes I \otimes X \\\\
&I \otimes I \otimes I \otimes I \otimes Z \otimes Z \otimes I \otimes I \otimes I \\
&I \otimes I \otimes I \otimes I \otimes I \otimes X \otimes I \otimes I \otimes X \\\\
&Z \otimes Z \otimes I \otimes I \otimes I \otimes I \otimes I \otimes I \otimes I \\
&X \otimes I \otimes I \otimes I \otimes I \otimes I \otimes X \otimes I \otimes I \\\\
&I \otimes I \otimes I \otimes Z \otimes Z \otimes I \otimes I \otimes I \otimes I \\
&I \otimes I \otimes I \otimes X \otimes I \otimes I \otimes X \otimes I \otimes I
\end{aligned}
$$
而刚好剩下一个比特作为稳定子形式，这 $4$ 个比特的错误不需要考虑，因为设计时信息仅存储在剩下的那一个比特中，进而**达到 $[[9,1,4,3]]$ 的纠错能力**，其中共有 $9$ 个量子比特参与纠错 $1$ 个比特，有 $4$ 个比特用于测量，其本身的错误不用考虑，汉明距离为 $3$。

 相较于稳定子形式，子系统编码有更大的优势，**测量群与逻辑群的分离**充分利用可交换性的特性，不需要修复其他空间的错误，保证纠错的正常进行。

### 晶格子系统纠错编码

#### 二维晶格 ( Bacon-Shor 编码)

在该实例中，考虑一个更具有物理含义的模型——**二维晶格算子量子纠错**。使用一个二维的晶格来存储以及纠错一个量子比特的信息。

先将二维坐标一一映射到泡利算符，代表所有发生**二维泡利错误**的情况
$$
P(a, b)=\prod_{i, j=1}^{n} X_{i, j}^{a_{i, j}} Z_{i, j}^{b_{i, j}}=\prod_{i, j=1}^{n} \begin{cases}X_{i, j} & \text { if } a_{i, j}=1 \text { and } b_{i, j}=0 \\ Z_{i, j} & \text { if } a_{i, j}=0 \text { and } b_{i, j}=1 \\ -i Y_{i, j} & \text { if } a_{i, j}=1 \text { and } b_{i, j}=1\end{cases}
$$

其中运用泡利算符恒等式 $XZ=\begin{pmatrix}0&1\\1&0\end{pmatrix}\begin{pmatrix}1&0\\0&-1\end{pmatrix}=\begin{pmatrix}0&-1\\1&0\end{pmatrix}=-iY$，在二维晶格上构建算子集合 $\mathcal{T},\mathcal{S},\mathcal{L}$，对应三种群，其数学形式如下：
$$
\begin{cases}
\mathcal{T}=\left\{(-1)^{\phi} P(a, b) \mid \phi \in \mathbb{Z}_{2}, \displaystyle \scriptsize \bigoplus_{i=1}^{n}\normalsize  a_{i, j}=0,\displaystyle \scriptsize \bigoplus_{j=1}^{n} \normalsize b_{i, j}=0\right\},\left\langle X_{i, j} X_{i+1, j}, Z_{j, i} Z_{j, i+1}\right\rangle\\
\mathcal{S}=\left\{P(a,b)|\displaystyle \scriptsize \bigoplus_{i=1}^{n}\normalsize \left(\displaystyle \scriptsize \bigwedge_{j=1}^{n}\normalsize a_{i,j}\right)=0,\displaystyle \scriptsize \bigoplus_{i=1}^{n}\normalsize \left(\displaystyle \scriptsize \bigwedge_{j=1}^{n}\normalsize b_{i,j}\right)=0\right\},
\displaystyle \left\langle\prod_{i=1}^{n} X_{j, i} X_{j+1, i}, \prod_{i=1}^{n} Z_{i, j} Z_{i, j+1}\right\rangle\\
\mathcal{L}=\left\{(-1)^{\phi} P(a, b) \mid \phi \in \mathbb{Z}_{2}, \displaystyle \scriptsize \bigoplus_{i=1}^{n}\normalsize \left(\displaystyle \scriptsize \bigwedge_{j=1}^{n}\normalsize a_{i,j}\right)=1, \displaystyle \scriptsize \bigoplus_{i=1}^{n}\normalsize \left(\displaystyle \scriptsize \bigwedge_{j=1}^{n}\normalsize b_{i,j}\right)=1\right\}
\end{cases}
$$

该数学形式比较抽象，可以形象地描述如下：

1. $\mathcal{T}$ 上的算子满足每一行的 $X$ 算符个数为偶数个，每一列的 $Z$ 算符个数也为偶数个， 其中 $X$ 和 $Z$ 可以交叉，交叉点写作 $Y$，体现在图 $\mathcal{T}$ 右上角区域中；
2. $\mathcal{S}$ 上的算子满足所有全包括 $X$ 的行个数为偶数个，所有全包括 $Z$ 的列个数也为偶数个，交叉点同理，可参考图 $\mathcal{S}$；
3. $\mathcal{L}$ 上的算子满足所有全包括 $X$ 的行个数为奇数个，所有全包括 $Z$ 的列个数也为奇数个，交叉点同理，可参考图 $\mathcal{L}$；

<img src="https://pic.imgdb.cn/item/62ef28c516f2c2beb127ba3a.jpg" style="zoom:25%;" />

由于 **$\mathcal{S}$ 可交换**，可分解 $(\mathbb{C}^2)^{2^{n}}$ 希尔伯特空间为 
$$
\mathcal{H}=\underset{s^{X}, s^{Z}}{\oplus} \mathcal{H}_{s^{X}, s^{Z}}
$$
又由于 $[\mathcal{T},\mathcal{L}]=0$，对每个 $\mathcal{H}_{s^{X}, s^{Z}}$ 可作如下分解，最终分解为
$$
H=\underset{s^{X}, s^{Z}}{\oplus} \mathcal{H}_{s^{X}, s^{Z}}^{\mathcal{T}} \otimes \mathcal{H}_{s^{X}, s^{Z}}^{\mathcal{L}}
$$
将信息编码在 $ \mathcal{H}_{s^{X}, s^{Z}}^{\mathcal{L}}$ 空间上， 作为子系统，定义纠错序列（**正交异或列**）
$$
e_{j}(a)=\oplus_{i=1}^{n} a_{i, j},\ f_{i}(b)=\oplus_{j=1}^{n} b_{i, j}
$$
**无噪声子系统**：满足 $e_j=f_i=0$ 的泡利错误 $P(a,b)\in \mathcal{H}_{s^{X}, s^{Z}}^{\mathcal{T}}$，此时对 $ \mathcal{H}_{s^{X}, s^{Z}}^{\mathcal{L}}$ 无影响，而编码并没有该空间上进行，相当于无噪声模型。

**有噪声子系统**：对更加一般的泡利错误 $P(a,b)$ ，选取一个泡利算子并与其作用，使其成为无噪声子系统中的错误，即 
$$
P^{\prime}(a,b)=Q(c,d)P(a,b)\in \mathcal{H}_{s^{X}, s^{Z}}^{\mathcal{T}}
$$
  $\mathcal{S}$ 用于错误纠正，其有 $2(n-1)$ 个生成元，分别作用在 $e_{j}(a)$ 和 $f_{i}(b)$ 上，同时得到生成结果，从 $\mathcal{S}$ 的生成元可知，问题**转化为两个一维重复编码**。
$$
\mathcal{S}=\left\langle\prod_{i=1}^{n} X_{j, i} X_{j+1, i}, \prod_{i=1}^{n} Z_{i, j} Z_{i, j+1}\right\rangle
$$
而对于一堆重复编码，其奇偶校验矩阵形式为 $\left[\begin{array}{llllll}
1 & 1 & & & & \\
& 1 & 1 & & & \\
& & \ \ \ddots & \ddots & & \\
& & & \ \ \ \ 1 & 1 & \\
& & & & 1 & 1
\end{array}\right]$

该矩阵任意 $n-1$ 列线性无关，存在 $n$ 列线性相关 （高斯消元），由经典线性码知识可知，其汉明距离为 $n$。

从而在该二维晶格中，有噪声子系统模型下，为 **$[n^2,1,n]$ 编码**，能纠正 $\lfloor\dfrac{n-1}{2}\rfloor$ 个错误，这这也说明 $n\geq 3$，否则无纠错效果。

该二维晶格子系统编码，本质上就是**把一维的重复编码扩展成二维**，能将 $2^{n^2}$ 维的**大希尔伯特空间分解成两个子系统**，将量子信息编码到其中一个子系统中，将信息和错误**部分分离**，达到更好的纠错效果。

#### 三维晶格

**三维晶格算子量子纠错**，与二维类似，在三维层面上加以修改，先定义**“三维”泡利错误**：
$$
\begin{aligned}
P(a, b) &=\prod_{i, j, k=1}^{n} X_{i, j, k}^{a_{i, j} k} Z_{i, j,, k}^{b_{i, j, k}} \\
&=\prod_{i, j, k=1}^{n} \begin{cases}X_{i, j, k} & \text { if } a_{i, j, k}=1 \text { and } b_{i, j, k}=0 \\
Z_{i, j, k} & \text { if } a_{i, j, k}=0 \text { and } b_{i, j, k}=1 \\
-i Y_{i, j, k} & \text { if } a_{i, j, k}=1 \text { and } b_{i, j, k}=1\end{cases}
\end{aligned}
$$
使用相同的手段构造出相应的算子群 $\mathcal{T}_3,\mathcal{S}_3,\mathcal{L}_3$ ，仅需要在求和时考虑多维度，同样也可以将 $\mathcal{H}$ 分解，利用相同的方式可以将错误都转换到整个大希尔伯特空间上的一个子集中，部分错误对其没有影响，剩余的错误则可以同时在每个维度上进行量子测量并加以修正。这样也可以**将三维问题转化为三个重复编码的问题**，最终得到 **$[n^3, 1, n]$ 编码**。

值得一提的是，由于现实世界是三维的，该三维晶格纠错可以从分析力学上找到相应的哈密顿量，例如在一个立方体晶格上定义哈密顿量
$$
H=-\lambda \sum_{i, j=1}^{n} \sum_{k=1}^{n-1}\left(X_{k, i, j} X_{k+1, i, j}+X_{i, k, j} X_{i, k+1, j}\right.
\left.+Z_{i, k, j} Z_{i, k+1, j}+Z_{i, j, k} Z_{i, j, k+1}\right)
$$
这与理论物理中的**伊辛耦合**相似，相应的，该哈密顿量也可以拆解为
$$
H=\underset{s^{X}, s^{Z}}{\oplus} H_{s^{X}, s^{\prime}} \otimes I_{2}
$$
于是可以利用量子信息的方法，将信息编码在 $I_2$ 中，达到纠错的效果。

## 抗噪性能

子系统纠错编码作为稳定子编码的扩充版本，这种**拆解**的思想，能让量子计算机的抵抗噪声性能有所提高，在前文经典量子纠错能力的基础上，该纠错编码方法能有效提高抵抗噪声性能。

### 随机噪声

 将上述二维晶格子系统纠错编码应用于实验室量子态，相应的纠缠附属态可以不需要，实现**最近两比特测量**，找到**对抗随机噪声**下**更低的量子准确极限 $1.94\times 10^{-4}$** ，相比之前下界提高一个数量级。

以下是应用**子系统编码**下，对于不同的编码，列出其需要的通用门 $\mbox{CNOT}$ 个数，使用子系统编码的理论计算得到的理论下界，在实验上，利用蒙特卡洛数值计算，其结果吻合度高：
$$
\begin{equation}
\begin{array}{llrcr}
\hline \hline {\text { Code }}  & \text { locs. } & \varepsilon_{0}\left(\times 10^{-4}\right) & \varepsilon_{0}^{\mathrm{MC}}\left(\times 10^{-4}\right) \\
\hline \text { Steane }[[7,1,3]]  & 575 & 0.27 & \\
\mathcal{C}_{\mathrm{BS}}^{(3)}[[9,1,3]]  & 297 & 1.21 & 1.21 \pm 0.06 \\
 & 297 & 1.26 & 1.26 \pm 0.05 \\
\mathcal{C}_{\mathrm{BS}}^{(5)}[[25,1,5]] & 1185 & 1.94 & 1.92 \pm 0.02 \\
 & 1185 & & 2.07 \pm 0.03 \\
\text { Golay }[[23,1,7]] & 7551 & & \approx 1 \\
\mathcal{C}_{\mathrm{BS}}^{(7)}[[49,1,7]]  & 2681 & & 1.74 \pm 0.01 \\
 & 2681 & & 1.91 \pm 0.01 \\
\hline \hline
\end{array}
\end{equation}
$$

可以看出，从真实的实验结果出发，子系统编码有比较更加的表现。

### 非随机噪声

在 Bacon-shor 二维晶格子系统纠错编码中，考虑某些特殊情形，噪声的分布不再是完全随机的，而是具有一定的偏向，设**比特翻转概率 $p_{X}$、相位翻转概率 $p_{Z}$**，按照**非随机噪声**是否有偏向，推导对应失败概率。

假设 $p_X=p_Z$，理论得到相应失败概率为
$$
p_{\text{fail}}=\left(\frac{2}{\pi \ln 2}\right)^{1 / 2} \exp \left(\frac{\ln ^{2} 2}{8}\right) p^{1 / 2} \exp \left(-\frac{\ln ^{2} 2}{8 p}+O(p)\right)
$$
相关数值计算表明，当失败概率小于 $0.01$ 时，需要 $p_X=p_Z<0.022$，这并不能带来更好的效果，但如果考虑有**偏向噪声**的情况，如 $p_X\ll p_Z$ ，此时通过 Bacon-Shor 编码的理论分析计算得到
$$
\ln (p_{\text{fail}})=-A(b) / p_{Z}-(0.5) \ln \left(1 / p_{Z}\right)+C(b)+O\left(p_{Z}\right.\  polylog \left.(b)\right)
\\
A(b)=\frac{1}{8}(W(\sqrt{b}))^{2}+O\left(b^{-1 / 2} \ln b\right)
$$
其中
$$
W(\sqrt{b})=\ln \sqrt{b}-\ln \ln \sqrt{b}+\frac{\ln \ln \sqrt{b}}{\ln \sqrt{b}}+O\left(\frac{\ln \ln \sqrt{b}}{\ln ^{2} \sqrt{b}}\right)
$$
这与现代计算机容错率 $10^{-17}$ 对比，仅需要保证 $p_{Z}/p_{X}\approx 0.02$ 的条件，说明在噪声有偏向的特殊情形下，子系统编码具有一定的优越性。



