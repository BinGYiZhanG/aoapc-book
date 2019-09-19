Bessie想要给她的太空飞船导航通过危险的小行星领域在一个N X N 的方格大小上。方格包含K个小行星（$1 \leq K \leq 10000$），它们方便地位于网格的格点上。<br>

幸运的是，Bessie拥有一种强大的武器，它可以一枪就把任何一排或一列的小行星都蒸发掉。这种武器相当贵，所以她希望零散地使用它。考虑到该区域内所有小行星的位置，找出贝西消灭所有小行星所需的最小射击次数。<br>

### 输入：
* Line 1:两个整数N，K
* Line 2..K+1:每一行包含两个整数R，C，分别代表小行星的横纵坐标

### 输出：
* Line 1:Bessie所需射击的最小次数

### Sample Input
```
3 4
1 1
1 3
2 2
3 2
```

### Sample Output
```
2
```

#### Hint:
输入细节：<br>
接下来的直方图代表数据，“X”是一个小行星，“.”代表空格。<br>
```
X.X
.X.
.X.
```
输出细节：<br>
Bessie或许会朝第1行开火来摧毁（1,1）和（1,3）的小行星，并且它会朝第2列开火摧毁（2,2）和（3,2）的小行星。<br>



* [增广路概念](https://baike.baidu.com/item/%E5%A2%9E%E5%B9%BF%E8%B7%AF)
* [最小点覆盖数等于最大匹配]
  * [1](https://blog.csdn.net/CY05627/article/details/90609736)
  * [2](https://www.cnblogs.com/Currier/p/6535787.html)
* [最小点覆盖，最小边覆盖，最大匹配，最小路径覆盖，最大独立集总结](https://blog.csdn.net/ACMer_ZP/article/details/78570926)


* [题解](https://blog.csdn.net/lyy289065406/article/details/6646007)
