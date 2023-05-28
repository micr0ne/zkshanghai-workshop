# 第7课 课后作业

## 第1题 修改Fibonacci程序，使其成为宽度为 3 的 AIR

$$
\begin{array}{|}
\hline
step & a & b & c \\
i=1 & 1 & 1 & 2 \\
i=2 & 3 & 5 & 8 \\
i=3 & 13 & 21 & 34 \\
\hline
\end{array}
$$

$$
\begin{array}\
f_1(x_1,x_2,x_3,x_1^{next},x_2^{next},x_3^{next}) = A^{next}-B+C \\
f_2(x_1,x_2,x_3,x_1^{next},x_2^{next},x_3^{next}) = B^{next}-A^{next}-C \\
f_3(x_1,x_2,x_3,x_1^{next},x_2^{next},x_3^{next}) = C^{next}-A^{next}-B^{next} \\
\end{array}
$$

## 第2题 写一个仅能在行$i=1$ 上应用RAP的多重集合相等性检查约束吗？
约束当 $i=1$ 时 $\mathcal{L}_{1}(X)=1$ 
$\mathcal{L}_1(X)(f(X)-1)=0$
