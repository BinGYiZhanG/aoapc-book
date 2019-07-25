在单处理器系统上并发执行的程序似乎是同时执行的。但是实际上在程序之间单个CPU交替进行，在转换到下一个程序之前，从每一个程序中转换一些指令。<br>
你将模拟并发执行的程序最多10个在一个系统上，并且决定他们将会产生的输出。<br>

正在执行的程序叫做 ```running```,所有等待执行的程序叫做```ready```.一个程序包含不超过25条语句的序列，每一行包含一条终止语句。可获得的语句如下所示：

```
Statement Type Syntax
Assignment variable = constant
Output print variable
Begin Mutual Exclusion lock
End Mutual Exclusion unlock
Stop Execution end

```
一个变量是任意单个小写字母，并且一个整数是一个无符号二进制数小于100。在计算机系统中只有26个变量，并且他们在程序中分配。<br>
因此，在一个程序中对变量赋值影响在另外不同的程序中的打印。所有变量都初始化为0。<br>

每个语句都需要执行整数个时间单位。一个正在运行的程序被允许继续执行指令在一段时间内叫做```quantum```。<br>
当一个程序的时间```quantum```终止时，另一个准备好的程序被选择运行。
任意目前正在执行的指令当时间```quantum```终止时将被允许完成。<br>
   
   
在一个ready queue中对于执行程序将会排队first-in-first-out。准备好的queue的初始顺序与在输入文件的程序的初始顺序相关。这个顺序会改变，然而，作为执行```lock```与```unlock```语句的结果。<br>

```lock```与```unlock```语句被使用无论何时一个程序想要手动的声明
