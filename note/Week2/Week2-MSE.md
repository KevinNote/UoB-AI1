# Week 2: Mathematical Symbols Explanations

## Basic Notations

Set $z$.

$P(x|z)$ means get an element $x$ from set $z$ and apply function $P$ on it.

## GMM

### Formulas

$$P(x)$$
$x$: lower case, one sample

$$
\begin{aligned}
P(X)
&= P(x_1)\cdot P(x_2)\cdots P(x_N)
\\&= \prod^N_{i=1}P(x_i)
\\&= \prod_nP(x_n)
\end{aligned}
$$
$X$: upper case, set of samples, i.e. $x_1, x_2, \cdots, x_N$

### Parameters

$\mu$: 决定了分布的中心点在哪

$\Sigma$: 标准差，决定了函数图像的形状，i.e. 是更圆滑还是更尖锐

$\pi$: 每个集群的权重，i.e.:
在 $k$ 个集合中， $\pi_k=P(Z_k)$

GMM 是为了寻找 $\mu, \Sigma, \pi$ 的最佳组合。

### Transformation

考虑到最终 $P(X)$ 公式中 $\prod_nP(x_n)$ 是难以处理的，因此我们需要进行优化：

$$
\begin{aligned}
   &\ln P(X) = \ln \left(\prod_nP(x_n)\right) \\
  =& \sum_n \ln P(x_n) \\
  =& \sum_n \ln \sum_z (P(x|z) \pi_z)\\
  =& \sum_n \ln \left( \sum_k\left(\pi_k \mathcal{N}(x_n|\mu_k, \Sigma_k)\right) \right)
\end{aligned}
$$

> 延申自 $\ln (ab)=\ln a + \ln b$

