# 第3课 课后作业

## 第1题 二次非剩余 Quadratic nonresidue
- 完备性：根据二次剩余性质
1. 与m互质的$s\in \mathbb{Z}_m$ ，若$s^2$ 与 m 互质则一定为二次剩余  
2. 二次剩余与非二次剩余相乘为非二次剩余。
故Prover和verify 都按照协议进行，则verify总是会接收证明。
- 可靠性：
由于$s^2x$ 和$s^2$ 具有不可区分性，故若$QR(m,x)=1$ ,那么prover 接收计算$QR(m,y)$时的结果错误的概率为$\frac{1}{2}$ ，则verify总能以$\ge \frac{1}{2}$ 的概率聚拒绝prover的结果。
## 第2题 二次剩余 Quadratic residue
**完备性**
根据协议如果$QR(m,x)=1$ ，验证者总能得到$y\equiv u^2x \pmod m$ 或者$y\equiv u^2x \pmod m$
可靠性：因为
b= 0 时 $y\equiv xt^2 \equiv u^2x \pmod m$
b= 1 时$y\equiv xt^2 \equiv u^2 \equiv s^2t^2\pmod m$ 
由于$QR(m,x)=0$，$y$ 一定不存在 $y\equiv u^2 \pmod m$  故verify 总会以超过$\frac{1}{2}$的概率拒绝。 
**知识可靠性**
该定义表示$prover$ 没有知识时会导致 $verify$ 验证失败，逆否命题则是如果$verify$验证成功则说明$prover$一定有知识。
这里假设$verify$具有同时查询$b\in{0,1}$的能力。
1. verify 先发送b=0 ，则prover 返回 u=t 给验证者，verify 验证$y \equiv u^2x \pmod m$ 是否相等，若相等则返回第一步
2. verify 先发送b=1 ，则prover 返回 u=st 给验证者，verify 验证$y \equiv u^2 \pmod m$ 是否相等。
3. 此时verify 同时拥有$t,st$,这很易提取出$s$，这证明了prover 具有知识可靠性。若无法提取出$s$,则说明prover 不具有知识可靠性。
**零知识**
这里假设有一个模拟器可以生成证明，且这个模拟器是没有任何知识的，若没有知识的模拟器生成的证明也能够通过verify的验证，说明协议具有零知识性。当然这里模拟器也需要具备一定的能力，即如果模拟器如果能从verify处知道b的值，就比较易构成证明。
1. 假设模拟器生成一个证明$u'\in \mathbb{Z}_m$  。
2. 随机选择一个随机数$b’ \in\{0,1\}$，并根据b的值构造等式$b=0,\ y \equiv u'^2 x \pmod m$ ,  若b =1时 $y\equiv u'^2 \pmod m$ 。
3. 随后模拟器接收，verify的发送的b，若$b' \neq b$ 我们则利用模拟器的额外能力（时光倒流的能力）返回第一步，并重新选择$b'$的值返回结果，最终模拟器能通过验证。
4. 这里模拟器没有知识也能通过验证，说明了恶意的verify无法提取知识，因为模拟器根本就没有知识。由此则证明了零知识性。
## 第3题 双线性自映射意味着DDH的失效 Self-pairing implies failure of DDH
如果需要在双线性曲线上判断$\alpha\beta g=y$ ，则只需要利用双线性映射的性质计算：
$$
e(\alpha g, \beta g) = e(g,g)^{\alpha \beta}= e(\alpha\beta g, g)=e(y,g)
$$    计算并判断上式是否相等时，即可判断$\alpha\beta g=y$
## 第4题 BLS 签名聚合 BLS signature aggregation
验证算法始终能接受正确的签名。因为验证签名阶段
$$
\begin{array}
e(g_0,\sigma) = e(g_0, \alpha H(m))\\
e(pk,H(m)) = e(\alpha g_0, H(m))= e(g_0,\alpha H(m))
\end{array}
$$由上可知验证阶段的等式相等，因此在都诚实的情况下都可以通过验证。
若攻击者伪造签名者需要根据公钥反推私钥，即$pk=\alpha g_0$ 中计算出$\alpha$这是一个离散对数难题无法在多项式时间内计算出来。

