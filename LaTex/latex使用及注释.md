```
\documentclass{article}  % 文档类声明为 article 类型

\usepackage{graphicx}  % 使用图形插入所需的宏包
\usepackage{amsmath}   % 使用 amsmath 宏包，提供了数学公式排版的增强功能
\usepackage{float}     % 导入控制浮动体位置的宏包
\usepackage{lipsum}    % 示例文本宏包
\usepackage{titlesec}  % 定制章节标题样式的宏包
\usepackage{titling}   % 定制标题样式的宏包
\usepackage{caption}   % 定制图表标题样式的宏包 ，这个可以去掉图片的自动标签

% 在标题前后添加样式，下面这些pretitle都是为了让标题居中，然后顺便调了一些格式
\pretitle{\begin{center}\Huge\bfseries}
\posttitle{\end{center}\vspace{2ex}}
\preauthor{\begin{center}\Large}
\postauthor{\end{center}\vspace{1ex}}
\predate{\begin{center}\large}
\postdate{\end{center}}

% 这里写标题，上面的-title后缀的都是调格式的
% \textbf是可以使文字粗体
\title{\huge \textbf{Balanced Round}}
%\author{Your Name} %写作者名字
%\date{\today}      %写日期，不写默认也会有日期


%titleformat是为了去掉后面的section前的编号
\titleformat{\section}{\normalfont\Large\bfseries}{}{0em}{}

\begin{document}  % 开始文档内容，文章结尾是\end{document}

\maketitle  % 创建标题、作者和日期

\section{1 Question(Copied)}  % 创建一个章节标题，因为前面对section设置去除了标题前标号，所以，手动设置编号为1

%默认情况下，在一个新的 section 或 subsection 开始后，第一个段落不会自动缩进。如果你想让段落自动缩进，你可以考虑在 \section 命令之后插入一个空行，然后再开始段落。这样段落就会自动缩进。这是一个示例：
\textbf{}  %在section下行加一个\textbf可以使下面的文章格式缩进对齐

You are the author of a Codeforces round and have prepared $n$ problems you are going to set, problem $i$ having difficulty $a_{i}$. You will do the following process:

1. Remove some (possibly zero) problems from the list;

2. Rearrange the remaining problems in any order you wish.

A round is considered balanced if and only if the absolute difference between the difficulty of any two consecutive problems is at most $k$.

What is the minimum number of problems you have to remove so that an arrangement of problems is balanced?

\section{2 Model}  % 创建一个章节标题为 "2 Model"
\textbf{}  % 空白文本

\textbf{\textbf{\Large Build Difference Array}}%textbf使变粗体

\textbf{Example:}%我发现newline下要另起一行
\newline %另起新的一行
% \newpage 另起一页
1. Input:
\newline

8 1
\newline

8 3 1 4 5 10 7 3
\newline

2. Output:
\newline

4
\newline

%这里是显示图片，需要先上传图片，然后使用下列代码
%在 figure 环境中，使用 \includegraphics 命令来插入图片。
% 通过参数 [width=0.6\textwidth]，我们将图片的宽度设置为文本宽度的 60%。
% caption 命令用于添加图片的标题，
% label 命令用于给图片添加标签，以便在文中引用。
\begin{figure}[H]
  \centering
  \includegraphics[width=1\textwidth]{1.png}
  \caption*{\textbf{\large 1. Sorted Array and Difference Array}} %加*号可以把图片自动的1 2 3 关掉
  \label{fig:Difference Array}%
\end{figure}

\section{3 Algorithm}  % 创建一个章节标题为 "3 Algorithm"
\textbf{}  % 空白文本

\textbf{Step 1:} Sort the Array

Because the problem description states, "rearrange the remaining problems in any order," we can assume that the array, after removing the minimum number of elements, will be sorted. Therefore, we can attempt to sort the array before performing removal.

\textbf{Step 2:} Build the \textbf{Difference Array}

Since the problem requires that the difference between any two consecutive numbers should be less than or equal to $k$, we need to construct a difference array.

\textbf{Step 3:} Find the Length of the Longest Subarray in the Difference Array that Satisfies the Condition, denoted as $\textbf{Max\_L}$.

\begin{enumerate} %如果想变成子内容，用enumerate 来嵌套
    \item[] \textbf{3.1. About How to Find $\textbf{Max\_}L$}
    
    \begin{enumerate}
        \item  Initialize two variables: $\textbf{Max\_}L = 0$ and $\textbf{Count} = 0$.
        
        $\textbf{Max\_}L$ indirectly holds the final result, and $\textbf{Count}$ keeps track of the current consecutive length.
        
        \item Iterate through the $\textbf{DifferenceArray}$.
        
        \begin{enumerate}
            \item[] If  \textbf{DifferenceArray 's current value} $\leq \textbf{K:}$  %小于等于用\leq
            
            \begin{enumerate}
                \item[] \textbf{Count++}.
                
                \begin{enumerate}
                
                    \item[] If $\textbf{Count} \geq \textbf{Max\_ L:}$
                        \begin{enumerate}
                            \item[]   $\textbf{Update Max\_}L$.
                        \end{enumerate}
                \end{enumerate}               
            \end{enumerate}
            
            \item[] \textbf{Else:}
            
            \begin{enumerate}
                \item[] $\textbf{Count} = 0$. %item好想可以实现换行，把[]加上会去掉编号
                
                (Restart the search for a consecutive subarray.)
            \end{enumerate}
        \end{enumerate}
    \end{enumerate}
\end{enumerate}

\textbf{Step 4:}  $\textbf{Max\_}L+1$

Because there are $n$ values in the difference array, we require $n+1$ values in the original array to represent them. 

\textbf{Step 5:}  Length - $(\textbf{Max\_}L+1)$

The problem requires determining the minimum number of elements to be removed. However, in \textbf{Steps 3} and \textbf{Steps 4}, we find the maximum number of elements that can be retained (which is the reverse of what we need). So, the minimum number of elements to be removed is obtained by subtracting the maximum number of elements retained from the total array length: Length - $(\textbf{Max\_}L+1)$.

\begin{figure}[H]
  \centering
  \includegraphics[width=1\textwidth]{2.png}
  \caption*{\textbf{\large 2. Algorithm Flowchart}} %加*号可以把图片自动的1 2 3 关掉
  \label{fig:Algorithm Flowchart}
\end{figure}

\clearpage

% 插入外部文件 main2.tex
\input{main2.tex}
\end{document}


% %latex函数问题，这里直接复制gpt问题和答案
% ！latex如何表示二分之一
% @ \frac{1}{2}


% ！latex 如何把公式的括号变的大一点，能包住整个函数
% @ 你可以使用 \left 和 \right 命令来调整括号的大小，使其能够包围整个函数
% \[
% \left( \frac{1}{2} \right)
% \]


% ！如何用latex公式表示，一个{包含两种情况，在x=1时，是a+b，在x！=1时，是a-b
% @
% \[
% f(x) =
% \begin{cases}
%     a + b & \text{if } x = 1, \\
%     a - b & \text{if } x \neq 1.
% \end{cases}
% \]
% !{号太小了，请改进公式
% @
% \[
% f(x) =
% \biggl\{
% \begin{array}{ll}
%     a + b & \text{if } x = 1, \\
%     a - b & \text{if } x \neq 1.
% \end{array}
% \biggr.
% \]

% ！latex怎么表示<=
% @ $x \leq y$
% ！大于呢
% @ $x \geq y$
```

