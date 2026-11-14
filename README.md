# 信号与系统笔记 · 排版模板版

把原来的 ElegantBook 版重排成了一套更安静、更"书"的模板：正文换了衬线中文字体，
章首页做成大标题 + 细线，节标题用深靛蓝色块编号，公式、三线表、代码、定义盒、注意盒
统一到同一个色系里。

**正文一个字都没有改动**（除了下面"与原稿的差异"里说明的一处表格列宽微调），
换的只是封面、版心、字体、标题样式和各类盒子。

---

## 一、编译

```bash
xelatex 信号与系统笔记.tex
xelatex 信号与系统笔记.tex     # 第二遍，生成目录和交叉引用
```

- 只用 XeLaTeX（ctexbook + fontspec + xeCJK），不要用 pdfLaTeX。
- TeX Live 2026 已在本机验证：28 页，编译零报错、零 overfull 警告，目录与书签正常。

## 二、文件说明

| 文件 | 作用 |
| --- | --- |
| `信号与系统笔记.tex` | 正文（原稿全文 + 4 处的盒子/图表代码保持原样） |
| `_preamble.tex` | **模板本体**：字体、版心、颜色、封面、章/节标题、目录样式、note/warning/proof 盒子 |
| `cover.png` | 封面插图（原图沿用），可换成任意 16:9 图片 |
| `preview/` | 6 张成品预览图（封面 / 目录 / 章首页 / 正文 / 公式页 / 插图页） |
| `信号与系统笔记.pdf` | 编译好的成品 |
| `figures/` | 给以后插图用的空目录，`\graphicspath` 已指向这里 |

想改模板：只动 `_preamble.tex`；正文里只放内容。

## 三、模板都做了什么

1. **版心**：A4，左右边距 2.8 cm，正文 15.4 cm，字号 11 pt，行距走 ctex 的 11 pt 档
   （约 1.3 倍），段距用 `\parskip=2pt plus 1pt`、上下公式间距用 `abovedisplayskip` 等微调
   （`_preamble.tex` 第 67–74 行）。页眉左边书名、右边当前章，页脚居中页码。
   想整体调松紧：在 `_preamble.tex` 里加 `\linespread{1.35}\selectfont` 即可。
2. **字体**（第 48–56 行）
   - 中文正文：霞鹜新致宋 `LXGW Neo ZhiSong`（宋体，字面略窄，比思源宋体轻盈）
   - 中文标题：鸿蒙黑体 `HarmonyOS Sans SC`（真粗体）
   - 西文正文：`TeX Gyre Termes`（Times 风格，和宋体搭配）
   - 引文/口诀：霞鹜文楷 `\kaishu`
   - ⚠️ 系统里的 `Noto Serif SC` / `Noto Sans SC` 是**可变字体**，XeTeX 加载会直接报错，
     所以没有采用；换机器编译时若缺字体，改这几行即可（或换成 `SimSun` / `SimHei`）。
3. **封面**：满幅插图（16:9，`cover.png`）+ 下方文字栏，左侧色条 + 小标签 + 大标题 + 副标题 +
   细线 + 作者/单位；页脚一条细线上放日期和一句短句。
   改文字只需要改 `_preamble.tex` 末尾的 `\title` `\subtitle` `\author` `\institute` `\date`
   `\cover` `\extrainfo` 这几行。
4. **章首页**：色条 + `第 N 章` 小标签、超大黑体标题、下面一条通栏细线，不居中、不花哨。
5. **节标题**：`2.1` 数字放在深靛蓝实心块里，标题黑体，下方一条淡色细线；
   子节 `2.3.1` 用赤陶色小标题 + 更细的线，三级层次靠颜色和线宽区分。
6. **目录**：章条目黑体粗体、`第 二 章` 与标题拉开成一栏，页码右对齐；
   节/子节灰色点线引导、页码右对齐成一条竖列（页码用固定宽度盒子排，不会和点线粘连）。
7. **数学**：`newtxmath`，`\dd` `\ee` `\jj` 等宏已定义；`equation` 编号右对齐。
8. **图表**：`booktabs` 三线表 + 灰色表头底纹；图表标题居中在上方，编号自动跟随章
   （`表 2.1`、`图 4.2`）。
