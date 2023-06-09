# 第5课 课后作业

## 第1题 已知 $\tau$ 制作假证明

假设我们想要证明 $p(z) = y$ ，这真实证明生成
$$q(X) = \frac{p(X)-y}{X-z}$$
证明 $\pi = [q(\tau)]_1$ ，多项式的承诺为 $C=[p(\tau)]_1$ .
假设我们知道$\tau$ 则可以构造
$$q(\tau)_{fake}=\frac{p(\tau)-y'}{\tau - z} \ (y \neq y') $$
则可以构造一个假的商多项式，即可作为一个假的证明。
## 第2题  构造向量承诺

假设向量为 $\vec{m} = (m_0, m_1,...m_{k-1})$  ；
证明任意位置$x_i$ 对应 $m_i$ , 使 向量中所有的$x_i$ ，我们先计算$p(x_i) = m_i$  的多项式 $I(X)$ . 可以使用拉格朗日插值法计算多项式$I(X)$ :
$$I(X) = \sum_{i=0}^{k-1}m_i \prod_{j=0\atop j \neq i}^{k-1} \frac{X-x_j}{x_i - x_j}$$
使用这个多项式则可以使用一个群元素来证明这个向量中的任意数量元素。

## 第3题 多重证明

假设我们通过插值法构造 $I(X)$ 使得 $I(x_i) = y_i$ , 那么意味多项式$x_0,x_1,...x_{k-1}$ 都是多项式的零点，令 $Z(X) = \prod_{i = 0}^{k-1} (X-x_i)$ , 则可以根据$I(X)$ 和 $Z(X)$ 计算多项式商值。
$$q(X)=\frac{f(X)-I(X)}{Z(X)}$$ 证明$\pi = [q(\tau)]_1$ ，仅仅是一个群元素。通过$$e(\pi,[Z(\tau)]_2)=e(C - [I(\tau)]_1,[1]_2)$$验证证明是否成立，仅仅使用一个群元素，就可以证明任意数量的计算。
