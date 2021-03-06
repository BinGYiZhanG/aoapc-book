* 解释了反向边的作用
  * PPT7,8,9,10 
* 为什么反向边是有效的?
  * PPT12,13,14,15,16


## POJ 1273 Drainage Ditches
### 描述

每当约翰的田里下雨，贝西最喜欢的三叶草地里就会形成一个池塘。这意味着三叶草被水覆盖了一段时间，需要很长时间才能重新生长。因此，农夫约翰建了一套排水沟，这样贝西的苜蓿地就不会被水覆盖了。相反，水被排到附近的小溪。作为一名一流的工程师，农夫约翰还在每条水沟的开头安装了调节器，这样他就能控制水流进水沟的速度。<br>
农夫约翰不仅知道每分钟每条沟渠能输送多少加仑的水，还知道沟渠的精确布局，这些沟渠从池塘里流出，相互流入，形成一个潜在的复杂网络。<br>
根据所有这些信息，确定水从池塘中进入小溪的最大速度。对于任何给定的沟渠，水只朝一个方向流动，但可能有一种方式可以让水在一个圆圈中流动。<br>

### 输入

输入包括多种样例。
* 对于每种情况，第一行包含两个空格分隔的整数，N (0 <= N <= 200)和M (2 <= M <= 200)。N是农民约翰挖的沟的数目。M是这些沟渠的交叉点个数。
* 交叉口1是池塘（起点）。交叉口M是终点。
* 下面N行中的每一行都包含三个整数，Si、Ei和Ci。Si和Ei (1 <= Si, Ei <= M)表示该沟渠流经的交叉口。水将通过这条沟从Si流到Ei。Ci (0 <= Ci <= 10,000,000)是水流通过沟渠的最大速度。


