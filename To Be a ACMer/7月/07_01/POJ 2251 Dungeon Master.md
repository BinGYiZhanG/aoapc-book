[题目链接](http://poj.org/problem?id=2251)

## 题意

三维DFS

### 我的 Time Exceeded 代码
#### 就是一个单纯的DFS，所以必然超出运行时间
```cpp
#include<iostream>
#include<cstdio>
#include<cstring>
#include<cstdlib>
#include<algorithm>

using namespace std;

char mp[35][35][35];
/*6维，而非12维
int mov[12][3]={{-1,0,1},{-1,1,0},{-1,0,-1},{-1,-1,0},
                {0,0,1},{0,1,0},{0,0,-1},{0,-1,0},
                 {1,0,1},{1,1,0},{1,0,-1},{1,-1,0}
                };
*/
int mov[6][3]={{1,0,0},{-1,0,0},{0,-1,0},{0,0,1},{0,1,0},{0,0,-1}};
bool vis[35][35][35];
int L,R,C;
int cnt;
int minstep;
struct node{
    int x,y,z;
    bool operator == (const node& rhs)const {
        return x==rhs.x&&y==rhs.y&&z==rhs.z;
    }
}st,ed;

bool islegal(int x,int y,int z){
    if(x<0||x>=R||y<0||y>=C||z<0||z>=L||mp[z][x][y]=='#'||vis[z][x][y]==true)
        return false;
    return true;
}

void DFS(node pos,int step){
    if(pos==ed){
        if(step<minstep)    minstep=step;
        return ;
    }
    for(int i=0;i<6;i++){
        node tmp;
        tmp.x=pos.x+mov[i][1];
        tmp.y=pos.y+mov[i][2];
        tmp.z=pos.z+mov[i][0];
        if(!islegal(tmp.x,tmp.y,tmp.z))    continue;
        vis[tmp.z][tmp.x][tmp.y]=true;
        DFS(tmp,step+1);
        vis[tmp.z][tmp.x][tmp.y]=false;
    }
    return ;
}

int main(){
    while(scanf("%d%d%d",&L,&R,&C)==3&&(L!=0&&R!=0&&C!=0)){
        getchar();
        for(int k=0;k<L;k++){
            for(int i=0;i<R;i++){
                for(int j=0;j<C;j++){
                    scanf("%c",&mp[k][i][j]);
                    if(mp[k][i][j]=='S'){
                        st.x=i;
                        st.y=j;
                        st.z=k;
                    }
                    if(mp[k][i][j]=='E'){
                        ed.x=i;
                        ed.y=j;
                        ed.z=k;
                    }
                }
                getchar();
            }
            if(k!=L-1)
                getchar();
        }
        //getchar();
        /*
        for(int k=0;k<L;k++){
            for(int i=0;i<R;i++){
                for(int j=0;j<C;j++){
                    printf("%c",mp[k][i][j]);
                }
                printf("\n");
            }
            printf("\n");
        }
*/



        minstep=9999999;
        memset(vis,false,sizeof(vis));
  //      fill(vis[0],vis[0]+22*22,false);
        DFS(st,0);
        if(minstep!=9999999)
            printf("Escaped in %d minute(s).\n",minstep);
        else
            printf("Trapped!\n");
    }
    return 0;
}

```
### 我自己又改了两个WA代码,日了
[博客地址](https://www.cnblogs.com/lfri/p/9068564.html)
### DFS+剪枝
```cpp
#include<iostream>
#include<cstdio>
#include<cstring>
#include<cstdlib>
#include<algorithm>

using namespace std;

char mp[35][35][35];
/*
int mov[12][3]={{-1,0,1},{-1,1,0},{-1,0,-1},{-1,-1,0},
                {0,0,1},{0,1,0},{0,0,-1},{0,-1,0},
                 {1,0,1},{1,1,0},{1,0,-1},{1,-1,0}
                };
*/
int step_map[35][35][35];
int mov[6][3]={{1,0,0},{-1,0,0},{0,-1,0},{0,0,1},{0,1,0},{0,0,-1}};
bool vis[35][35][35];
int L,R,C;
int step;
int minstep;
struct node{
    int x,y,z;
    bool operator == (const node& rhs)const {
        return x==rhs.x&&y==rhs.y&&z==rhs.z;
    }
}st,ed;

bool islegal(int x,int y,int z){
    if(x<0||x>=R||y<0||y>=C||z<0||z>=L||mp[z][x][y]=='#'||vis[z][x][y]==true)
        return false;
    return true;
}

void DFS(node pos){
    if(pos==ed){
        if(step<minstep)    minstep=step;
        return ;
    }
    for(int i=0;i<6;i++){
        node tmp;
        tmp.x=pos.x+mov[i][1];
        tmp.y=pos.y+mov[i][2];
        tmp.z=pos.z+mov[i][0];
       // if((!sta[tmp.z][tmp.x][tmp.y])&&islegal())
        if(islegal(tmp.x,tmp.y,tmp.z)){
            step++;
            if(step<step_map[tmp.z][tmp.x][tmp.y]){
            //剪枝二：当前步数已大于曾经过该点的最小步数，停止搜索
                step_map[tmp.z][tmp.x][tmp.y]=step;
                if(step<minstep){
                //剪枝一：当前步数已大于或等于最小步数，停止搜索
                    vis[tmp.z][tmp.x][tmp.y]=true;
                    DFS(tmp);
                    vis[tmp.z][tmp.x][tmp.y]=false;
                }
            }
            step--;
        }
    }
    return ;
}

int main(){
    while(scanf("%d%d%d",&L,&R,&C)==3&&(L!=0&&R!=0&&C!=0)){
        getchar();
        for(int k=0;k<L;k++){
            for(int i=0;i<R;i++){
                for(int j=0;j<C;j++){
                    scanf("%c",&mp[k][i][j]);
                    if(mp[k][i][j]=='S'){
                        st.x=i;
                        st.y=j;
                        st.z=k;
                    }
                    if(mp[k][i][j]=='E'){
                        ed.x=i;
                        ed.y=j;
                        ed.z=k;
                    }
                }
                getchar();
            }
            if(k!=L-1)
                getchar();
        }
        //getchar();
        /*
        for(int k=0;k<L;k++){
            for(int i=0;i<R;i++){
                for(int j=0;j<C;j++){
                    printf("%c",mp[k][i][j]);
                }
                printf("\n");
            }
            printf("\n");
        }
*/

        step=0;
        memset(step_map,0,sizeof(step_map));
        minstep=9999999;
        memset(vis,false,sizeof(vis));
  //      fill(vis[0],vis[0]+22*22,false);
        DFS(st);
        if(minstep!=9999999)
            printf("Escaped in %d minute(s).\n",minstep);
        else
            printf("Trapped!\n");
    }
    return 0;
}
```
### BFS+优先队列
```cpp
#include<iostream>
#include<cstdio>
#include<cstring>
#include<cstdlib>
#include<algorithm>
#include<queue>
using namespace std;

char mp[35][35][35];

int step_map[35][35][35];
int mov[6][3]={{1,0,0},{-1,0,0},{0,-1,0},{0,0,1},{0,1,0},{0,0,-1}};
bool vis[35][35][35];
int L,R,C;
int step;
int minstep;
struct node{
    int x,y,z;
    int step;
 //   bool operator == (const node& rhs)const {
 //       return x==rhs.x&&y==rhs.y&&z==rhs.z;
  //  }
}st,ed,curp;

///判断是否到达终点
bool success(struct node cur){
 //   if(cur==ed)
    if(cur.x==ed.x&&cur.y==ed.y&&cur.z==ed.z)
        return true;
    return false;
}

///判断该点是否合法
bool islegal(int x,int y,int z){
    if(x<0||x>=R||y<0||y>=C||z<0||z>=L||mp[z][x][y]=='#'||vis[z][x][y]==true)
        return false;
    return true;
}


void BFS(){
    struct node nnode;
    queue<node> q;
    q.push(st);
    while(!q.empty()){
        curp=q.front();
        q.pop();
        if(success(curp))
            return ;
        else{
            vis[curp.x][curp.y][curp.z]=true;
            for(int i=0;i<6;i++){
                nnode.x=curp.x+mov[i][1];
                nnode.y=curp.y+mov[i][2];
                nnode.z=curp.z+mov[i][0];
                if(islegal(nnode.x,nnode.y,nnode.z)){
                    nnode.step=curp.step+1;
                    vis[nnode.x][nnode.y][nnode.z]=true;
                    q.push(nnode);
                }
            }
        }
    }
}


int main(){
    while(scanf("%d%d%d",&L,&R,&C)==3&&(L!=0&&R!=0&&C!=0)){
        getchar();
        for(int k=0;k<L;k++){
            for(int i=0;i<R;i++){
                for(int j=0;j<C;j++){
                    scanf("%c",&mp[k][i][j]);
                    if(mp[k][i][j]=='S'){
                        st.x=i;
                        st.y=j;
                        st.z=k;
                    }
                    if(mp[k][i][j]=='E'){
                        ed.x=i;
                        ed.y=j;
                        ed.z=k;
                    }
                }
                getchar();
            }
            if(k!=L-1)
                getchar();
        }

        memset(vis,false,sizeof(vis));
        BFS();
        if(success(curp))
            printf("Escaped in %d minute(s).\n",curp.step);
        else
            printf("Trapped!\n");
    }
    return 0;
}

```
