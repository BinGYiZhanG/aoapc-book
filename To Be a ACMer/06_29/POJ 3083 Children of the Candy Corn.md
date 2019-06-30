玉米地迷宫是万圣节最受欢迎的美食。游客被带着进入迷宫，在寻找出口的过程中，他们必须面对僵尸、挥舞链锯的精神病患者、嬉皮士和其他恐怖分子，在迷宫中漫步。
一种流行的迷宫行走策略保证游客最终会找到出口。简单地选择右边或左边的墙，并遵循它。当然，不能保证哪一种策略(左或右)会更好，而且所采取的路径很少是最有效的。(在出口不在边缘的迷宫上也不行;这些类型的迷宫在这个问题中没有表示。)
作为一个即将被改造成迷宫的麦田的管理者，你需要一个计算机程序，它可以确定左边和右边的路径以及最短的路径，这样你就可以找出哪一种布局最有可能让游客感到困惑。
### 输入
这个问题的输入将从一行开始，其中包含一个整数n，表示迷宫的数量。每个迷宫将由一条宽度为w、高度为h (3 <= w, h <= 40)的线组成，然后是代表迷宫布局的w个字符组成的h条线。墙壁由散列符号('#')表示，空格由句点('.')表示，开头用'S'表示，结尾用'E'表示。
一个“S”和一个“E”将出现在迷宫中，它们将始终位于迷宫的一个边缘，而不是一个角落。迷宫将完全由墙壁('#')包围，唯一的开口是'S'和'E'。“S”和“E”之间还将至少隔一堵墙(“#”)。
您可以假设迷宫出口总是可以从起点到达。
### 输出
对于输入中的每个迷宫，在单行上输出一个人将访问的(包括'S'和'E')左、右和最短路径的方块数量(不一定是唯一的)(按顺序排列)，每个方块之间用一个空格分隔。从一个正方形移动到另一个正方形只允许在水平或垂直方向;不允许沿对角线移动。

#### 题目大意:

给定一个迷宫，S是起点，E是终点，#是墙不可走，.可以走

先输出左转优先时，从S到E的步数

再输出右转优先时，从S到E的步数

最后输出S到E的最短步数

![](https://github.com/BinGYiZhanG/aoapc-book/blob/master/To%20Be%20a%20ACMer/Images/06300953.png)

### 使我加深了对DFS与BFS的用途的理解
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

int mov[4][2]={{-1,0},{0,1},{1,0},{0,-1}};///顺时针

int h,w;///高，宽
bool vis[42][42];
char mp[42][42];
int d[42][42];

int ans1,ans2;
int flag;

struct node{
    int x,y;
}st,ed;

int cnt;

bool judge(int x,int y){
    if(x<0||x>=h||y<0||y>=w||vis[x][y]==true||mp[x][y]=='#')
        return false;
    return true;
}

//face表示的是当前的朝向，step表示的是当前的步数
void dfs1(int x,int y,int step ,int face)//向左走，进行的是顺序的，递归
{
    printf("DFS1\n");
    if(flag == 1)
        return ;
    if(x==ed.x && y==ed.y)
    {
        flag=1;
        ans1 = step;
        return ;
    }
    //根据上一个的朝向判断下一个应该向那转弯
    if(face == 1)
    {
        if(judge(x+1,y)) dfs1(x+1,y,step+1,4);
        if(judge(x,y-1)) dfs1(x,y-1,step+1,1);
        if(judge(x-1,y)) dfs1(x-1,y,step+1,2);
        if(judge(x,y+1)) dfs1(x,y+1,step+1,3);
    }
    else if(face == 2)
    {
        if(judge(x,y-1)) dfs1(x,y-1,step+1,1);
        if(judge(x-1,y)) dfs1(x-1,y,step+1,2);
        if(judge(x,y+1)) dfs1(x,y+1,step+1,3);
        if(judge(x+1,y)) dfs1(x+1,y,step+1,4);
    }
    else if(face == 3)
    {
        if(judge(x-1,y)) dfs1(x-1,y,step+1,2);
        if(judge(x,y+1)) dfs1(x,y+1,step+1,3);
        if(judge(x+1,y)) dfs1(x+1,y,step+1,4);
        if(judge(x,y-1)) dfs1(x,y-1,step+1,1);
    }
    else
    {
        if(judge(x,y+1)) dfs1(x,y+1,step+1,3);
        if(judge(x+1,y)) dfs1(x+1,y,step+1,4);
        if(judge(x,y-1)) dfs1(x,y-1,step+1,1);
        if(judge(x-1,y)) dfs1(x-1,y,step+1,2);
    }
}
void dfs2(int x,int y,int step,int face)//向右走，进行的是逆序的，递归
{
    printf("DFS2\n");
    if(flag == 1)
      return ;
    if(x==ed.x && y==ed.y)
    {
        flag=1;
        ans2 = step;
        return ;
    }
    if(face == 1)
    {
        if(judge(x-1,y)) dfs2(x-1,y,step+1,2);
        if(judge(x,y-1)) dfs2(x,y-1,step+1,1);
        if(judge(x+1,y)) dfs2(x+1,y,step+1,4);
        if(judge(x,y+1)) dfs2(x,y+1,step+1,3);
    }
    else  if(face == 2)
    {
        if(judge(x,y+1)) dfs2(x,y+1,step+1,3);
        if(judge(x-1,y)) dfs2(x-1,y,step+1,2);
        if(judge(x,y-1)) dfs2(x,y-1,step+1,1);
        if(judge(x+1,y)) dfs2(x+1,y,step+1,4);
    }
    else if(face == 3)
    {
        if(judge(x+1,y)) dfs2(x+1,y,step+1,4);
        if(judge(x,y+1)) dfs2(x,y+1,step+1,3);
        if(judge(x-1,y)) dfs2(x-1,y,step+1,2);
        if(judge(x,y-1)) dfs2(x,y-1,step+1,1);
    }
    else
    {
        if(judge(x,y-1)) dfs2(x,y-1,step+1,1);
        if(judge(x+1,y)) dfs2(x+1,y,step+1,4);
        if(judge(x,y+1)) dfs2(x,y+1,step+1,3);
        if(judge(x-1,y)) dfs2(x-1,y,step+1,2);
    }
}

void BFS(){
    queue<node> q;
    q.push(st);
    d[st.x][st.y]=1;
    while(!q.empty()){
        node top=q.front();
        q.pop();
        vis[top.x][top.y]=true;
        //cnt++;
        if(top.x==ed.x&&top.y==ed.y)    break;
        for(int i=0;i<4;i++){
            node tmp;
            tmp.x=top.x+mov[i][0];
            tmp.y=top.y+mov[i][1];
            if(!judge(tmp.x,tmp.y))   continue;
            //vis[top.x][top.y]=true;
            q.push(tmp);
            d[tmp.x][tmp.y]=d[top.x][top.y]+1;
        }
    }
}

int main(){
    int T;
    scanf("%d",&T);
    while(T--){
        scanf("%d%d",&w,&h);
        getchar();
        for(int i=0;i<h;i++){
            for(int j=0;j<w;j++){
                scanf("%c",&mp[i][j]);
                if(mp[i][j]=='S'){
                    st.x=i;
                    st.y=j;
                }
                if(mp[i][j]=='E'){
                    ed.x=i;
                    ed.y=j;
                }
            }
            getchar();
        }
        /*
        for(int i=0;i<h;i++){
            for(int j=0;j<w;j++){
                printf("%c",mp[i][j]);
            }
            printf("\n");
        }
        */
        cnt=0;
        fill(vis[0],vis[0]+42*42,false);
        BFS();

        flag=0;ans1=0;
        dfs1(st.x,st.y,1,1);//一直向左走
        flag=0;ans2=0;
        dfs2(st.x,st.y,1,3);//一直向右走

        printf("%d %d %d\n",ans1,ans2,d[ed.x][ed.y]);
    }
    return 0;
}

```
