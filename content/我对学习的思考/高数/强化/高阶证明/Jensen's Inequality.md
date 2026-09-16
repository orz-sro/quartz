# 证明

$f$ 在区间上满足 $f''\ge 0$（下凸），权重 $\lambda_i\ge 0$ 且 $\sum_{i=1}^n\lambda_i=1$，则

$$
f\left(\sum_{i=1}^n\lambda_i x_i\right)\le\sum_{i=1}^n\lambda_i f(x_i)
$$

$f''\le0$（上凸）时不等号反向。几何上：下凸函数的弦在弧的上方，所以函数值的平均 $\ge$ 平均值的函数。

等权形式，考试基本只用这个：

$$
f\left(\frac{x_1+\dots+x_n}{n}\right)\le\frac{f(x_1)+\dots+f(x_n)}{n}
$$

什么时候想到它：要证的是"n 项的和（或积）与平均之间的关系"，且每一项都能写成同一个函数 $f$。

套路固定三步：

1. 设函数：乘积或几何平均设 $\ln x$（把乘法变加法），平方和设 $x^2$，三角和设对应的三角函数；

2. 求 $f''$ 判凹凸，这一步必须写出来，漏了扣分；

3. 代等权形式，把题目条件（比如 $A+B+C=\pi$）代进去化简。

>[!example] 例1
> $x_1,\dots,x_n>0$，证明 $\sqrt[n]{x_1\cdots x_n}\le\dfrac{x_1+\dots+x_n}{n}$。
>
> 乘积结构，设 $f(x)=\ln x\ (x>0)$，$f''(x)=-\dfrac{1}{x^2}<0$，上凸，等权取 $\ge$：
> $$
> \frac{\sum_{i=1}^n\ln x_i}{n}\le\ln\frac{\sum_{i=1}^n x_i}{n}
> $$
> 左边就是 $\ln(x_1\cdots x_n)^{1/n}$，$\ln$ 单调递增，两边取 $e$ 指数即证。

>[!example] 例2
> 锐角 $\triangle ABC$ 中，证明 $\sin A+\sin B+\sin C\le\dfrac{3\sqrt3}{2}$。
>
> 设 $f(x)=\sin x\ (0<x<\tfrac{\pi}{2})$，$f''=-\sin x<0$，上凸：
> $$
> \frac{\sin A+\sin B+\sin C}{3}\le\sin\frac{A+B+C}{3}=\sin\frac{\pi}{3}=\frac{\sqrt3}{2}
> $$
> 两边乘 3 即证。

平方和那道是下凸方向：设 $f(x)=x^2$，$f''=2>0$，得 $\dfrac{\sum x_i^2}{n}\ge\left(\dfrac{\sum x_i}{n}\right)^2$。

严格凸/凹时，当且仅当 $x_1=\dots=x_n$ 取等，判断能不能取等时要用到。

证明是归纳法：先证 $n=2$（端点为零加 $g''\ge0$），再对点数归纳合并，考研不要求默写，知道有这回事就行。