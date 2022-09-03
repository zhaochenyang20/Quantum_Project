# 量子纠错基础

**量子噪声定义**

量子噪声产生的主要原因是实验室环境下的量子系统并不是一个完美的孤立系统，总是会与环境发生相互作用，在这个大系统中的演化，就表现为实验系统中的噪声。

 我们可以假设初始状态下系统和环境之间是没有纠缠的，状态分别表示为 $\rho$ 和 $\rho_{env}$，且在系统和环境组成的大系统中经历演化 $U$，那么从实验室系统的角度来看，$\rho$ 经历如下的变化：
$$
\Epsilon (\rho) = tr_{env}[U (\rho \otimes \rho_{env})U^{\dagger}]
$$
由于我们总是可以引入一个额外的系统对 $\rho_{env}$ 进行纯化，并且假设它在纯化后表示状态 $|0\rangle$，我们总是可以假设环境的初始状态为 $|0\rangle$。所以以上的作用总是可以写作下面的 operator sum 的形式：
$$
E(\rho) = \sum_i E_i \rho E_i^\dagger
$$
它显然是线性的，并且若 $\rho$ 为正，$\Epsilon(\rho)$ 也为正，并且保持 trace 不变。集合 $E = \{E_i\}$ 就称之为错误。

我们可以假设初始状态下系统和环境之间是没有纠缠的，状态分别表示为 $\rho$ 和 $\rho_{env}$，且在系统和环境组成的大系统中经历演化 $U$，那么从实验室系统的角度来看，$\rho$ 经历如下的变化：
$$
\Epsilon (\rho) = tr_{env}[U (\rho \otimes \rho_{env})U^{\dagger}]
$$
由于我们总是可以引入一个额外的系统对 $\rho_{env}$ 进行纯化，并且假设它在纯化后表示状态 $|0\rangle$，我们总是可以假设环境的初始状态为 $|0\rangle$。所以以上的作用总是可以写作下面的 operator sum 的形式：
$$
E(\rho) = \sum_i E_i \rho E_i^\dagger
$$
它显然是线性的，并且若 $\rho$ 为正，$\Epsilon(\rho)$ 也为正，并且保持 trace 不变。集合 $E = \{E_i\}$ 就称之为错误。

# Shor 码

有一种简单的量子码能针对单量子比特上任意差错的影响进行保护。这种码就是以其发明者命名的 Shor 码，它是量子比特相位翻转码和三量子比特比特翻转码的组合。我们首先用相位翻转码来编码量子比特: $|0\rangle \rightarrow|+++\rangle,|1\rangle \rightarrow$ $|---\rangle$。其次，我们用三个量子比特比特翻转码来编码这些量子比特中的每个：$|+\rangle$ 编码为 $(|000\rangle+|111\rangle) / \sqrt{2},|-\rangle$ 编码为 $(|000\rangle-|111\rangle) / \sqrt{2}$。这个结果为 9 量子比特，其码字为：
$$
\begin{array}{l}
|0\rangle \rightarrow\left|0_{\mathrm{L}}\right\rangle \equiv \dfrac{(|000\rangle+|111\rangle)(|000\rangle+|111\rangle)(|000\rangle+|111\rangle)}{2 \sqrt{2}} \\
|1\rangle \rightarrow\left|1_{\mathrm{L}}\right\rangle \equiv \dfrac{(|000\rangle-|111\rangle)(|000\rangle-|111\rangle)(|000\rangle-|111\rangle)}{2 \sqrt{2}}
\end{array}
$$

Shor 码能对任一量子比特上的相位翻转差错和比特翻转差错进行保护。事实上，Shor 码对单量子比特上的保护要比比特翻转和相位翻转差错多得多。

我们现来证明，Shor 码可对完全任意的差错进行保护，只要规定它们仅影响一个单量子比特。

为简化分析，设一个任意类型的噪声只出现在第一量子比特上。我们用保迹量子运算 $\varepsilon$ 来描述噪声，分析纠错的最为方便的做法是将 $\varepsilon$ 展开为具有运算元 $\left\{E_{i}\right\}$ 的算子和表示。设噪声作用前编码后的量子比特状态为： $|\psi\rangle=\alpha\left|0_{\mathrm{L}}\right\rangle+\beta\left|1_{\mathrm{L}}\right\rangle$，则噪声作用以后这个状态为 $\varepsilon(|\psi\rangle\langle\psi|)=\displaystyle \displaystyle \sum_{i} E_{i}|\psi\rangle\langle\psi| E_{i}^{\dagger}$。为分析纠错的作用，最容易的做法是把纠错作用集中到这个和式的一个单项上，比如说 $E_{i}|\psi\rangle\langle\psi| E_{i}^{\dagger}$。作为第一量子比特上的一个单独的算子 $E_{i}$，可以被展开为单位阵 $I$ 、比特翻转 $X_{1}$ 、相位翻转 $Z_{1}$ 以及组合位与相位翻转 $X_{1} Z_{1}$ 的一个线性组合：
$$
E_{i}=e_{i 0} I+e_{i 1} X_{1}+e_{i 2} Z_{1}+e_{i 3} X_{1} Z_{1}
$$
(非归一化) 量子状态 $E_{i}|\psi\rangle$ 因而可写成 $|\psi\rangle, X_{1}|\psi\rangle, Z_{1}|\psi\rangle, X_{1} Z_{1}|\psi\rangle$ 四项的叠加。测量差错症状会将这个叠加结果坍塌为四个状态 $|\psi\rangle, X_{1}|\psi\rangle, Z_{1}|\psi\rangle, X_{1} Z_{1}|\psi\rangle$ 之一，恢复过程由随后通过作用适当的逆运算而执行，并获得最终状态 $|\psi\rangle$。这些对于所有其他运算元 $E_{i}$ 也是正确的。因此，纠错会使原来状态 $|\psi\rangle$ 恢复，尽管事实上第一量子比特上的差错是任意的。这是关于量子纠错的一个基本和深刻的事实，通过只纠正差错的一个离散集一一在这个例子中，为比特翻转、相位翻转以及组合比特与相位翻转一一量子纠错码就会自动地纠正要比这个离散集明显大得多的 (连续) 差错类。

