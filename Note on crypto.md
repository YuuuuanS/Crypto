## Note on crypto (a bit chaotic)
## 安全强度(security level)
定义：加密系统的安全性以比特（bits）为单位进行度量。n位安全性理解为“需要大约2^n次操作才能破解它”。
- 对于椭圆曲线加密来说，安全性主要涉及到使离散对数问题变得困难(即给定一个点g和一个点g^k（用乘法群表示），找到k必须是不可行的)。至少需要大约2^n次操作才能实现这一目标，对于今天的标准来说，n > 100左右。

- 对于配对友好曲线（pairing-friendly curves），离散对数问题在我们使用的三个群中都必须变得困难。因此，为了达到nbit安全性，

  - 素数群(prime group)的阶数r必须至少为2^n比特长，因为存在像Pollard的rho算法这样的算法，其成本为$O\sqrt(r)$。

  - 我们的扩展域$F_q^k$必须足够大，以免容易受到像数域筛选（number field sieve）这样的方法的攻击。

这些措施可以确保在椭圆曲线加密和配对友好曲线中达到n位安全性。

**期望的安全级别、曲线参数的位大小和相应的嵌入度**[1]
|Security level | Subgroup size r |Extension fields size $q^k$ |Embedding degree (\rou =1 \2)|
| :----- | :--: | -------: | -------: |
| 80 | 160 |960-1280 |6-8 |2^*, 3-4|
| 112 | 224 | 2200 - 3600 | 10 – 16 | 5 – 8 |
| 128 | 256 | 3000 – 5000 | 12 – 20  |6 – 10 |
| 192 | 384 | 8000 – 10000 | 20 – 26|  10 – 13| 
| 256 | 512 | 14000 – 18000 | 28 – 36 | 14 – 18| 

**曲线的及相应的安全强度**
| Curve   | order (bits) |     security level |
| :----- | :--: | -------: |
| BLS12-381 |  255  | 128 |

[1] A Taxonomy of Pairing-Friendly Elliptic Curves

## Library for pairing

- pairing with rust (https://docs.rs/pairing/0.14.2/pairing/). In Tyurek's Github (https://github.com/tyurek), there are two python wrapper for the pairing library. Unfortunately, the pairing library does not optimize the multi-exponentiations and multi-pairing.
- An introduction for bls12-381 (https://hackmd.io/@benjaminion/bls12-381)
- bls12-381 with rust
 - ark_bls12_381 (https://docs.rs/ark-bls12-381/0.4.0/ark_bls12_381/): a python wrapper for this library (https://docs.rs/ark-bls12-381/0.4.0/ark_bls12_381/), which does not support the newest version.
 - blstrs by filecoin (https://github.com/filecoin-project/blstrs)
- the py_ecc (https://github.com/ethereum/py_ecc/tree/master) by ethereum supports secp256k1, alt_bn128, and bls12_381 withou any optimization.
- a python implementation (https://github.com/wborgeaud/python-pippenger) with ecdsa library for fast multi-exponentiations, but does not support bls12-381 curve.
