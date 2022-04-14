# Week 6: Naïve Bayes/朴素贝叶斯

## Rule

### Independence

A 独立于（independent of）B 则 $P(A\mid B)=P(A)$


### Conditional Independence

$A$ 和 $B$ 在给定条件 $C$ 条件独立（Conditional Independence of） 则

$$
\begin{aligned}
&P(A, B\mid C)=P(A\mid C)P(B\mid C)\\
\equiv& P(A\mid B, C)=P(A\mid C)
\end{aligned}
$$

## Sample Data

| Days | Rain (X1) | Temp (X2) | Play (Y) |
| ---- | :-------: | :-------: | :------: |
| 1    |    Yes    |    12     |    No    |
| 2    |    No     |    11     |   Yes    |
| 3    |    Yes    |    17     |    No    |

## Categorical Independent Var.

数据类似 Sample Data 中 X1 的 （给出的为分类的），则为 CIV。

如果条件独立成立，则：

$$
\begin{aligned}
P(c\mid a_1, \cdots,a_n)=&\alpha P(c)P( a_1, \cdots,a_n\mid c)\\
=&\alpha P(c)P(a_1\mid c)P(a_2\mid c)\cdots P(a_n\mid c)\\
=&\alpha P(c)\prod_{i=1}^{n}P(a_i\mid c)
\end{aligned}
\\
\text{Where } \alpha=1/\beta, \beta = \sum_{c\in \mathbb{y}}\left( P(c)\prod_{i=1}^{n} P(a_i\mid c)\right)
$$

## Laplace Smoothing

对于 Categorical Inde. Var.，如果表格中出现了未观测到的数据（即表格中存在 0），则应应用 laplace smooth

E.g,

|       | x   | ¬x  | Total |
| ----- | --- | --- | ----- |
| y     | 1   | 0   | 1     |
| ¬y    | 3   | 1   | 4     |
| Total | 4   | 1   | 5     |

¬x | y 存在 0，执行 smooth



|       | x   | ¬x  | Total |
| ----- | --- | --- | ----- |
| y     | 1+1 | 0+1 | 1+2   |
| ¬y    | 3+1 | 1+1 | 4+2   |
| Total | 4+2 | 1+2 | 5+4   |

## Numerical Independent Var./Gaussian Naive Bayes

数据类似 Sample Data 中 X2 的 （给出的为数值的），则为 NIV。

如果条件独立成立，则：

$$
\begin{aligned}
P(c\mid a_1, \cdots,a_n)=&\alpha P(c)P( a_1, \cdots,a_n\mid c)\\
=&\alpha P(c)P(a_1\mid c)P(a_2\mid c)\cdots P(a_n\mid c)\\
=&\alpha P(c)\prod_{i=1}^{n}P(a_i\mid c)
\end{aligned}
\\
\text{Where } \alpha=1/\beta, \beta = \sum_{c\in \mathbb{y}}\left( P(c)\prod_{i=1}^{n} P(a_i\mid c)\right)
$$

然后使用下列公式预测class：

$$
\max_c[P(c\mid a_1,\cdots, a_n)]
$$

通常来说，我们会对参数进行高斯分布，先计算出平均值和标准差：

$$
\mu = \frac{1}{n}\sum_{i=1}^{n}a_i\\
\sigma^2=\frac{1}{n-1}\sum_{i=1}^{n}(x_i-\mu)^2
$$

然后计算出其高斯。

假设我们存在布尔标签 Y 和参数 X。我们可以计算
1. Y 时，X 的 $\mu, \sigma^2$
2. 计算 Y 的高斯函数
3. ¬Y 时，X 的 $\mu, \sigma^2$
4. 计算 ¬Y 的高斯函数

因此我们可以获得对应函数，得出 $P(Y\mid X=a)$ 和 $P(¬Y\mid X=a)$。

## Pros & Cons

Pros
- 易于实现并可以快速预估
- 在多类型预测工作良好
- 适用于 categorical var

Cons
- 未观测到的数据需要Smooth技术
- 对于 Numerical Var，高斯分布被强假设了
- 不适用于回归