# 量子纠错理论

量子纠错理论的基本思想自然地推广了由 Shor 码引发的思想，量子状态通过酉运算被编码为量子纠错码，其形式定义为某个较大 Hilbert 空间中的一个子空间 $C$。为方便起见，我们采用符号 $P$ 表示到码空间 $C$ 上的投影算子；且对三量子比特比特翻转码，$P=|000\rangle\langle 000|+| 111\rangle\langle 111|$。在编码以后，这个码会受到噪声的影响，紧接着执行差错症状测量以检测所出现的差错类型。一旦差错症状确定，恢复运算就会执行，以使量子系统回到这个码的原来状态。

不同的差错症状对应于整个 Hilbert 空间中保形的和正交的子空间，这些子空间必是正交的，否则它们就不能被差错症状测量可靠地区分。进而，由于到不同子空间的差错映射必将正交码字映射到正交状态，因此这些不同的子空间必为原来码空间的保形版本，这样就能使其从差错中恢复。这个直观的图像基本上就是下面所要讨论的量子纠错条件的要旨。

## 量子纠错假定

我们仅只作两个很宽泛的假定：噪声由量子运算 $\varepsilon$ 所描述，整个纠错方法由我们称之为纠错运算的一个保迹量子运算 $\mathscr{R}$ 承担。这个纠错运算把我们上面称为差错检测和恢复的两个步骤合并，为确保纠错是成功的，我们要求对任何状态 $\rho$，其支集位于码空间 $C$ 中，有：

$$
(\mathscr{R} \circ \varepsilon)(\rho) \propto \rho
$$

量子纠错条件是一个简单方程组，它们可被检验以确定量子纠错码是否能对抗特殊类型的噪声 $\varepsilon$。我们将应用这些条件来构造大量的量子码，并将研究量子纠错码的一些普遍性质。

## 量子纠错条件

令 $C$ 为一个量子码，令 $P$ 为到 $C$ 的投影算子。设 $\varepsilon$ 为具有运算元 $\left\{E_{i}\right\}$ 的量子运算。则纠正 $C$ 上 $\varepsilon$ 的纠错运算 $R$ 存在的充分必要条件为，对某个复数  Hermite 矩阵 $\alpha$ 成立：
$$
P E_{i}^{\dagger} E_{j} P=\alpha_{i j} P
$$
我们称运算元 $\left\{E_{i}\right\}$ 为噪声 $\varepsilon$ 的差错，且如果这样一个 $\Re$ 存在，我们就说 $\left\{E_{i}\right\}$ 组成一个可纠正的差错集合。

## 差错离散化

我们已经讨论了针对一种特定噪声过程的量子信息的保护。但是，一般来说，我们并不准确知道量子系统遭受的是什么噪声。如果特定码 $C$ 和纠错运算 $\mathscr{R}$ 能被用于针对全部类型噪声过程的保护，那么这将会非常有用。幸运的是，量子纠错条件很容易用于严格地提供这类保护。

定理：设 $C$ 为量子码，$\mathscr{R}$ 为符合量子纠错条件的纠错运算，用以从具有算子元 $\left\{E_{i}\right\}$ 的噪声过程中恢复。设 $\mathscr{F}$ 为具有运算元 $\left\{F_{j}\right\}$ 的量子运算，运算元 $\left\{F_{j}\right\}$ 为 $E_{i}$ 的线性组合，即对某个复数矩阵 $m_{j i}$ 有 $F_{j}=\displaystyle \sum_{i} m_{j i} E_{i}$。那么，纠错运算 $\mathscr{R}$ 也可对码 $C$ 上的噪声过程 $\mathscr{F}$ 的作用来进行纠正。

由此，一噪声过程 $\varepsilon$，其运算元由这些差错算子 $\left\{E_{i}\right\}$ 的线性组合而成，都将通过恢复运算 $\mathscr{R}$ 可被纠正。

