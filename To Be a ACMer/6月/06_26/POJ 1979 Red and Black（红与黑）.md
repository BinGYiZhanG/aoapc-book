做题实在太少了，只顾着背模板，用处不大，下面这个代码，是我背的DFS，但是AC不了
原因：本题实际上是一个判断连通块大小的问题，而非DFS解决背包问题，所以不能用回溯来解决问题
```cpp
vis[tmp.x][tmp.y]=true;
        cnt++;
        DFS(tmp);
        vis[tmp.x][tmp.y]=false;
        cnt--;
```
### 本人WA代码：
```cpp
#include<iostream>
#include<cstdio>
#include<cstring>
#include<cstdlib>
#include<algorithm>

using namespace std;

char mp[22][22];
int mov[4][2]={{0,1},{1,0},{0,-1},{-1,0}};
bool vis[22][22];
int n,m;
int cnt;
struct node{
    int x,y;
}st;

bool islegal(int x,int y){
    if(x<0||x>=n||y<0||y>=m||mp[x][y]=='#'||mp[x][y]=='@')
        return false;
    return true;
}

void DFS(node pos){
    for(int i=0;i<4;i++){
        node tmp;
        tmp.x=pos.x+mov[i][0];
        tmp.y=pos.y+mov[i][1];
        if(!islegal(tmp.x,tmp.y))    continue;
        vis[tmp.x][tmp.y]=true;
        cnt++;
        DFS(tmp);
        vis[tmp.x][tmp.y]=false;
        cnt--;
    }
    return ;
}

int main(){
    while(scanf("%d%d",&m,&n)==2){
        getchar();
        for(int i=0;i<n;i++){
            for(int j=0;j<m;j++){
                scanf("%c",&mp[i][j]);
                if(mp[i][j]=='@'){
                    st.x=i;
                    st.y=j;
                }
            }
            getchar();
        }
        cnt=0;
        fill(vis[0],vis[0]+22*22,false);
        DFS(st);
        printf("%d\n",cnt);
    }
    return 0;
}
```

### AC代码:
### 注：vis置true应该在DFS开始时置，而非在for循环里注，
Good！
```cpp
void DFS(node pos){
    cnt++;
    vis[pos.x][pos.y]=true;
    for(int i=0;i<4;i++){
        node tmp;
        tmp.x=pos.x+mov[i][0];
        tmp.y=pos.y+mov[i][1];
        if(!islegal(tmp.x,tmp.y))    continue;
        DFS(tmp);
    }
    return ;
}
```
Bad！
```cpp
void DFS(node pos){
    for(int i=0;i<4;i++){
        node tmp;
        tmp.x=pos.x+mov[i][0];
        tmp.y=pos.y+mov[i][1];
        if(!islegal(tmp.x,tmp.y))    continue;
        cnt++;
        vis[pos.x][pos.y]=true;
        DFS(tmp);
    }
    return ;
}
```
#### 输出，比正解大1，或者比正解小1

```cpp
#include<iostream>
#include<cstdio>
#include<cstring>
#include<cstdlib>
#include<algorithm>

using namespace std;

char mp[22][22];
int mov[4][2]={{0,1},{1,0},{0,-1},{-1,0}};
bool vis[22][22];
int n,m;
int cnt;
struct node{
    int x,y;
}st;

bool islegal(int x,int y){
    if(x<0||x>=n||y<0||y>=m||mp[x][y]=='#'||mp[x][y]=='@'||vis[x][y]==true)
        return false;
    return true;
}

void DFS(node pos){
    cnt++;
    vis[pos.x][pos.y]=true;
    for(int i=0;i<4;i++){
        node tmp;
        tmp.x=pos.x+mov[i][0];
        tmp.y=pos.y+mov[i][1];
        if(!islegal(tmp.x,tmp.y))    continue;
        DFS(tmp);
    }
    return ;
}

int main(){
    while(scanf("%d%d",&m,&n)==2&&m&&n){
        getchar();
        for(int i=0;i<n;i++){
            for(int j=0;j<m;j++){
                scanf("%c",&mp[i][j]);
                if(mp[i][j]=='@'){
                    st.x=i;
                    st.y=j;
                }
            }
            getchar();
        }
        cnt=0;
        fill(vis[0],vis[0]+22*22,false);
        DFS(st);
        printf("%d\n",cnt);
    }
    return 0;
}
```


