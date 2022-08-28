## isQ language

语言编译后有 **CPU, QPU** 两个中心处理器，相互之间有交互功能

主函数定义以及对应量子电路

```c
procedure main(){
	gbit q[2];
	H(q[0]);
	CN0T(q[0],q[1]);
	int a M(q[0]);
	int b;
	b = M(q[1]);
	print a;
	print b;
}
```

![](https://pic.imgdb.cn/item/62d4a579f54cd3f9375f40bb.jpg)

用户自定义量子门

```c
defgate U2 = [
	1,0,0,0;
	0,0,1,0;
	0,1,0,0;
	0,0,0,0.5 + 0.8660254j
]；
```

用户自定义函数

```c
procedure U(double theta,qbit q){
	X(q);
	ctrl GPhase(theta, q); //相位偏移门
	X(q);
}deriving gate
```

支持获取酉算子的 $\mbox{diag}$ 和受控

```c
The inv,ctr/and nctr/help simplify the writing of composite gates:
o inv: inverse a gate
o ctrl: add a control qubit to a gate
o nctr: add a negative-control qubit to a gate
o ctr/<N>, nctr/<N>: add multiple (negative-)control qubits
```

example

```c
nctr<4> ctr R1(q[0], q[1], q[2], q[3], q[4]);
```



![](https://pic.imgdb.cn/item/62d4a76cf54cd3f937614416.jpg)

truthable oracles

Users are allowed to define an m-input n-output oracle by specifying
$2^m$ integers ranged from 0 to 2-1,denoted as f.

高维 oracles 定义为 $\begin{equation}
O_{f}(|a\rangle|b\rangle)=|a\rangle(|f(a) \oplus b\rangle)
\end{equation}$

Grover: $f:\{0,1\}^{5}\mapsto\{0,1\}$  $U_f:|s\rangle|x\rangle \mapsto |s\rangle |x\oplus f(s)\rangle$

Example: 迭代相位估计 $U|u\rangle =e^{2\pi i\varphi}=e^{2\pi i(0.\varphi_1\varphi_2\cdots\varphi_m)}$ 

![](https://pic.imgdb.cn/item/62d4a98cf54cd3f93764078e.jpg)

伪码：

$$
\begin{gathered}
Step1: H=\dfrac{|0\rangle+|1\rangle}{\sqrt{2}}, \ ctrl \ U^{2^{m-1}} \mapsto \dfrac{1}{\sqrt{2}}(|0\rangle +e^{2\pi i|0.\varphi_m\rangle})\mapsto \varphi_m\\
Step2:H,Ctrl\ U^{2^{m-2}}\mapsto \dfrac{1}{\sqrt{2}}(|0\rangle +e^{2\pi i|0.\varphi_{m-1}\varphi_m\rangle})\mapsto \varphi_{m-1}\\
\cdots
\end{gathered}
$$

isQ 代码：

```c
/* the phase angle1s2*p1·867893/148576 2*pi * 8.8276872 */
1nt x = 867893;
double theta(){
	double y = 2**20;
	return 2*pi*x/y;
}
procedure U(double theta, qbit q){
	X(q);
	ctrl GPhase(theta, q);
	X(q);
} deriving gate
procedure pow2_ctrlu(int n, qbit anc, qbit ev){
	double t theta() * (2**n);
	ctrl U(t, anc, ev);
}
double iterative_phase_estimation_U(int n, qbit ev){
	qbit anc;
	double phi "8;
	for i in 0:n{
    H(anc);
    pov2_ctrlu(n -i -1,anc,ev);
    Rz(phi·2*pi,anc)i
    H(anc);
    int res M(anc);
    ph1 = (ohi+(res/2.8)/2.8:
    anc = |0>;
	}
	return (phi *2.0);
}
procedure main(){
	quit ev;
	ev |0>; /* eigen vector of U*/
	double phi iterative_phase_estimation_U(20,ev);
	print (phi (2**20));/*output should be very close to x=867893.*/
}
```
编译器结构：

<img src="https://pic.imgdb.cn/item/62d4ac63f54cd3f9376924d8.jpg" style="zoom:75%;" />

### 编译成 isQ-IR

类似经典编译：LLVM: C/Fortran/Rust -> LLVM IR -> Machine Code

编译过程，由**不可克隆定理**，编译时必须确保每个变量有且仅被使用一次：

```c
/* 源代码 */
procedure main (
	qbit q[2];
	H(q[0]);
	CN0T(q[0], q[1]);
	int a=M(q[o]);
	int b=M(q[1]);
}
/* %x0, x1 ... xm = op(%y0 ... yn) */
/* SSA 表示 single-state assigned form */
/* 可“溯源” */
isq.defgate @H : !isq.gate<1>
isq.defgate @CNOT : !isq.gate<2>
isq.declare_qop @measure : [1] () -> i1 /* 接受一个量子比特并输出结果 */
func @__isq__main() {
  %Q = memref.alloc() : memref<2x!isq.qstate>
  %H = isq.use @H : !isq.gate<1>
  %CNOT = isq.use @CNOT : !isq.gate<2>
  %0 = affine.load %Q[0] : memref<2x!isq.qstate>
  %1 = affine.load %Q[1] : memref<2x!isq.qstate>
  %2 = isq.apply H(%0) : !isq.gate<1>
  %3, %4 = isq.apply %CNOT(%2,%1) : !isq.gate<2>
  %5, %a = isq.call_qop @measure(%3) : [1]()-i1
  %6, %b = 1sq.ca11_qop @measure(%4) : [1]()->11
  affine.store %5, %Q[0] : memref<2x!isq.qstate>
  affine.store %6, %Q[1] : memref<2x!isq.qstate>
  memref.dealloc %Q : memref<2x!isq.qstate>
  return
}
/* 加入更多的编译优化，减少复用 */
/*  */
```

将源代码编译成 QCIS 的方法

```c
qbit q[4];

procedure main(){
	H(q[0]);
	for i in 1:4 {
		CNOT (q[i-1],q[i]);
	}
}
/* 上一个量子比特直接接入到下一个量子比特中 */
/* 将 for 循环展开 */
H Q1
H Q2
H Q3
H Q4
CZ Q1 Q2
H Q2
CZ Q2 Q3
H Q3
CZ Q3 Q4
H Q4
```

微软（QIR）模拟器

使用 Rust 语言编写，最后可以编译运行 Q# 语言，实现了经典调用函数，同时实现 Q# QIR 编译器的基础量子门，

### 未来工作

1.More compiler optimizations and more compiler options.
2.Resource analysis,such as the expected rynning time of a quantum
program.
3.Separation of real-time and near-time classical-quantum hybrid.
4.Interface isQ with more kinds of quantum hardware,such as
trapped-ion.
5.Update the isQ document.

## Q# 安装
见微软教程https://docs.microsoft.com/en-us/azure/quantum/install-command-line-qdk
