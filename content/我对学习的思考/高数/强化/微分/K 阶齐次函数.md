
k阶齐次函数是指 `当自变量全乘以一个倍数 t 时，函数值会等于原函数值乘以 t 的 k 次方`。

# 基本定义


- 对于函数 \(f(x_1, x_2, \dots, x_n)\)，如果对任意 t > 0（或非零常数），满足：  
    $$f(tx_{1},tx_{2},\dots ,tx_{n})=t^{k}f(x_{1},x_{2},\dots ,x_{n})$$

- 其中 k 就是函数的**齐次阶数**。



# **欧拉定理**


如果 k 阶齐次函数  $f(x_1, x_2, \dots, x_n)$  具有一阶偏导数，那么它满足以下微分方程：

$$x_{1}\frac{\partial f}{\partial x_{1}}+x_{2}\frac{\partial f}{\partial x_{2}}+\dots +x_{n}\frac{\partial f}{\partial x_{n}}=k\cdot f(x_{1},x_{2},\dots ,x_{n}) $$ 
对于二元函数 $f(x, y)$  ，形式则简化为：  

$$x\frac{\partial f}{\partial x}+y\frac{\partial f}{\partial y}=k\cdot f(x,y)$$

主要性质

- **偏导数降阶**：k 阶齐次函数的一阶偏导数是 **k-1 阶**齐次函数。

- **多项式特例**：如果一个 n 元多项式每一项的总次数都相同（例如 x² + 3xy + y²），它就是一个齐次函数，次数即为阶数。