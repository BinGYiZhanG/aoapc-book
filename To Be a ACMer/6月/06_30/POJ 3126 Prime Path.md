[题目链接](http://poj.org/problem?id=3126)

## 题意

求从给定数到目标数的最小素数变换个数

### 从第160个到第1230个素数就包含了1000~9999的全部素数
![](https://github.com/BinGYiZhanG/aoapc-book/blob/master/To%20Be%20a%20ACMer/Images/06302052.png)

### 我的WA代码
**注：** 样例过了，但是A不了。

```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
#include <algorithm>
#include <cmath>
#include <queue>
using namespace std;

const int maxn=10010;
bool vis[maxn];
int d[maxn];
int st,ed;

bool isprime(int n){
    if(n<=1)    return false;
    int sqr=(int)sqrt(1.0*n);
    for(int i=2;i<=sqr;i++){
        if(n%i==0)
            return false;
    }
    return true;
}

int a[4];
void toarray(int n){
    int cnt=0;
    while(n){
        a[cnt++]=n%10;
        n/=10;
    }
    reverse(a,a+4);
}

int toint(){
    int res=0;
    for(int i=0;i<4;i++){
        res=res*10+a[i];
    }
    return res;
}

void BFS(int st){
    queue<int> q;
    q.push(st);
    while(!q.empty()){
        int top=q.front();
        q.pop();
        toarray(top);
       if(top==ed)
            return ;
        for(int i=0;i<10;i++){
            for(int j=0;j<4;j++){
                if(i!=a[j]){
                    int tmp=a[j];
                    a[j]=i;
                    int tmpres=toint();
                    if(!isprime(tmpres)||vis[tmpres]==true){
                        a[j]=tmp;
                        continue;
                    }
                    d[tmpres]=d[top]+1;
                    q.push(tmpres);
                    a[j]=tmp;
                    vis[tmpres]=true;
                }
            }
        }
    }
}


int main()
{
    int T;
    scanf("%d",&T);
    while(T--){
        fill(vis,vis+maxn,false);
        fill(d,d+maxn,0);
        scanf("%d%d",&st,&ed);
        BFS(st);
        printf("%d\n",d[ed]);
    }
    return 0;
}


```

### AC代码：
### 加了一个tmpres<1000，退出的判断，然后A了
```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
#include <algorithm>
#include <cmath>
#include <queue>
using namespace std;

const int maxn=10010;
bool vis[maxn];
int d[maxn];
int st,ed;

bool isprime(int n){
    if(n<=1)    return false;
    int sqr=(int)sqrt(1.0*n);
    for(int i=2;i<=sqr;i++){
        if(n%i==0)
            return false;
    }
    return true;
}

int a[4];
void toarray(int n){
    int cnt=0;
    while(n){
        a[cnt++]=n%10;
        n/=10;
    }
    reverse(a,a+4);
}

int toint(){
    int res=0;
    for(int i=0;i<4;i++){
        res=res*10+a[i];
    }
    return res;
}

void BFS(int st){
    queue<int> q;
    q.push(st);
    while(!q.empty()){
        int top=q.front();
        q.pop();
        toarray(top);
       if(top==ed)
            return ;
        for(int i=0;i<10;i++){
            for(int j=0;j<4;j++){
                if(i!=a[j]){
                    int tmp=a[j];
                    a[j]=i;
                    int tmpres=toint();
                    if(!isprime(tmpres)||vis[tmpres]==true||tmpres<1000){
                        a[j]=tmp;
                        continue;
                    }
                    d[tmpres]=d[top]+1;
                    q.push(tmpres);
                    a[j]=tmp;
                    vis[tmpres]=true;
                }
            }
        }
    }
}


int main()
{
    int T;
    scanf("%d",&T);
    while(T--){
        fill(vis,vis+maxn,false);
        fill(d,d+maxn,0);
        scanf("%d%d",&st,&ed);
        BFS(st);
        printf("%d\n",d[ed]);
    }
    return 0;
}

```





