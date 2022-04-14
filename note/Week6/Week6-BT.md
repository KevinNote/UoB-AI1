# Week 6: Bayers' Theorem/贝叶斯定理

## Terminology/术语

- Input Attribute = Independent Var. = Input Var.
- Output Attribute = Dependent Var. = Output Var. = Label (Classification)
- Predictive Model = Classifier (Classification) = Hypothesis (Statistical Learning)

## Formula/公式

$$
P(X, Y) = P(X\mid Y)P(Y)=P(Y\mid X)P(X)
\\
\Downarrow
\\
P(X\mid Y)P(Y)=P(Y\mid X)P(X)
\\
\Downarrow
\\
P(X\mid Y)=\frac{P(Y\mid X)P(X)}{P(Y)}
$$

我们使用其在可能性推理之中（probabilistic inference）。

## Example

考虑数据集

| Days  | Sunny ($X_1$) | Windy ($X_2$) | Tennis ($Y$) |
| ----- | ------------- | ------------- | ------------ |
| Day 1 | Yes           | No            | Yes          |
| Day 2 | Yes           | No            | Yes          |
| Day 3 | Yes           | Yes           | Yes          |
| Day 4 | No            | Yes           | No           |
| Day 5 | No            | No            | No           |
| Day 6 | No            | Yes           | No           |

如果我们只考虑 Windy ($X_2$)

| Frequency Table | Tennis = Y | Tennis = N | Total |
| --------------- | ---------- | ---------- | ----- |
| Windy = Y       | 1          | 2          | 3     |
| Windy = N       | 2          | 1          | 3     |
| Total           | 3          | 3          | 6     |

$$
\begin{aligned}
&P(W\mid T)           & = 1/3\\
&P(\neg W\mid T)      & = 2/3\\
&P(W\mid \neg T)      & = 2/3\\
&P(\neg W\mid \neg T) & = 1/3\\
\\
&P(W)      &= 3/6 &= 1/2\\
&P(\neg W) &= 3/6 &= 1/2\\
&P(T)      &= 3/6 &= 1/2\\
&P(\neg T) &= 3/6 &= 1/2
\end{aligned}
$$

我们应用 Bayes' Theorem:

$$
\begin{aligned}
&P(c\mid a) &=& \frac{P(a\mid c)P(c)}{P(a)}\\
&P(T\mid W) &=& \frac{P(W\mid T)P(T)}{P(W)}\\
&           &=& \frac{1/3\cdot 1/2}{1/2}\\
&           &=& 1/3\\
\end{aligned}
$$

对于条件 $W$，我们需要判断 $T$ 的概率，为此我们可以获得

$$
\begin{aligned}
&P( T\mid W) &=& 1/3\\
&P(\neg T\mid W) &=& 2/3\\
&\max_c P(c\mid a) &=& \max\{1/3, 2/3\}=2/3\\
\end{aligned}
$$

## Normalising Factor

### 1 Independent Var.

$$
\begin{aligned}
&P(c\mid a) &=& \frac{P(a\mid c)P(c)}{P(a)}\\
&P(T\mid W) &=& \frac{P(W\mid T)P(T)}{P(W)}\\
&P(\neg T\mid W) &=& \frac{P(W\mid T)P(\neg T)}{P(W)}\\
\end{aligned}
$$

对于上述，我们可以将 $1/P(W)$ 看作常数 $\alpha$ (normalisation factor)，而其分布 $P(W)$ 则看作 $\beta$，因此 $\alpha=1/\beta$

进行通用化：

$$
\begin{aligned}
P(c\mid a) &= \frac{P(a\mid c)P(c)}{P(a)}\\
\beta &= P(a)\\
      &= \sum_{c\in \mathbb{y}}P(c)P(a\mid c)\\
\end{aligned}
$$

对于 $\beta$，我们可以认为是把所有情况的 $P(a)$ 都合并起来了：
$$
\begin{aligned}
P(a) =& P(a\mid c=1)P(c=1)\\
     &+ P(a\mid c=2)P(c=2)\\
     &+ P(a\mid c=3)P(c=3)\\
     &+ \cdots\\
     =& \sum_{c\in \mathbb{y}}P(c)P(a\mid c)\\
\end{aligned}
$$


### Multiple Independent Var.

$$
\begin{aligned}
P(c\mid a_1, \cdots,a_n)=&\frac{P( a_1, \cdots,a_n\mid c)P(c)}{P(a_1, \cdots,a_n)}\\
=&\frac{P( a_1, \cdots,a_n\mid c)P(c)}{\beta}\\
\end{aligned}
\\
\ 
\\
\begin{aligned}
\beta =& P(a_1, \cdots,a_n)\\
      =& \sum_{c\in \mathbb{y}}P(c)P(a_1, \cdots,a_n\mid c)\\
      =& \sum_{c\in \mathbb{y}}\left( P(c)\prod_{i=1}^{n} P(a_i\mid c)\right)\\
\end{aligned}
\\
\ 
\\
\begin{aligned}
P(c\mid a_1, \cdots,a_n)=&\frac{P( a_1, \cdots,a_n\mid c)P(c)}{\sum_{c\in \mathbb{y}}\left( P(c)\prod_{i=1}^{n} P(a_i\mid c)\right)}\\
=&\alpha P( a_1, \cdots,a_n\mid c)P(c)
\end{aligned}
$$

## Problem: Scaling & Missing Values

对于一个拥有 $n$ 个 Boolean 变量的表格，我们存在 $2^n$ 种可能性，因此需要进行 $O(2^n)$ 步进行处理，而 Naive Bayes 可以解决此问题