[N皇后问题](http://acm.hdu.edu.cn/showproblem.php?pid=2553)

## 类型：DFS

```cpp
#include <iostream>
#include <cstdio>
#include <cstdlib>
#include <cstring>
using namespace std;

int C[11];
int vis[3][11];

int n,tot;
void search_one(int cur){
    if(cur==n)  tot++;
    else for(int i=0;i<n;i++){
        int ok=1;
        C[cur]=i;
        for(int j=0;j<cur;j++){
            if(C[cur]==C[j]||cur-C[cur]==j-C[j]||cur+C[cur]==j+C[j]){
                ok=0;break;
            }
        }
        if(ok)  search_one(cur+1);
    }
}

void search_two(int cur){
    if(cur==n){
        tot++;
    }
    else for(int i=0;i<n;i++){
        if(!vis[0][i]&&!vis[1][cur+i]&&!vis[2][cur-i+n]){
            C[cur]=i;
            vis[0][i]=vis[1][cur+i]=vis[2][cur-i+n]=1;
            search_two(cur+1);
            vis[0][i]=vis[1][cur+i]=vis[2][cur-i+n]=0;
        }
    }
}


int main(){
    while(scanf("%d",&n)==1&&n!=0){
        tot=0;
        fill(vis[0],vis[0]+3*11,0);///search_two时得初始化
        search_one(0);
        printf("%d\n",tot);
    }
    return 0;
}


```


超时间限制

### 只能打表
```cpp
//打表，表中数据来自dfs
#include<iostream>
#include<cstdio>
#include<cstring>
#include<cstdlib>
#include<algorithm>

using namespace std;

const int maxn=30;
const int INF=(1<<28);

int a[]={1,0,0,2,10,4,40,92,352,724};

int main()
{
    int n;
    while(cin>>n&&n){
        cout<<a[n-1]<<endl;
    }
    return 0;
}
```
