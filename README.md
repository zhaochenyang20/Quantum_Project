# 前言

## 论文内容

本次量子计算研讨课程我们组选择对量子纠错理论进行研究。主要回顾了量子纠错的基本背景和传统理论，并且对 Subsystem Code 与 Surface Code 两个子领域进行了更为深入的讨论。

## 研讨内容

研讨，也即专门针对某一领域在集中场地进行探索、研究并讨论。出于对于量子计算领域的浓厚兴趣，小组同学在夏季学期积极广泛进行了论文分享、理论分析等组内讨论。

在课程本身的作业要求之外，我们对课程所讲述材料与推荐阅读书籍也进行了深入学习，并完成了量子编程语言笔记，课堂笔记与 《Quantum Computation and Quantum Information》习题的整理，相应的文件请参考[此链接](https://github.com/zhaochenyang20/Quantum_Project/tree/main/course-notes/suggestion)。

## 作业提交

我们将所写论文以 pdf 格式提交，然而 pdf 对图片的渲染并不完美，为了方便老师与助教批阅，也可以将我们的 github 仓库按照如下指令克隆至本地并查阅 `./submission.md`：

```bash
git clone --depth 1 git@github.com:zhaochenyang20/Quantum_Project.git
```

## 仓库说明

我们用以提交作业的开源[课程仓库](https://github.com/zhaochenyang20/Quantum_Project)主要文件树如下：

```shell
.
├── LICENSE
├── README.md
├── README.pdf
├── code-switch-and-baseline
│   ├── error-correction.md
│   └── paper
├── course-notes
│   ├── Nielsen-solutions
│   └── suggestion
├── proprosal.md
├── submission.md
├── submission.pdf
├── subsystem-code
│   ├── paper
│   └── subsystem-code-notes-refix.md
└── surface-code
    ├── Surface-code-note-refix.md
    ├── paper
    ├── pic
    └── quantum-error.md

10 directories, 10 files
```

1. `./code-switch-and-baseline` 文件夹下总结了传统量子纠错理论与方法。
2. `./course-note` 文件夹下的 `./course-note/Nielsen-solutions` 为一份残缺且存在错误的原书答案，而小组成员在其基础上展开讨论，共同编写了修订后的参考答案并放置于 `./course-note/suggestion` 文件夹下。
3. `./subsystem-code` 文件夹下总结了 subsystem code 子领域的最新发展，并附录了参考论文。
4. `./surface-code` 文件夹下总结了 surface-code 子领域的最新发展，并附录了参考论文。此外，还为量子错误提供了形式化定义。
5. `./submission.md` 与 `./submission.pdf` 为最终提交的论文。而 `README.md` 与 `README.pdf` 为对作业与仓库的说明文件。

此外，为方便下载单个文件夹，请复制该文件夹的网址，粘贴入 [DownGit](https://minhaskamal.github.io/DownGit/#/home) 中，选择 download 即可。

## 课程开源

量子计算领域的知名学者 John Martinis 曾经指出，开源不仅是一种行为，更是一种信仰。出于对于课程本身的热爱与量子计算领域的浓厚兴趣，我们将课程在 Github 平台、计算机系学生会权益发展部 bypass-thu-cst 仓库与计算机系课程分享平台 [REKCARC-TSC-UHT](https://github.com/PKUanonym/REKCARC-TSC-UHT) 进行了开源分享，希望以此帮助以后选修本门课程的同学克服量子计算理论部分学习的困难并且鼓励更多同学产生对前景广阔的量子计算领域的兴趣，共同促进这一领域的发展。

## 组内分工

小组由三名同学组成（按照姓氏首字母先后顺序排列）：

1. 黄书鸿 计算机系计 01 班 2019010435
2. 鲁睿 未央书院未央软 11 班 2021012539
3. 赵晨阳 计算机系计 06 班 2020012363

### 论文主体分工

1. 经典量子纠错码：由赵晨阳收集资料并整理原稿，黄书鸿负责审定并提供量子噪声的形式化定义
2. Shor 码：由鲁睿收集传统部分资料并交由赵晨阳整理原稿，后续在第七章子系统编码实例一节中的 Shor 码由鲁睿整理，赵晨阳负责审定
3. 量子纠错理论：由黄书鸿收集资料并整理原稿，赵晨阳负责审定
4. 量子码的构建：由赵晨阳收集资料并整理原稿，鲁睿负责审定
5. 稳定子码：由鲁睿收集资料并整理原稿，赵晨阳负责审定
6. Surface code：由黄书鸿收集资料并整理原稿，赵晨阳增补图片并审定
7. 子系统编码理论与实例：理论部分由鲁睿收集资料并整理原稿，实例部分由赵晨阳收集资料而鲁睿整理原稿，数学公式的审定由黄书鸿负责

### 附件与论文编写分工

1. `./course-note/Nielsen-solutions` 由鲁睿收集并整理
2. `./course-note/suggestion` 下，`isQ_language.md` 由黄书鸿整理；`量子信息与量子计算习题解答.md` 与 `量子信息与量子计算习题解答.pdf` 由赵晨阳和鲁睿共同完成；`量子计算课堂笔记.pdf` 由鲁睿完成

## 致谢

感谢**应明生教授**与**季铮锋教授**的倾情讲授与对量子计算领域前沿的相关引导。

感谢助教老师**郭敬哲**的指点与在作业上的帮助。

最后，感谢交叉信息学院《量子计算》课程的助教老师为我们提供论文资源与研究展望。

