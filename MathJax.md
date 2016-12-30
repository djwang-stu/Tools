[资料来源网站](http://mlworks.cn/posts/introduction-to-mathjax-and-latex-expression/)

## MathJax简介

[MathJax](http://www.mathjax.org/)是一款运行在浏览器中的开源的数学符号渲染引擎，使用MathJax可以方便的在浏览器中显示数学公式，不需要使用图片。目前，MathJax可以解析Latex、MathML和ASCIIMathML的标记语言。 MathJax项目于2009年开始，发起人有American Mathematical Society, Design Science等，还有众多的支持者，个人感觉MathJax会成为今后数学符号渲染引擎中的主流，也许现在已经是了。 本文接下来会讲述MathJax的基础用法，但不涉及MathJax的安装及配置。此外，推荐使用[StackEdit](https://stackedit.io/)学习MathJax的语法，它支持Markdown和MathJax，本文使用此编辑器撰写。



## 基础

### 公式标记与查看公式

使用MathJax时，需要用一些适当的标记告诉MathJax某段文本是公式代码。此外，MathJax中的公式排版有两种方式，inline和displayed。inline表示公式嵌入到文本段中，displayed表示公式独自成为一个段落。例如，f(x)=3×x这是一个inline公式，而下面f(x)=3×x是一个displayed公式。

在MathJax中，默认的displayed公式分隔符有`$$...$$` 和`\[…\]`,而默认的inline公式分隔符为` (…) `,当然这些都是可以自定义的，具体配置请参考[文档](http://docs.mathjax.org/en/latest/start.html#tex-and-latex-input)。下文中，使用`$$…$$`作为displayed分隔符，`$…$`作为inline分隔符。

此外，可以在渲染完成的公式上方右键点击，唤出右键菜单。在菜单中提供了查看公式代码、设置显示效果和渲染模式的选项。

### 希腊字母

请参见下表：

| 名称      | 大写   | Tex      | 小写   | Tex      |
| ------- | ---- | -------- | ---- | -------- |
| alpha   | A    | A        | α    | \alpha   |
| beta    | B    | B        | β    | \beta    |
| gamma   | Γ    | \Gamma   | γ    | \gamma   |
| delta   | Δ    | \Delta   | δ    | \delta   |
| epsilon | E    | E        | ϵ    | \epsilon |
| zeta    | Z    | Z        | ζ    | \zeta    |
| eta     | H    | H        | η    | \eta     |
| theta   | Θ    | \Theta   | θ    | \theta   |
| iota    | I    | I        | ι    | \iota    |
| kappa   | K    | K        | κ    | \kappa   |
| lambda  | Λ    | \Lambda  | λ    | \lambda  |
| mu      | M    | M        | μ    | \mu      |
| nu      | N    | N        | ν    | \nu      |
| xi      | Ξ    | \Xi      | ξ    | \xi      |
| omicron | O    | O        | ο    | \omicron |
| pi      | Π    | \Pi      | π    | \pi      |
| rho     | P    | P        | ρ    | \rho     |
| sigma   | Σ    | \Sigma   | σ    | \sigma   |
| tau     | T    | T        | τ    | \tau     |
| upsilon | Υ    | \Upsilon | υ    | \upsilon |
| phi     | Φ    | \Phi     | ϕ    | \phi     |
| chi     | X    | X        | χ    | \chi     |
| psi     | Ψ    | \Psi     | ψ    | \psi     |
| omega   | Ω    | \Omega   | ω    | \omega   |

### 上标与下标

上标和下标分别使用^与_，例如x_i^2：x2i。默认情况下，上下标符号仅仅对下一个组起作用。一个组即单个字符或者使用{..}包裹起来的内容。也就是说，如果使用10^10，会得到1010，而10^{10}才是1010。同时，大括号还能消除二义性，如x^5^6将得到一个错误，必须使用大括号来界定^的结合性，如{x^5}^6：x56 或者 x^{5^6}：x56。

### 括号

1. 小括号与方括号：使用原始的( )，[ ]即可，如(2+3)[4+4]：(2+3)[4+4]
2. 大括号：时由于大括号{}被用来分组，因此需要使用\{和\}表示大括号，也可以使用\lbrace 和\rbrace来表示。如\{a*b\}:a∗b，\lbrace a*b \rbrace：{a∗b}。
3. 尖括号：使用\langle 和 \rangle表示左尖括号和右尖括号。如\langle x \rangle：⟨x⟩。
4. 上取整：使用\lceil 和 \rceil 表示。 如，\lceil x \rceil：⌈x⌉。
5. 下取整：使用\lfloor 和 \rfloor 表示。如，\lfloor x \rfloor：⌊x⌋。
6. 不可见括号：使用.表示。

需要注意的是，原始符号并不会随着公式大小缩放。如，(\frac12)：(12)。可以使用\left(…\right)来自适应的调整括号大小。如下，{n∑i=0i2=(n2+n)(2n+1)6}

{n∑i=0i2=(n2+n)(2n+1)6}可以看到，公式1.2中的括号是经过缩放的。

### 求和与积分

\sum用来表示求和符号，其下标表示求和下限，上标表示上限。如，\sum_1^n：∑n1。

\int用来表示积分符号，同样地，其上下标表示积分的上下限。如，\int_1^\infty：∫∞1。

与此类似的符号还有，\prod：∏，\bigcup:⋃，\bigcap：⋂，\iint：∬。

### 分式与根式

分式的表示。第一种，使用\frac ab，\frac作用于其后的两个组a，b，结果为ab。如果你的分子或分母不是单个字符，请使用{..}来分组。第二种，使用\over来分隔一个组的前后两部分，如{a+1\over b+1}：a+1b+1。

根式使用\sqrt来表示。如，\sqrt[4]{\frac xy} ：4√xy

### 字体

1. 使用\mathbb或\Bbb显示黑板粗体字，此字体经常用来表示代表实数、整数、有理数、复数的大写字母。如，CHNQRZ。
2. 使用\mathbf显示黑体字，如，ABCDEFGHIJKLMNOPQRSTUVWXYZ，abcdefghijklmnopqrstuvwxyz。
3. 使用\mathtt显示打印机字体，如，ABCDEFGHIJKLMNOPQRSTUVWXYZ，abcdefghijklmnopqrstuvwxyz。
4. 使用\mathrm显示罗马字体，如，ABCDEFGHIJKLMNOPQRSTUVWXYZ，abcdefghijklmnopqrstuvwxyz。
5. 使用\mathscr显示手写体，如，ABCDEFGHIJKLMNOPQRSTUVWXYZ。
6. 使用\mathfrak显示Fraktur字母（一种德国字体），如ABCDEFGHIJKLMNOPQRSTUVWXYZ，abcdefghijklmnopqrstuvwxyz。

### 特殊函数与符号

1. 常见的三角函数，求极限符号可直接使用+缩写即可。如sinx,arctanx,lim1→∞。
2. 比较运算符：\lt \gt \le \ge \neq ： <>≤≥≠。可以在这些运算符前面加上\not，如\not\lt：≮。
3. \times \div \pm \mp表示：×÷±∓，\cdot表示居中的点，x \cdot y : x⋅y。
4. 集合关系与运算：\cup \cap \setminus \subset \subseteq \subsetneq \supset \in \notin \emptyset \varnothing ：∪∩∖⊂⊆⊊⊃∈∉∅∅.
5. 表示排列使用{n+1 \choose 2k} 或 \binom{n+1}{2k}，(n+12k)。
6. 箭头：\to \rightarrow \leftarrow \Rightarrow \Leftarrow \mapsto : →→←⇒⇐↦。
7. 逻辑运算符：\land \lor \lnot \forall \exists \top \bot \vdash \vDash ： ∧∨¬∀∃⊤⊥⊢⊨。
8. \star \ast \oplus \circ \bullet ： ⋆∗⊕∘∙。
9. \approx \sim \cong \equiv \prec ： ≈∼≅≡≺。
10. \infty \aleph_0 ∞ℵ0 \nabla \partial ∇∂ \Im \Re Imℜ。
11. 模运算 \pmode, 如，a\equiv b\pmod n：a≡b(modn)。
12. \ldots与\cdots，其区别是dots的位置不同，ldots位置稍低，cdots位置居中。a1+a2+⋯+an，a1,a2,…,an。
13. 一些希腊字母具有变体形式，如 \epsilon \varepsilon : ϵε, \phi \varphi ϕφ。

使用[Detexify](http://detexify.kirelabs.org/classify.html)，你可以在网页上画出符号，Detexify会给出相似的符号及其代码。这是一个方便的功能，但是不能保证它给出的符号可以在MathJax中使用，你可以参考[supported-latex-commands](http://docs.mathjax.org/en/latest/tex.html#supported-latex-commands)确定MathJax是否支持此符号。

### 空间

通常MathJax通过内部策略自己管理公式内部的空间，因此a…b与a…….b（.表示空格）都会显示为ab。可以通过在ab间加入\,增加些许间隙，\;增加较宽的间隙，\quad 与 \qquad 会增加更大的间隙，如，ab。

### 顶部符号

对于单字符，\hat：ˆx，多字符可以使用\widehat,^xy.类似的还有\hat,\overline,\vec,\overrightarrow, \dot \ddot : ˆx¯xyz→a→x˙x¨x。

### 结束

基础部分就是这些。需要注意的是一些MathJax使用的特殊字符，可以使用\转义为原来的含义。如`\$`表示‘$‘，`\_`表示下划线。

## 表格

使用`$$\begin{array}{列样式}…\end{array}$$`这样的形式来创建表格，列样式可以是clr表示居中，左，右对齐，还可以使用|表示一条竖线。表格中 各行使用\\分隔，各列使用&分隔。使用\hline在本行前加入一条直线。 例如，

```
$$
\begin{array}{c|lcr}
n & \text{Left} & \text{Center} & \text{Right} \\
\hline
1 & 0.24 & 1 & 125 \\
2 & -1 & 189 & -8 \\
3 & -20 & 2000 & 1+10i \\
\end{array}
$$

```

结果：

nLeftCenterRight10.2411252−1189−83−2020001+10i

一个复杂的例子如下：

min012300000101112012230123max012300123111232222333333Δ012300123110122210133210

## 矩阵

### 基本用法

使用`$$\begin{matrix}…\end{matrix}$$`这样的形式来表示矩阵，在\begin与\end之间加入矩阵中的元素即可。矩阵的行之间使用\\分隔，列之间使用&分隔。

例如

```
$$
        \begin{matrix}
        1 & x & x^2 \\
        1 & y & y^2 \\
        1 & z & z^2 \\
        \end{matrix}
$$

```

结果：

1xx21yy21zz2

### 加括号

如果要对矩阵加括号，可以像上文中提到的一样，使用\left与\right配合表示括号符号。也可以使用特殊的matrix。即替换`\begin{matrix}…\end{matrix}`中的matrix为pmatrix，bmatrix，Bmatrix，vmatrix,Vmatrix.

如pmatrix:(1234) bmatrix:[1234] Bmatrix:{1234} vmatrix:|1234| Vmatrix:‖1234‖

### 省略元素

可以使用\cdots ⋯ \ddots ⋱ \vdots ⋮来省略矩阵中的元素，如：

(1a1a21⋯an11a2a22⋯an2⋮⋮⋮⋱⋮1ama2m⋯anm)

### 增广矩阵

增广矩阵需要使用前面的array来实现，如

```
$$ \left[
      \begin{array}{cc|c}
        1&2&3\\
        4&5&6
      \end{array}
    \right]
$$

```

结果：

[123456]

## 对齐的公式

有时候可能需要一系列的公式中等号对齐，如：

√37=√732−1122=√732122⋅732−1732=√732122√732−1732=7312√1−1732≈7312(1−12⋅732)

这需要使用形如`\begin{align}…\end{align}`的格式，其中需要使用&来指示需要对齐的位置。请使用右键查看上述公式的代码。

## 分类表达式

定义函数的时候经常需要分情况给出表达式，可使用`\begin{cases}…\end{cases}`。其中，使用\来分类，使用&指示需要对齐的位置。如：

f(n)={n/2,if n is even3n+1,if n is odd

上述公式的括号也可以移动到右侧，不过需要使用array来实现，如下：

if n is even:n/2if n is odd:3n+1}=f(n)

最后，如果想分类之间的垂直间隔变大，可以使用\[2ex]代替\来分隔不同的情况。(3ex,4ex也可以用，1ex相当于原始距离）。

## 数学符号查询

一般而言，从一个巨大的符号表中查询所需要的特定符号是一件令人沮丧的事情。在此向大家介绍一个LATEX手写符号识别系统，如下图：

![Detexify 介绍 ](http://i.stack.imgur.com/ScK3R.png)

尽情享用吧~ [Detexify²](http://detexify.kirelabs.org/classify.html)。

## 空间问题

在使用Latex公式时，有一些不会影响公式正确性，但却会使其看上去很槽糕的问题。

### 不要在再指数或者积分中使用 \frac

在指数或者积分表达式中使用\frac会使表达式看起来不清晰，因此在专业的数学排版中很少被使用。应该使用一个水平的/来代替，效果如下：

BadBettereiπ2eiπ2eiπ/2∫π2−π2sinxdx∫π/2−π/2sinxdx

### 使用 \mid 代替 | 作为分隔符

符号|作为分隔符时有排版空间大小的问题，应该使用\mid代替。效果如下：

BadBetter{x|x2∈Z}{x∣x2∈Z}

### 多重积分

对于多重积分，不要使用\int\int此类的表达，应该使用\iint \iiint等特殊形式。效果如下：

BadBetter∫∫Sf(x)dydx∬Sf(x)dydx∫∫∫Vf(x)dzdydx∭Vf(x)dzdydx

此外，在微分前应该使用\,来增加些许空间，否则TEX会将微分紧凑地排列在一起。如下：

BadBetter∭Vf(x)dzdydx∭Vf(x)dzdydx

## 连分数

书写连分数表达式时，请使用\cfrac代替\frac或者\over两者效果对比如下：

x=a0+12a1+22a2+32a3+44a4+⋯x=a0+12a1+22a2+32a3+44a4+⋯

## 方程组

使用`\begin{array} … \end{array}`与`\left{…\right.`配合，表示方程组，如：

{a1x+b1y+c1z=d1a2x+b2y+c2z=d2a3x+b3y+c3z=d3

同时，还可以使用`\begin{cases}…\end{cases}`表达同样的方程组，如：

{a1x+b1y+c1z=d1a2x+b2y+c2z=d2a3x+b3y+c3z=d3

对齐方程组中的 = 号，可以使用 `\being{aligned} .. \end{aligned}`，如：

{a1x+b1y+c1z=d1+e1a2x+b2y=d2a3x+b3y+c3z=d3

如果要对齐 = 号 和项，可以使用`\being{array}{列样式} .. \end{array}`，如：

{a1x+b1y+c1z=d1+e1a2x+b2y=d2a3x+b3y+c3z=d3



## 颜色

命名颜色是浏览器相关的，如果浏览器没有定义相关的颜色名称，则相关文本将被渲染为黑色。以下颜色是HTML4与CSS2标准中定义的一些颜色，其应该被大多数浏览器定义了。

\color{black}{text}text\color{gray}{text}text\color{silver}{text}text\color{white}{text}text\color{maroon}{text}text\color{red}{text}text\color{yellow}{text}text\color{lime}{text}text\color{olive}{text}text\color{green}{text}text\color{teal}{text}text\color{aqua}{text}text\color{blue}{text}text\color{navy}{text}text\color{purple}{text}text\color{fuchsia}{text}text

此外，HTML5与CSS3也定义了一些颜色名称，[参见](http://www.w3.org/TR/css3-color/#svg-color)。 同时，颜色也可以使用#rgb的形式来表示，r、g、b分别表示代表颜色值得16进制数，如：

\#000text#00Ftext#0F0text#0FFtext#F00text#F0Ftext#FF0text#FFFtext

[HTML色彩快速参考手册](http://www.w3schools.com/html/html_colors.asp)

## 公式标记与引用

使用\tag{yourtag}来标记公式，如果想在之后引用该公式，则还需要加上\label{yourlabel}在\tag之后，如：

a:=x2−y3

为了引用公式，可以使用

```
\eqref{rlabel}
```

，如：

a+y3(*)=x2

可以看到，通过超链接可以跳转到被引用公式位置。