在PopPush城市这是一条著名的铁路站。那里的城市难以置信地多山的。在上个世纪末车站被建立。不幸的是，经费被严格地限制在那时。
建立一个表面的轨道是可能的。而且，此外，事实证明，该站可能只是一个死胡同(见图)，由于缺乏可用的空间，它只能有一个轨道。<br>

当地的传统是，每辆从A方向驶来的列车都会继续沿着B方向行驶，而列车的车厢也会以某种方式重组。
假定从A方向驶来的列车有N（$\leq $1000）节车厢序号是按递增序的1,2,3,...，N。
列车重组主管必须知道是否有可能调集继续往B方向行驶的列车，使其顺序为a1。a2，…,一个。
帮助他并编写一个程序来决定是否有可能获得所需的列车顺序。
您可以假设，在进入车站之前，单节车厢可以与列车断开连接，并且可以自己移动，直到到达B方向的轨道上。
你也可以假设在任何时候可以有尽可能多的车厢在车站。
但是，一旦一辆客车进入车站，它就不能从A方向返回轨道，而且一旦它从B方向离开车站，它也不能返回车站。

### 输入：

输入文件包含若干行。每一块除了最后是描述一节火车和尽可能多的重组的需要。<br>
在块的每一行中都有一个1,2，…块的最后一行只包含“0”。<br>
最后一个块只包含一行包含“0”<br>

### 输出：


### Sample Input
```
5
1 2 3 4 5
5 4 1 2 3
0
6
6 5 4 3 2 1
0
0
```

### Sample Output
```
Yes
No
Yes
```

### 注意：每组数据输入结束之后，存在换行,不然报```Presentation Error```
```cpp
#include <iostream>
#include <cstdio>
#include <stack>
using namespace std;

const int maxn=1010;
int a[maxn];

int main()
{
    int N;
    while(scanf("%d",&N)==1){
        if(N==0)
            break;
        while(scanf("%d",&a[1])){
            if(a[1]==0){
                printf("\n");
                break;
            }
            for(int i=2;i<=N;i++)
                scanf("%d",a+i);

            stack<int> st;
            int cur=1;
            for(int i=1;i<=N;i++){
                st.push(i);

                while(!st.empty()&&st.top()==a[cur]){
                    cur++;
                    st.pop();
                }

            }
            if(!st.empty())
                printf("No\n");
            else
                printf("Yes\n");
        }
    }

    return 0;
}
```


