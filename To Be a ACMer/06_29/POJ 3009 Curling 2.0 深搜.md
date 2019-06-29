### 描述
在MM-21星球上，在这一年他们的奥林匹克竞赛结束之后，卷毛开始流行，但是规则我们的有些不同。这个游戏是在一个标有正方形网格的冰游戏板上进行的。他们只用一块石头。游戏的目的是用最少的步数把石头从起点引到终点。<br>
图1显示了一个游戏板的例子。有些正方形可能被方块占据。有两个特殊的方块，即起点和终点，它们没有被方块占据。(这两个正方形是不同的。)一旦石头开始移动，它就会一直移动，直到碰到一块石头为止。为了把石头带向目标，你可能必须阻止石头撞到一块石头上，然后再扔一次。

石头的运动遵循以下规则:
* 开始的时候，石头一动不动地站在开始的广场上。
* 石头的运动受到x和y方向的限制。禁止对角线移动。
* 当石头静止不动时，你可以把它扔出去，让它动起来。你可以把它扔向任何方向，除非它立即被堵住(图)。2 (a))。
* 一旦扔出去，石头就会一直朝同一个方向移动，直到出现以下情况之一:
  * 石头击中了一块石头(图2(b)， (c))。
    * 这块石头停在它击中的街区旁边的方格上。
    * 石块就消失了。
  * 石头从木板上掉下来了。
    * 比赛以失败告终。
  * 石头到达目标广场。
    * 石头停在那里，游戏以成功告终。
* 在一场比赛中，你扔石头的次数不能超过10次。如果石头在10步内没有达到目标，游戏将以失败告终。<br>
根据规则，我们想知道石头在开始时是否可以达到目标，如果可以，需要的最小步数。<br>
根据图1所示的初始配置，将石头从起点移动到终点需要4步。路线如图3(a)所示。注意当石头达到目标时，板的配置发生了变化，如图3(b)所示。


### 我的WA代码：
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

int h,w;
int mp[22][22];
bool vis[22][22];
struct node{
    int x,y;
}st,ed;
int mov[4][2]={{0,1},{1,0},{0,-1},{-1,0}};

int step,minstep;

bool judge(int x,int y){
    if(x<0||x>=h||y<0||y>=w||mp[x][y]==1)
        return false;
    return true;
}

void DFS(node pos){
   // vis[pos.x][pos.y]=true;
   if(step>10)  return ;

    for(int i=0;i<4;i++){
        node tmp;
        tmp.x=pos.x+mov[i][0];
        tmp.y=pos.y+mov[i][1];
        bool ok=false;///判断某个方向能不能走的一个标志变量

        while(judge(tmp.x,tmp.y)){
            ok=true;
            if(tmp.x==ed.x&&tmp.y==ed.y){
                if(step<minstep)    minstep=step;
                return ;
            }
            tmp.x+=mov[i][0];
            tmp.y+=mov[i][1];
        }
        if(mp[tmp.x][tmp.y]==1&&ok){
            step++;
            mp[tmp.x][tmp.y]=0;
            tmp.x-=mov[i][0];
            tmp.y-=mov[i][1];
            DFS(tmp);
            step--;
            tmp.x+=mov[i][0];///这两步也得复原
            tmp.y+=mov[i][1];
            mp[tmp.x][tmp.y]=1;
        }
    }
}


int main(){
    while(scanf("%d%d",&w,&h)==2&&h!=0){
        getchar();
        for(int i=0;i<h;i++){
            for(int j=0;j<w;j++){
                scanf("%d",&mp[i][j]);
                if(mp[i][j]==2){
                    st.x=i;
                    st.y=j;
                }
                if(mp[i][j]==3){
                    ed.x=i;
                    ed.y=j;
                }
            }
            getchar();
        }
//        for(int i=0;i<h;i++){
//            for(int j=0;j<w;j++){
//                printf("%d",mp[i][j]);
//            }
//            printf("\n");
//        }


        step=1;
        minstep=0x3f3f3f3f;
        DFS(st);
        if(minstep>10)  printf("-1\n");
        else    printf("%d\n",minstep);

    }
    return 0;
}


```
#### 始终WA啊！
[AC代码：](https://blog.csdn.net/liusuangeng/article/details/38985357)
```cpp
    #include <iostream>
    #include <stdio.h>
    #include <string.h>
    #include <string>
    #include <cstdio>
    #include <cmath>
    #define  judge(x,y) x>=1&&x<=n&&y>=1&&y<=m&&map[x][y]!=1
 
    using namespace std;
 
    int n,m,sx,sy,ex,ey; //设置全局变量
    int map[25][25];
 
    //设置方向数组优化深搜代码
    int xx[]={-1,1,0,0};
    int yy[]={0,0,-1,1};
    int step,steps;
 
    void dfs(int x,int y)
    {
 
      if(step>10)return;     //  递归出口，步数大于10步就返回
 
      for(int i=0;i<4;i++)
      {
        int dx=x+xx[i];
        int dy=y+yy[i];
        int ok=0;  //作为某个方向能不能走的一个标志变量
 
        while(judge(dx,dy))
        {
            ok=1;
            if(dx==ex&&dy==ey)
            {
              if(step<steps)steps=step;
            }
            dx+=xx[i]; //搜索整条直线
            dy+=yy[i];
        }
        if(map[dx][dy]==1&&ok)
        {
            step++;
            map[dx][dy]=0;
            dfs(dx-xx[i],dy-yy[i]);
            step--;
            map[dx][dy]=1;
        }
      }
 
    }
 
    int main()
    {
            while(cin>>m>>n)
            {
                if(n==0&&m==0)break;
                memset(map,0,sizeof(map));
                for(int i=1;i<=n;i++)
                 for(int j=1;j<=m;j++)
                  {
                      cin>>map[i][j];
                      if(map[i][j]==2){sx=i;sy=j;}
                      if(map[i][j]==3){ex=i;ey=j;}
                  }
                step=1;
                steps=1000000;
                dfs(sx,sy);
 
                if(steps>10) cout<<-1<<endl;
                else  cout<<steps<<endl;
            }
            return 0;
    }
```



