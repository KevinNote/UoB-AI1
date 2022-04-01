# Cheat Sheet

## Similarity Measures/近似度测量

Euclidean:

$$
d(p, q)=d(p,q)=\sqrt{(q_1-p_1)^2+(q_2-p_2)^2+\cdots+(q_n-p_n)^2}
$$

Manhattan:

$$
d(p, q)=\sum^n_{i=1}{|p_i-q_i|}
$$

Chebyshev:

$$
d(p, q)=\max^n_{i=1}{(|p_i-q_i|)}
$$

Minkowski:

$$
d(p, q)=\left(
  \sum^n_{i=1}{|p_i-q_i|^b}
  \right)^{1/b}
$$

## Clustering Algorithms

| Algo.                   | 确定性           | 簇形状 | 预参数               |
| ----------------------- | ---------------- | ------ | -------------------- |
| Hierarchical Clustering | 是               | 不规则 | 无                   |
| K-means                 | 否：随机的初始点 | 圆形   | 簇数量               |
| GMM                     | 否：随机的初始点 | 圆形   | 簇数量               |
| DBSCAN                  | 否：取决实现     | 不规则 | $\epsilon$, *minPts* |

## Cost Function

### Square loss/L2 loss/Mean Square Error (MSE):

$$
g(\mathbf{w})=
\frac{1}{N}
\sum_{n=1}^N{
    \left(
        f(x^{(n)}; \mathbf{w})
        -
        y^{(n)}
    \right)^2
}
$$

### Cross-entropy

$$
\begin{aligned}
g(\mathbf{w})&=\frac{1}{N}\sum_{n=0}^N Cost(h(\mathbf{x}^{(n)}; \mathbf{w}),y^{(n)})\\
&=\frac{1}{N}\sum_{n=0}^N \left(
    y^{(n)} \log(h(\mathbf{x}^{(n)}; \mathbf{w})) +
    (1-y^{(n)})\log(1-h(\mathbf{x}^{(n)}; \mathbf{w}))
\right)
\end{aligned}
$$

## 常用函数

### Sigmoid 函数

$$
\sigma(u) = \frac{1}{1+e^{-u}}
$$

### 梯度下降

$$
\mathbf{w} = \mathbf{w} - \alpha \nabla g(\mathbf{w})
$$