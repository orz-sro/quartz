####  伽玛函数是阶乘的推广，它将 ==阶乘== 的定义域从 整数 扩展到了 实数和复数


函数定义： $\Large\Gamma(s)=\int_{0}^{+\infty} e^{-x}x^{s-1} \, dx\,\,(s>0)$
#伽马函数 

如何积分 ，观察到如果 s-1 小于0，此时 x = 0 为函数的瑕点


比较审敛法 极限收敛法 

#瑕点 





此处贴一张伽马函数的图像

![[Pasted image 20260317173908.png]]



##  递推公式： $\Gamma(s+1) = s\Gamma(s) \,(s>0)$
 
 证明如下： 
$$\large
\Gamma(s+1)= \int_{0}^{+\infty}  e^{-x}x^s\,dx=[-x^se^{-x}]^{+\infty}_{0}+ s\int_{0}^{+\infty}  e^{-x}x^{s-1}\, dx =s\Gamma(s)
$$

>[!example] 细节
> 其中  $\large[-x^se^{-x}]_{0}^{+\infty}=\lim_{ x \to \infty }\frac{-x^s}{e^{x}}=0$
> 
因为 ==指数函数== 的发散速度大于 ==幂函数== ，因此分母比分子大，结果为0


###  余元公式

当   $\large F(s)F(s-1)=\frac{\pi}{\sin \pi s}\,\,(0<s<1)$

该公式也叫做 余元公式 ，基本上教材都不做证明

通过该公式可以得到   $\large F\left( \frac{1}{2} \right)=\sqrt{ \pi }$



