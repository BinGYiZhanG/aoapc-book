大概有这几种：

Runtime Error(ARRAY_BOUNDS_EXCEEDED) // array bounds exceed     数组越界
Runtime Error(DIVIDE_BY_ZERO) //divisor is nil                                   除零
Runtime Error(ACCESS_VIOLATION) //illegal memory access                  非法内存读取
Runtime Error(STACK_OVERFLOW) //stack overflow                             系统栈过载

具体解决办法：

　　检查一下数组、指针是否越界；

　　是否除0；

　　检查一下小数组是否符合题意，可以把数组开的大一些；

　　检查一下局部数组变量是否过大。
  
  
--------------------- 
作者：小白vc 
来源：CSDN 
原文：https://blog.csdn.net/abc12580/article/details/51067159 
版权声明：本文为博主原创文章，转载请附上博文链接！
