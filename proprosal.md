# Quantum_Project
第一阶段，7 月 24 日前确定选题。

7 月 22 日确定选题为**量子纠错码**，参照茶园论文

**Quantum error correction**

- **Surface code**
  - A. G. Fowler, et al., Surface codes: Towards practical large-scale quantum computation, Phys. Rev. A 86, 032324 (2012)
  - C. Horsman, et al., Surface code quantum computing by lattice surgery, New J. Phys. 14123011 (2012)
  - H. Bombin and M. A. Martin-Delgado, Optimal resources for topological two-dimensional stabilizer codes: Comparative study, Phys. Rev. A 76, 012305 (2007)
  - Y. Tomita and K. M. Svore, Low-distance surface codes under realistic quantum noise, Phys. Rev. A 90, 062320 (2014)


- **Subsystem code**
  - D. Bacon, Operator quantum error-correcting subsystems for self-correcting quantum memories, Phys. Rev. A 73, 012340 (2006)
  - P. Aliferis and A. W. Cross, Subsystem Fault Tolerance with the BaconShor Code, Phys. Rev. Lett. 98, 220502 (2007)
  - J. Napp and J. Preskill, Optimal Bacon-Shor codes, Quantum Info. Comput. 13, 490 (2013)


- **~~Code-switching~~**
  - J. T. Anderson, G. Duclos-Cianci, and D. Poulin, Fault-Tolerant Conversion between the Steane and Reed-Muller Quantum Codes, Phys. Rev. Lett. 113, 080501 (2014)
  - C. D. Hill, et al., Fault-tolerant quantum error correction code conversion, Quantum Inf. Comput. 13, 439451 (2013)
  - H. P. Nautrup, N. Friis, and H. J. Briegel, Fault-tolerant interface between quantum memories and quantum processors. Nat Commun 8, 1321 (2017).

# To Be Merged

**stage 2**

内容详略和衔接

整体字数 1.5W ~ 2W

**将改过的内容写新文件，比如 `./xxxx_refix.md`，不要删改原稿**

1. 语言风格 ==@zcy==
2. 公式统一 ==@zcy==
3. 中英格式 ==@zcy==
4. 调整样式（typora / Latex / 参考文献） ==@lr==
5. 图床 ==@zcy==

## Baseline（1w）

1. 历史回顾，==量子错误的数学定义@hsh==，量子纠错理论（around 5k）

> 包括量子纠错理论，纠错条件，差错离散化和独立差错模型

2. 为具体 code 做的铺垫（around 5k）

> 量子 Hamming 界，经典线性码（定义，删除例子），CSS 码 + stablize 编码（highlight）
>
> ==@hsh==，extract：在同级文件下面开个新的 md，然后抽出内容

## surface code（5k）

1. 背景在 stablize 介绍了，不再重复
1. 构建

## subsystem code（5k）

1. 背景删除 ==@lr==
2. 习题单独提交（和笔记一起作为附录）==@zcy==
3. Shor algorithm 修改，然后注意风格统一 ==@lr==
4. paper 作为 appendix，写参考文献（写对应关系，不必在意样式），不按 paper 为小标题 ==@lr==
5. 考虑数学公式的可解释，如果解释不清楚，就删了 ==@lr==

## Pipeline

### 8.27 23:59:00

- [x] 量子错误的数学定义& extract 具体的 code @hsh
- [x] Subsystem 风格统一 + 解释 + 标题 @lr

------
### 8.28 23:59:00

- [x] 语言风格 + 公式统一 + 中英文格式 + 图床 @zcy
-----
### 8.30 23:59:00



- [ ] 二位开分支，把你们的主要部分 merge 进入根目录下的 ./submission.md，注意前后衔接，实在衔接不上就加入衔接词
- [ ] merge 结束了，师兄操刀删改下  ./submission.md，主要是删
- [ ] 删完了，鲁大师来复查下  ./submission.md，主要看逻辑链条
- [ ] 这些做完了，我来写完整 readme，然后鲁大师分别导出 readme.pdf 和 submission.pdf，注意样式 / perhaps Latex @lr & zcy
- [ ] 师兄最后审核下，结束了我就去交了