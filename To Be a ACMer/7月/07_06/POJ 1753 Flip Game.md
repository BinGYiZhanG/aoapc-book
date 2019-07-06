[题目链接](http://poj.org/problem?id=1753)

### BFS
### WA

```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
#include <queue>
using namespace std;

char tmmp[4][4];
int mp[4][4];
int mov[4][2]={{-1,0},{0,-1},{1,0},{0,1}};
int vis[4][4];
int dis[4][4];
struct node{
    int x,y;
};

bool judge(){
    ///行比较
    for(int i=1;i<4;i++){
        for(int j=0;j<4;j++){
            if(mp[i-1][j]!=mp[i][j])
                return false;
        }
    }
    ///列比较
    for(int i=0;i<4;i++){
        for(int j=1;j<4;j++){
            if(mp[i][j-1]!=mp[i][j])
                return false;
        }
    }
    return true;
}

bool islegal(node pos){
    if(pos.x<0||pos.x>=4||pos.y<0||pos.y>=4)
        return false;
    return true;
}

void BFS(){
    node tmp;
    queue<node> q;
    ///假设起点,
    q.push(node{0,0});
    while(!q.empty()){
        node top=q.front();q.pop();
        if(judge()) break;
        if(vis[top.x][top.y]==true)///再次翻这个点,
            continue;
        for(int i=0;i<4;i++){
            tmp.x=top.x+mov[i][0];
            tmp.y=top.y+mov[i][1];
            if(!islegal(tmp))   continue;///判断是否出界
            if(mp[tmp.x][tmp.y]==1)
                mp[tmp.x][tmp.y]=0;
            else
                mp[tmp.x][tmp.y]=1;
            dis[tmp.x][tmp.y]=dis[top.x][top.y]+1;
            vis[tmp.x][tmp.y]=true;///判断节点是否再次翻
            q.push(tmp);
        }
    }
}


void flip(node pos){
    int x=pos.x,y=pos.y;
    mp[x][y]=!mp[x][y];
    if(x-1>=0)
        mp[x-1][y]=!mp[x-1][y];
    if(x+1<4)
        mp[x+1][y]=!mp[x+1][y];
    if(y-1>=0)
        mp[x][y-1]=!mp[x][y-1];
    if(y+1<4)
        mp[x][y+1]=!mp[x][y+1];
}

int ans=0;
///b -- 1
///w -- 0
int DFS(node pos,int t){
    node tmp;
    if(judge()){
        if(ans>t)
            ans=t;
        return 0;
    }
    if(pos.x>=4||pos.y>=4)
        return 0;
    for(int i=0;i<4;i++){
        tmp.x=pos.x+mov[i][0];
        tmp.y=pos.y+mov[i][1];
        if(islegal(tmp)==false)    continue;
   //     DFS(tmp,t);
        flip(tmp);
        DFS(tmp,t+1);
        flip(tmp);
    }
    return 0;
}

int main()
{
    memset(vis,false,sizeof(vis));
    memset(dis,0,sizeof(dis));
    for(int i=0;i<4;i++){
        scanf("%s",tmmp[i]);
        for(int j=0;j<4;j++){
            if(tmmp[i][j]=='b')
                mp[i][j]=1;
            else
                mp[i][j]=0;
        }
    }
    node st={0,0};

    BFS();
    DFS(st,0);
    /*
    for(int i=0;i<4;i++){
        for(int j=0;j<4;j++){
            printf("%d ",dis[i][j]);
        }
        printf("\n");
    }
*/
    printf("%d\n",ans);
    return 0;
}

```
## 一，DFS
[博客地址1](https://blog.csdn.net/u013476556/article/details/30781771)
```cpp
#include <stdio.h>
 
const int inf=9999999;
char s[10];
int map[10][10],i,j;
int ans=inf;
 
int panduan()
{
    int x=map[0][0];
    for (i=0; i<4; i++)
    {
        for (j=0; j<4; j++)
        {
            if (map[i][j]!=x)
                return 0;
        }
    }
    return 1;
}
void fan (int x,int y)
{
    map[x][y]=!map[x][y];
    if (x - 1 >= 0)
        map[x-1][y]=!map[x-1][y];
    if (x + 1 < 4)
        map[x+1][y]=!map[x+1][y];
    if (y - 1 >= 0)
        map[x][y-1]=!map[x][y-1];
    if (y + 1 < 4)
        map[x][y+1]=!map[x][y+1];
}
int dfs (int x,int y,int t)
{
    if ( panduan())
    {
        if (ans > t)
            ans = t ;
        return 0;
    }
    if (x >= 4 || y >= 4)
        return 0;
    int nx,ny;
    nx = (x + 1)%4;
    ny = y + ( x + 1 ) / 4;
 
    dfs (nx,ny,t);
    fan (x,y);
 
    dfs (nx,ny,t+1);
    fan (x,y);
 
    return 0;
}
 
int main ()
{
    for (i=0; i<4; i++)
    {
        scanf ("%s",s);
        for (j=0; j<4; j++)
        {
            if (s[j]=='b')
                map[i][j]=0;
            else
                map[i][j]=1;
        }
    }
    dfs (0,0,0);
    if (ans == inf )
        printf ("Impossible\n");
    else printf ("%d\n",ans);
    return 0;
}
```


## 二，状态压缩
[博客地址2](https://www.cnblogs.com/BlackStorm/p/5231470.html)
![](https://github.com/BinGYiZhanG/aoapc-book/blob/master/To%20Be%20a%20ACMer/Images/07061952.png)

### 每行压缩成一个数字
```cpp
#include <stdio.h>

int field[6]={0};
int state[][4]={{8,4,2,1},{12,14,7,3}};

void read() {
    for(int i=1; i<=4; i++) {
        for(int j=1; j<=4; j++) {
            field[i]<<=1;
            if(getchar()=='b')
                field[i]|=1;
        }
        getchar();
    }
}

void flip(int i, int j) {--j;
    field[i-1]^=state[0][j];
    field[i]  ^=state[1][j];
    field[i+1]^=state[0][j];
}

bool check() {
    return (field[1]==0||field[1]==15)
         && field[1]==field[2]
         && field[2]==field[3]
         && field[3]==field[4];
}

bool find(int n, int i, int j) {
    if(n==0) return check();
    j+=1; if(j>4) i+=1, j=1;
    if(i>4) return false;
    for(; i<=4; i++) {
        for(; j<=4; j++) {
            flip(i, j);
            if(find(n-1,i,j))
                return true;
            flip(i, j);
        }
        j=1;
    }
    return false;
}

void work() {
    for(int i=0; i<=16; i++)
        if(find(i,1,0)) {
            printf("%d\n", i);
            return;
        }
    puts("Impossible");
}

int main() {
    read();
    work();
    return 0;
}

POJ 1753 方法一
```

### 打表,4X4棋盘压缩成一个数字
```cpp
void init() {
    for(int i=1; i<=16; i++) {
        int v=0, k=1<<(i-1); v|=k;
        if((i+1)%4!=1) v|=k<<1;
        if((i-1)%4!=0) v|=k>>1;
        if(i>4)  v|=k>>4;
        if(i<13) v|=k<<4;
        printf("%d,",v);
    }
}

很丑的打表
```


```cpp
#include <stdio.h>

int field;
int state[]={19,39,78,140,305,626,1252,2248,4880,10016,20032,35968,12544,29184,58368,51200};

void read() {
    for(int i=0; i<4; i++) {
        for(int j=0; j<4; j++) {
            field<<=1;
            if(getchar()=='b')
                field|=1;
        }
        getchar();
    }
}

void flip(int i) {
    field^=state[i];
}

bool check() {
    return field==0x0000||field==0xFFFF;
}

bool find(int n, int i) {
    if(n==0) return check();
    //if(i>=16) return false;
    for(; i<16; i++) {
        flip(i);
        if(find(n-1,i+1))
            return true;
        flip(i);
    }
    return false;
}

void work() {
    for(int c=0; c<=16; c++)
        if(find(c,0)) {
            printf("%d\n", c);
            return;
        }
    puts("Impossible");
}

int main() {
    read();
    work();
    return 0;
}

POJ 1753 方法二
```
