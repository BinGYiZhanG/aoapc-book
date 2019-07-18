### 描述
晶格点是有序对(x, y)其中x和y都是整数。给定三角形顶点的坐标(恰好是格点)，您要计算完全位于三角形内部的格点的数量(三角形边缘上的点或三角形顶点上的点不计算)。

### 输入
(x1,y1),(x2,y2),(x3,y3)三个点

### 输出
内部格点数

![](https://github.com/BinGYiZhanG/aoapc-book/blob/master/To%20Be%20a%20ACMer/Images/07181956.png)

```cpp
第二道 用到pick定理的题目，一直错在一个地方了，后来才发现，
代码：
#include <iostream>
#include <cstdio>
#include <cstring>
#include <cmath>
using namespace std;
 
 
int gcd(int a,int b)
{
    if(!a || !b)
    {
        return a>b?a:b;
    }
    else
    {
        return b==0? a: gcd(b,a%b);
    }
}
int main()
{
    int x1,y1,x2,y2,x3,y3;
    while(true)
    {
        cin>>x1>>y1>>x2>>y2>>x3>>y3;
        if(!x1&&!y1&&!x2&&!y2&&!x3&&!y3)
        {
            break;
        }
        int sum=0.5*abs((x2-x1)*(y3-y1)-(x3-x1)*(y2-y1));//这里忘记加abs了，一直WA
        int k1=gcd(abs(x1-x2),abs(y1-y2));
        int k2=gcd(abs(x1-x3),abs(y1-y3));
        int k3=gcd(abs(x3-x2),abs(y3-y2));
        int i=sum+1-(k1+k2+k3)/2;
        cout<<i<<endl;
    }
    return 0;
}
```


