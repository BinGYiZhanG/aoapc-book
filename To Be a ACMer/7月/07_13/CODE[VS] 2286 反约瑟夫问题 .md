[题目链接](http://codevs.cn/problem/2286/)

反约瑟夫问题，就是反过来的求编号
本题我不会递推，发现一篇[好文](https://blog.csdn.net/u011500062/article/details/72855826)：感谢！



### 约瑟夫问题模板代码
![](https://github.com/BinGYiZhanG/aoapc-book/blob/master/To%20Be%20a%20ACMer/Images/20170604001714345.png)
```cpp
int cir(int n,int m)
{
    int p=0;
    for(int i=2;i<=n;i++)
    {
        p=(p+m)%i;
    }
    return p+1;//求的是编号
}

```

### AC代码:
#### 枚举m时不应该存在范围，m可以大于n，没通过的样例就是
```
120 26 
124
```
```cpp
#include <iostream>
#include <cstdio>
#include <algorithm>
#include <cstring>
using namespace std;

int cir(int n,int m)
{
    int p=0;
    for(int i=1;i<=n;i++)///i从1开始还是2开始都一样，反正胜利者的下标都为0
    {
        p=(p+m)%i;
    }
    return p+1;
}

int main()
{
    int n,m,k;
    scanf("%d%d",&n,&k);
    for(m=1;;m++){
        int y=cir(n,m);
        if(y==k){
            break;
        }
    }
    printf("%d\n",m);
    return 0;
}
```