9. **盒子**：`note`（米色底、细边、西文标签可写 `\begin{note}[提示]`）、`warning`（浅赤陶底 + 左侧色条）、
   `proof`、`definition*` 这些环境名和原稿完全兼容，正文里的用法不用改。
   盒子都 `breakable`，跨页时不会被截断。
10. **代码**：`listings` 配了等宽西文 + 米色底 + 左侧留白，行号灰蓝色。

## 四、换配色 / 换字体（最常改的两件事）

配色全在 `_preamble.tex` 第 35–43 行，改一行回车即可：

```latex
\definecolor{accent}{HTML}{2E4A63}   % 主色：深靛蓝（章节数字、线条）
\definecolor{warm}{HTML}{B4562C}     % 辅色：赤陶（提示、强调）
```

换成学术蓝紫 `accent=33415C` + `warm=8C5A73`，或者墨绿 `accent=2F4F45` + `warm=A9713B`
都很好看；只要保持"一深一暖"两个色 + 三个灰阶，整本就不会花。

字体在第 48–56 行，换成 `SimSun` / `SimHei` / `FandolSong` 也能直接编译。

## 五、与原稿的差异

1. 文档类由 `elegantbook` 换成 `ctexbook` + 手写模板（`elegantbook.cls` 不再需要）。
2. 删掉了 `\usepackage{microtype}`：它在 XeLaTeX 下会干扰中文断行和字距，
   去掉后行末不再出现字挤在一起的现象。
3. 表 2.1（齐次解形式）第一列由 `0.24\linewidth` 加宽到 `0.31\linewidth`，
   否则"一对共轭复根 λ_{1,2}=α±jβ"会折成两行。除此之外正文未改。
4. 第 1 章《绪论》在原稿里整章都是注释状态（只剩 `\chapter`），所以 PDF 第 4 页只有一张
   章首页、正文一片空白——不是排版出错，把注释打开就有内容了。

## 六、用编辑器编译会遇到的坑（重要）

如果是在 **VS Code + LaTeX Workshop**（或 TeXstudio）里，打开 `_preamble.tex` 直接点"编译"，
会看到这样的报错：

```
Latexmk: Getting log file '.aux/_preamble.log'
Latexmk: Log file says no output from latex
Latexmk: For rule 'xelatex', no output was made
```

原因：`_preamble.tex` 里也有 `\documentclass`，但没有 `\begin{document}`（它只是导言区），
编辑器就把它当成了"根文件"去编译，于是必然 Emergency stop、没有 PDF。

已经修好了：两个文件的第一行都加了

```latex
% !TEX root = ./信号与系统笔记.tex
```

LaTeX Workshop / TeXstudio 认这行 magic comment，之后再在 `_preamble.tex` 里点编译，
它会自动改去编译主文件。如果编辑器仍然认错根文件，任选一种：

- 对主文件 `信号与系统笔记.tex` 按 `Ctrl+Alt+B`（或者右键 → LaTeX Workshop: Build LaTeX project）；
- 在 VS Code 设置里关掉自动识别：`latex-workshop.latex.rootFile.useSubFile = false`；
- 在 `_preamble.tex` 里右键 → *LaTeX Workshop: Set as LaTeX root* 之前，
  先对主文件用 *Set as LaTeX root*。

> 顺带说一句：报错里那个 "undefined LaTeX [行 1, 列 1]" 只是 VS Code 给"这次编译没有产出"
> 打的通用标记，不是真的少了宏定义，不用去找第 1 行。

## 七、常见改动速查

- 加一章：`\chapter{标题}`，章首页样式自动套用。
- 加提示框：`\begin{warning}[易错点] ... \end{warning}`；笔记框：`\begin{note}[核心概念] ... \end{note}`。
- 加图：图片放进 `figures/`，正文 `\includegraphics[width=0.7\linewidth]{xxx.png}`，
  图表标题用 `\caption{}` 即可，编号自动带章号。
- 想让章首页标题往下挪一点：改 `_preamble.tex` 里 chapter 的 `titlespacing` 第一个参数。
