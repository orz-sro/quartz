
# 分类名称

|名称|涵盖的积分类型|
|---|---|
|**反双曲函数积分**|结果为 $\sinh^{-1}x$、$\cosh^{-1}x$、$\tanh^{-1}x$ 等|
|**含 $\sqrt{a^2+x^2}$ 的积分**|用三角换元 $x=a\tan\theta$ 或双曲换元 $x=a\sinh t$|
|**第二类换元积分（三角换元）**|中国高校教材的通用叫法；英文教材称 Trigonometric Substitution|

---

# 三种核心根式对应的换元

|根式|换元方法|结果类型|
|---|---|---|
|$\sqrt{a^2 - x^2}$|$x = a\sin\theta$|反三角函数|
|$\sqrt{a^2 + x^2}$|$x = a\tan\theta$ 或 $x = a\sinh t$|反双曲函数|
|$\sqrt{x^2 - a^2}$|$x = a\sec\theta$ 或 $x = a\cosh t$|反双曲函数|

---

# 证明

**目标：**

$$\int \frac{1}{\sqrt{1+x^2}}, dx = \ln\left|x + \sqrt{1+x^2}\right| + C$$

**令 $x = \tan\theta$，则 $dx = \sec^2\theta, d\theta$**

$$\sqrt{1+x^2} = \sqrt{1+\tan^2\theta} = \sqrt{\sec^2\theta} = |\sec\theta| = \sec\theta$$

代入积分：

$$\int \frac{1}{\sec\theta} \cdot \sec^2\theta, d\theta = \int \sec\theta, d\theta$$

**计算 $\int \sec\theta, d\theta$：**

$$\int \sec\theta, d\theta = \int \sec\theta \cdot \frac{\sec\theta + \tan\theta}{\sec\theta + \tan\theta}, d\theta$$

令 $u = \sec\theta + \tan\theta$，则 $du = (\sec\theta\tan\theta + \sec^2\theta),d\theta$，于是：

$$= \int \frac{du}{u} = \ln|u| + C = \ln|\sec\theta + \tan\theta| + C$$

**回代 $x$：**

由 $x = \tan\theta$，得 $\sec\theta = \sqrt{1+x^2}$，故：

$$\boxed{\int \frac{1}{\sqrt{1+x^2}}, dx = \ln\left|x + \sqrt{1+x^2}\right| + C}$$

---

> **备注：** 此结果也常写作 $\sinh^{-1}(x) + C$，两者相差常数，等价。


> [!note] 备注 此结果也常写作 $\sinh^{-1}(x) + C$，因为 $\sinh^{-1}(x) = \ln(x+\sqrt{x^2+1})$，两者相差常数，等价。

---

# 推广公式

$$\int \frac{dx}{\sqrt{a^2+x^2}} = \ln\left(x+\sqrt{x^2+a^2}\right)+C \qquad (a>0)$$