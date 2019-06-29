[题目链接](http://poj.org/problem?id=2488)

### 我的WA代码：
```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
using namespace std;

int mov[8][2]={{-2,-1},{-1,-2},{1,-2},{2,-1},{2,1},{1,2},{-1,2},{-2,1}};
bool vis[27][27];
char mp[27*27][2];
int cnt;
int p,q;
bool flag;
bool islegal(int x,int y){
    if(x<0||x>p||y<0||y>q||vis[x][y]==true)
        return false;
    return true;
}
//int ceng;
void DFS(int x,int y,int step){
    //mp[cnt++]='A'+x;
    //mp[cnt++]='1'+y;
  //  printf("层数:%d\n",ceng++);
    //mp[cnt]='A'+x;
    //mp[cnt+1]='1'+y;
    mp[step][0]='A'+x;
    mp[step][1]='1'+y;
    if(step==p*q){
        flag=true;
        return ;
    }
    for(int i=0;i<8;i++){
        int tmpx=x+mov[i][0];
        int tmpy=y+mov[i][1];
        if(!islegal(tmpx,tmpy))     continue;
       // mp[cnt++]='A'+p;
       // mp[cnt++]='1'+q;
        vis[tmpx][tmpy]=true;
        DFS(tmpx,tmpy,step+1);
        vis[tmpx][tmpy]=false;
        //cnt--;
        //cnt--;
    }
    //return true;
}

int main(){
    int T,cas=0;
    scanf("%d",&T);
    while(T--){
        scanf("%d%d",&p,&q);
       // cnt=0;
      //  ceng=0;
        flag=false;
        fill(vis[0],vis[0]+27*27,false);
        vis[0][0]=true;
        DFS(0,0,0);
        printf("Scenario #%d:\n",++cas);
        printf("%d\n",cnt);
        if(flag)
        {
            for(int i=0;i<p*q;i++)
                printf("%c%c",mp[i][0],mp[i][1]);
        }
        else
            printf("impossible");
        printf("\n");
        if(T != 0)
            printf("\n");
    }
    return 0;
}


```

### AC代码:(很好理解)
```cpp

#include<cstdio>
#include<cstring>
#include<algorithm>
using namespace std;
 
int path[88][88], vis[88][88], p, q, cnt;
bool flag;
 
int dx[8] = {-1, 1, -2, 2, -2, 2, -1, 1};
int dy[8] = {-2, -2, -1, -1, 1, 1, 2, 2};
 
bool judge(int x, int y)
{
    if(x >= 1 && x <= p && y >= 1 && y <= q && !vis[x][y] && !flag)
        return true;
    return false;
}
 
void DFS(int r, int c, int step)
{
    path[step][0] = r;
    path[step][1] = c;
    if(step == p * q)
    {
        flag = true;
        return ;
    }
    for(int i = 0; i < 8; i++)
    {
        int nx = r + dx[i];
        int ny = c + dy[i];
        if(judge(nx,ny))
        {
 
            vis[nx][ny] = 1;
            DFS(nx,ny,step+1);
            vis[nx][ny] = 0;
        }
    }
}
 
int main()
{
    int i, j, n, cas = 0;
    scanf("%d",&n);
    while(n--)
    {
        flag = 0;
        scanf("%d%d",&p,&q);
        memset(vis,0,sizeof(vis));
        vis[1][1] = 1;
        DFS(1,1,1);
        printf("Scenario #%d:\n",++cas);
        if(flag)
        {
            for(i = 1; i <= p * q; i++)
                printf("%c%d",path[i][1] - 1 + 'A',path[i][0]);
        }
        else
            printf("impossible");
        printf("\n");
        if(n != 0)
            printf("\n");
    }
    return 0;
}
```
