[题目链接](http://poj.org/problem?id=1573)

### 简单模拟题
### 坑：一开始以为如果走路重复的话，要记录走过的方向种类，这完全是无稽之谈，因为如果发生loop情况，肯定包含四个方向,


```cpp
#include <iostream>
#include <cstdio>
#include <string>
#include <algorithm>
#include <cstring>
#include <set>
using namespace std;

///每行每列的范围是1~10
bool vis[12][12];///设置机器人是否访问过
char mp[12][12];///存储地图
int R,C,north_C;///地图的行数，列数，机器人从北面来的列数
struct robot{
    int x,y;
}rob,node,cur;
int mov[4][2]={{-1,0},{0,-1},{1,0},{0,1}};
int asppos[256];
int dis[12][12];///记录步数
//int dis_type[12][12];///记录该步数下，方向的种类
//set<char> st;///记录该步数下，方向的种类
void Init(){
    asppos['N']=0;///根据方向，确定要行进的格数
    asppos['W']=1;
    asppos['S']=2;
    asppos['E']=3;
    memset(vis,0,sizeof(vis));
    memset(dis,0,sizeof(dis));
//    memset(dis_type,0,sizeof(dis_type));
//    st.clear();
}

bool islegal(int x,int y){
    if(x<0||x>=R||y<0||y>=C)
        return false;
    return true;
}

void Simulation(){
    node.x=0,node.y=north_C-1;
    dis[node.x][node.y]=0;
    vis[node.x][node.y]=true;
    while(true){
        cur.x=node.x+mov[asppos[mp[node.x][node.y]]][0];
        cur.y=node.y+mov[asppos[mp[node.x][node.y]]][1];

        if(vis[cur.x][cur.y]==true){///重复
            int preruns=dis[cur.x][cur.y];
            dis[cur.x][cur.y]=dis[node.x][node.y]+1;
            printf("%d step(s) before a loop of %d step(s)\n",preruns,dis[cur.x][cur.y]-preruns);
            break;
        }

        dis[cur.x][cur.y]=dis[node.x][node.y]+1;
        if(islegal(cur.x,cur.y)==false){///如果出界了
            printf("%d step(s) to exit\n",dis[cur.x][cur.y]);
            break;
        }
        node.x=cur.x;
        node.y=cur.y;
        vis[node.x][node.y]=true;
    }
}

int main()
{
    while(scanf("%d%d%d",&R,&C,&north_C)==3){
        if(R==0&&C==0&&north_C==0)
            break;
        getchar();
        for(int i=0;i<R;i++){
            for(int j=0;j<C;j++){
                scanf("%c",&mp[i][j]);
            }
            getchar();
        }
/*
        for(int i=0;i<R;i++){
            for(int j=0;j<C;j++){
                printf("%c",mp[i][j]);
            }
            printf("\n");
        }
*/
        Init();
        Simulation();
    }
    return 0;
}
```
