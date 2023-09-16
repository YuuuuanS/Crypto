## 安全强度(security level)
定义：加密系统的安全性以比特（bits）为单位进行度量。n位安全性理解为“需要大约2^n次操作才能破解它”。

对于椭圆曲线加密来说，安全性主要涉及到使离散对数问题变得困难(即给定一个点g和一个点g^k（用乘法群表示），找到k必须是不可行的)。
至少需要大约2^n次操作才能实现这一目标，对于今天的标准来说，n > 100左右。

对于配对友好曲线（pairing-friendly curves），离散对数问题在我们使用的三个群中都必须变得困难。因此，为了达到n位安全性，

主群的阶数r必须至少为2^n比特长，因为存在像Pollard的rho算法这样的算法，其成本为O(√r)。

我们的扩展域F_q^k必须足够大，以免容易受到像数域筛选（number field sieve）这样的方法的攻击。

这些措施可以确保在椭圆曲线加密和配对友好曲线中达到n位安全性。