按此观点，设 $\varepsilon$ 为作用于单量子比特上的量子运算。那么，其每个运算元 $\left\{E_{i}\right\}$ 都可以被写成为 Pauli 矩阵 $\sigma_{0}, \sigma_{1}, \sigma_{2}, \sigma_{3}$ 的线性组合。

# 量子码构建

**CSS 码**

量子纠错码大类中的第一个例子是 Calderbank-Shor-Steane 码，通常更多地被称为 CSS 码，这是以码发明者姓名的首字母所命名的。CSS 码是更为一般类稳定子码的一个重要子类。

设 $C_{1}$ 和 $C_{2}$ 为 $\left[n, k_{1}\right]$ 和 $\left[n, k_{2}\right]$ 经典线性码，使有 $C_{2} \subset C_{1}$且 $C_{1}$ 和 $C_{2}^{\perp}$。两者可纠正 $t$ 个差错。通过下面的构造，我们将要定义能纠正 $t$ 个量子比特上差错的一个 $\left[n, k_{1}-k_{2}\right]$ 量子码  $\operatorname{CSS}\left(C_{1},C_{2}\right)$。即 $C_{2}$ 上 $C_{1}$ 的 $\operatorname{CSS}$ 码。设 $x \in C_{1}$ 为 $C_{1}$ 中的任一码字，那么，我们就定义量子状态 $\left|x+C_{2}\right\rangle$ 为：
$$
\left|x+C_{2}\right\rangle \equiv \dfrac{1}{\sqrt{\left|C_{2}\right|}} \sum_{y \in C_{2}}|x+y\rangle
$$
其中，“ +” 为按比特的模 2 方式加。设 $x^{\prime}$ 为 $C_{1}$ 的一个元，使有 $x-x^{\prime} \in C_{2}$。那么，容易看到 $\left|x+C_{2}\right\rangle=\left|x^{\prime}+C_{2}\right\rangle$，因此状态 $\left|x+C_{2}\right\rangle$ 只依赖于 $x$ 所在的陪集 $C_{1} / C_{2}$，这同时解释了我们已用于 $\left|x+C_{2}\right\rangle$ 的陪集符号。进而，如果 $x$ 和 $x^{\prime}$ 属于 $C_{2}$ 的不同陪集，那么不存在 $y, y^{\prime} \in C_{2}$，使得 $x+y=x^{\prime}+y^{\prime}$，因而 $\left|x+C_{2}\right\rangle$ 和 $\left|x^{\prime}+C_{2}\right\rangle$ 为正交状态。量子码  $\operatorname{CSS}\left(C_{1}, C_{2}\right)$ 就定义为由所有 $x \in C_{1}$ 的状态 $\left|x+C_{2}\right\rangle$ 所张成的向量空间。$C_{1}$ 中 $C_{2}$ 的陪集的数目为 $\left|C_{1}\right| /\left|C_{2}\right|$，所以 $\operatorname{CSS}\left(C_{1}, C_{2}\right)$ 的维数为 $\left|C_{1}\right| /\left|C_{2}\right|=$ $2^{k_{1}-k_{2}}$，因此 $\operatorname{CSS}\left(C_{1}, C_{2}\right)$ 是一个 $\left[n, k_{1}-k_{2}\right]$ 量子码。

# 稳定子码

设 $S$ 为 $G_{n}$ 的一个子群，定义 $V_{S}$ 为 由 $S$ 的每个元所固定的 $n$ 量子比特状态的集合。$V_{S}$ 为由 $S$ 所稳定的向量空间，$S$ 被称为空间 $V_{S}$ 的稳定子，因为 $V_{S}$ 的每个元为在 $S$ 中元的作用下是稳定的。

如果 $G$ 的每个元都可被写为序列 $g_{1}, \cdots, g_{l}$ 的元的一个乘积，群 $G$ 中的一组元 $g_{1}, \cdots, g_{l}$ 被说成为来生成这个群 $G$，写为 $G=$ $\left\langle g_{1}, \cdots, g_{l}\right\rangle$。在例子中，由于 $Z_{1} Z_{3}=\left(Z_{1} Z_{2}\right)\left(Z_{2} Z_{3}\right)$ 和 $I=\left(Z_{1} Z_{2}\right)^{2}$，所以 $S=\left\langle Z_{1} Z_{2},Z_{2} Z_{3}\right\rangle$。事实上，大小为 $|G|$ 的一个 群 $G$ 具有最多 $\log (|G|)$ 个的一组生成元。进而，为看清一个特定的向量可用群 $S$ 来稳定，我们只需要检验向量可用生成元稳定。因为它自动就会由生成元的乘积稳定。

并非 Pauli 群的任一子群 $S$ 都可被用作非平凡向量空间的稳定子。举例来说，考虑由 $(\pm I, \pm X)$ 组成的 $G_{1}$ 的子群，显然 $(-I)|\psi\rangle=|\psi\rangle$ 只有解 $|\psi\rangle=0$。因而， $(\pm I, \pm X)$ 是平凡向量空间的稳定子。为使 $S$ 稳定一个非平凡向量空间 $V_{S}, S$ 必须满足 两个必要条件：

1. S 的元可对易；
2. $-I$ 不是 $S$ 的一个元。

