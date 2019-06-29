[题目链接](http://poj.org/problem?id=3278)
## 题意
利用+1，-1，*2 求出n转换到k的最小步数

### 我的WA代码

**A不过原因:**
* 没考虑到该数是否入过队，即没进行vis处理
* 进行操作的数，没有判断是否合法

```cpp
#include <iostream>
#include <cstdio>
#include <algorithm>
#include <vector>
#include <string>
#include <cstring>
#include <cstdlib>
#include <queue>
using namespace std;

const int maxn= 100010;
int n,k;
int d[maxn];
int mind=0x3f3f3f3f;
bool vis[maxn];

void BFS(){
    queue<int> q;
    q.push(n);
    while(!q.empty()){
        int top=q.front();
        q.pop();
        if(top==k){
            if(d[k]<mind){
                mind=d[k];
                continue;
            }
        }
        int walking1=top+1;
        int walking2=top+2;
        int teleport=top*2;
        d[walking1]=d[top]+1;
        d[walking2]=d[top]+1;
        d[teleport]=d[top]+1;
        q.push(walking1);
        q.push(walking2);
        q.push(teleport);
    }
}


int main(){
    while(scanf("%d%d",&n,&k)==2){
        fill(d,d+maxn,0);
        fill(vis,vis+maxn,false);
        BFS();
        printf("%d\n",mind);
    }
}

```

### AC代码
```cpp
#include <iostream>
#include <cstdio>
#include <algorithm>
#include <vector>
#include <string>
#include <cstring>
#include <cstdlib>
#include <queue>
using namespace std;

const int maxn= 100010;
int n,k;
int d[maxn];
int mind=0x3f3f3f3f;
bool vis[maxn];

int BFS(){
    queue<int> q;
    q.push(n);
    while(!q.empty()){
        int top=q.front();
        q.pop();
        if(top==k){
            return d[top];
        }
        int walking1=top+1;
        if(walking1>=0&&walking1<100001&&vis[walking1]!=true){
            d[walking1]=d[top]+1;
            q.push(walking1);
            vis[walking1]=true;
        }
        int walking2=top-1;
        if(walking2>=0&&walking2<100001&&vis[walking2]!=true){
            d[walking2]=d[top]+1;
            q.push(walking2);
            vis[walking2]=true;
        }
        int teleport=top*2;
        if(teleport>=0&&teleport<100001&&vis[teleport]!=true){
            d[teleport]=d[top]+1;
            q.push(teleport);
            vis[teleport]=true;
        }
    }
    return -1;
}


int main(){
    while(scanf("%d%d",&n,&k)==2){
        fill(d,d+maxn,0);
        fill(vis,vis+maxn,false);
        mind=BFS();
        printf("%d\n",mind);
    }
}
```
