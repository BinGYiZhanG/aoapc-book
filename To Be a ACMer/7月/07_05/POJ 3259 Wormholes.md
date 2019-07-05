
### Bellman-Ford算法核心在于松弛
[博客地址](https://blog.csdn.net/lyy289065406/article/details/6645790)

```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
using namespace std;

int dis[1001];
const int max_w=10001;

class weight{
public:
    int s,e,t;
}edge[5200];

int N,M,W_h;

int all_e;

bool bellman(void){
    bool flag;

    for(int i=0;i<N-1;i++){
        flag=false;
        for(int j=0;j<all_e;j++){
            if(dis[edge[j].e]>dis[edge[j].s]+edge[j].t){
                dis[edge[j].e]=dis[edge[j].s]+edge[j].t;
                flag=true;
            }
        }
        if(!flag)
            break;
    }

    for(int k=0;k<all_e;k++)
        if(dis[edge[k].e]>dis[edge[k].s]+edge[k].t)
            return true;

    return false;
}

int main(){
    int u,v,w;
    int F;
    scanf("%d",&F);
    while(F--){
        fill(dis,dis+1001,max_w);
        scanf("%d%d%d",&N,&M,&W_h);
        all_e=0;

        for(int i=1;i<=M;i++){
            scanf("%d%d%d",&u,&v,&w);
            edge[all_e].s=edge[all_e+1].e=u;
            edge[all_e].e=edge[all_e+1].s=v;
            edge[all_e++].t=w;
            edge[all_e++].t=w;
        }

        for(int j=1;j<=W_h;j++){
            scanf("%d%d%d",&u,&v,&w);
            edge[all_e].s=u;
            edge[all_e].e=v;
            edge[all_e++].t=-w;
        }

        ///Bellman-Ford Algorithm
        if(bellman())
            printf("YES\n");
        else
            printf("NO\n");
    }
    return 0;
}
```
