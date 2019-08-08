### 问题描述
* 给定一个R行C列的地图，地图的每一个方格可能是'#', '+', '-', '|', '.', 'S', 'T'七个字符中的一个，分别表示如下意思：
* '#': 任何时候玩家都不能移动到此方格；
* '+': 当玩家到达这一方格后，下一步可以向上下左右四个方向相邻的任意一个非'#'方格移动一格；
* '-': 当玩家到达这一方格后，下一步可以向左右两个方向相邻的一个非'#'方格移动一格；
* '|': 当玩家到达这一方格后，下一步可以向上下两个方向相邻的一个非'#'方格移动一格；
* '.': 当玩家到达这一方格后，下一步只能向下移动一格。如果下面相邻的方格为'#'，则玩家不能再移动；
* 'S': 玩家的初始位置，地图中只会有一个初始位置。玩家到达这一方格后，下一步可以向上下左右四个方向相邻的任意一个非'#'方格移动一格；
* 'T': 玩家的目标位置，地图中只会有一个目标位置。玩家到达这一方格后，可以选择完成任务，也可以选择不完成任务继续移动。如果继续移动下一步可以向上下左右四个方向相邻的任意一个非'#'方格移动一格。
* 此外，玩家不能移动出地图。
* 请找出满足下面两个性质的方格个数：
  * 1. 玩家可以从初始位置移动到此方格；
  * 2. 玩家不可以从此方格移动到目标位置。
### 输入格式
* 输入的第一行包括两个整数R 和C，分别表示地图的行和列数。(1 ≤ R, C ≤ 50)。
* 接下来的R行每行都包含C个字符。它们表示地图的格子。地图上恰好有一个'S'和一个'T'。
### 输出格式
* 如果玩家在初始位置就已经不能到达终点了，就输出“I'm stuck!”（不含双引号）。否则的话，输出满足性质的方格的个数。
### 样例输入
```
5 5
--+-+
..|#.
..|##
S-+-T
####.
```
### 样例输出
```
2
```
### 样例说明
* 如果把满足性质的方格在地图上用'X'标记出来的话，地图如下所示：
```
　　--+-+
　　..|#X
　　..|##
　　S-+-T
　　####X
```


[题解：双向DFS](https://blog.csdn.net/wingrez/article/details/85132648)

### 坑：
* 起始点是“S”，在DFS时如何处理
* ed的step如何记录，虽然我把ed设为全局变量，但是在DFS中又重新初始化了结点

```cpp
#include <iostream>
#include <cstdio>
#include <cstring>

using namespace std;

struct position{
    int x,y,step;
}st,ed;

char mp[52][52];
bool vis[52][52];
int R,C;
int ans=0;

int dx[]={0,0,-1,1};///左右，上下
int dy[]={-1,1,0,0};

bool islegal(position node){
    int x=node.x,y=node.y;
    if(x<0||x>=R||y<0||y>=C||mp[x][y]=='#'||vis[x][y]==true)
        return false;
    return true;
}

void DFS(position node){
    int x=node.x,y=node.y;
    vis[x][y]=true;
    printf("x:%d,y:%d,step:%d\n",x,y,node.step);
    if(mp[x][y]=='T')  {///node型的ed的step变量没更新
        ed.step=node.step;
        return ;
    }

    if(mp[x][y]=='+'||mp[x][y]=='S'||mp[x][y]=='T'){///可以朝着四个方向移动
        for(int i=0;i<4;i++){
            position tmp;
            tmp.x=x+dx[i];
            tmp.y=y+dy[i];
            if(islegal(tmp)==false) continue;
            tmp.step=node.step+1;
            DFS(tmp);
        }
    }
    else if(mp[x][y]=='-'){
        for(int i=0;i<2;i++){
            position tmp;
            tmp.x=x+dx[i];
            tmp.y=y+dy[i];
            if(islegal(tmp)==false) continue;
            tmp.step=node.step+1;
            DFS(tmp);
        }
    }
    else if(mp[x][y]=='|'){
        for(int i=2;i<4;i++){
            position tmp;
            tmp.x=x+dx[i];
            tmp.y=y+dy[i];
            if(islegal(tmp)==false) continue;
            tmp.step=node.step+1;
            DFS(tmp);
        }
    }
    else if(mp[x][y]=='.'){
        for(int i=3;i<4;i++){
            position tmp;
            tmp.x=x+dx[i];
            tmp.y=y+dy[i];
            if(islegal(tmp)==false) continue;
            tmp.step=node.step+1;
            DFS(tmp);
        }
    }
   // return ;
}



int main(){
    scanf("%d%d",&R,&C);
    for(int i=0;i<R;i++){
        getchar();
        for(int j=0;j<C;j++){
            scanf("%c",&mp[i][j]);
            if(mp[i][j]=='S'){
                st.x=i;
                st.y=j;
            }
            if(mp[i][j]=='T'){
                ed.x=i;
                ed.y=j;
            }
        }
    }

    memset(vis,0,sizeof(vis));
    st.step=0;
    ed.step=0;
  //  printf("%d %d %d %d\n",st.x,st.y,ed.x,ed.y);
    DFS(st);
   // if(ed.step!=0)
    if(vis[ed.x][ed.y]==0){
        printf("I'm stuck!\n");
        return 0;
    }

 //   for(int i=0;i<R;i++){
  //      printf("%s\n",mp[i]);
  //  }

    return 0;
}


```
