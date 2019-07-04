[题目链接](http://poj.org/problem?id=1860)

Bellman-Ford算法<br>
我再一次深切感受到，背模板只是自我安慰而已<br>
[博客地址1](https://www.cnblogs.com/martinue/p/5490523.html)<br>
[博客地址2](http://blog.sina.com.cn/s/blog_8131a3920101dtbn.html)<br>
### 自己改的，还未成功.
```cpp
#include <iostream>
#include <vector>
#include <cstdio>
using namespace std;

//解决单源最短路径问题
//const int MAXV = 210;
const int INF = 1000000000;

struct Node {
    int v;
    double rate,commission;
};

//int G[210][2];
vector<Node> Adj[210];//图G，Adj[u]存放从顶点u出发可以到达的所有顶点
//int n;//n为顶点数，图G使用邻接表实现，MAXV为最大顶点数
//int d[MAXV];//起点到达各点的最短路径长度
//bool vis[MAXV] = { false };//标记数组,true表示已访问

int n,m,st;
double money;
double dis[110];

bool Bellman() {
    //fill(d, d + MAXV, INF);
    for(int i=0;i<=n;i++)
        dis[i]=0;

    dis[st] = money;

    for (int i = 0; i < n; i++) {
        for (int u = 0; u < n; u++) {
            for (int j = 0; j < Adj[u].size(); j++) {
                int v = Adj[u][j].v;
            //    int dis = Adj[u][j].dis;
                double tmp=(dis[u]-Adj[u][j].commission)*Adj[u][j].rate;

                if (dis[u] > dis[v]) {
                    dis[v] = tmp;
                }
            }
        }
    }
    for (int u = 0; u < n; u++) {
        for (int j = 0; j < Adj[j].size(); j++) {
            int v = Adj[u][j].v;
            //    int dis = Adj[u][j].dis;
            double tmp=(dis[u]-Adj[u][j].commission)*Adj[u][j].rate;

            if (dis[u] > dis[v]) {
                return false;
            }
        }
    }
    return true;
}

int main()
{
    int u,v;
    double R1,C1,R2,C2;
    while(scanf("%d%d%d%lf",&n,&m,&st,&money)!=EOF){
        for(int i=0;i<m;i++){
            scanf("%d%d%lf%lf%lf%lf",&u,&v,&R1,&C1,&R2,&C2);
            Adj[u].push_back(Node{v,R1,C1});
            Adj[v].push_back(Node{u,R2,C2});
         //   Adj[v].v=u;
           // Adj[u].rate=R1,Adj[u].commission=C1;
           // Adj[v].rate=R2,Adj[v].commission=C2;
        }
        Bellman();
    }
    return 0;
}
```


