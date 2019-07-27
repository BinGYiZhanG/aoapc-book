[题目链接](http://acm.hdu.edu.cn/showproblem.php?pid=1241)

题意：给出一个矩阵，找出连通块的数量（对角线连也算）。

### DFS

**坑：** 
### 1，主函数要机上vis判断连通块是否已访问<br>
### 2，字符数组的读取      
```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
#include <algorithm>
using namespace std;
const int maxn=110;
char mp[maxn][maxn];
bool vis[maxn][maxn];
int m,n;
int cnt;
int mov[8][2]={{-1,-1},{0,-1},{1,-1},{1,0},{1,1},{0,1},{-1,1},{-1,0}};///逆时针

bool islegal(int x,int y){
    if(x<0||x>=n||y<0||y>=m||mp[x][y]=='*'||vis[x][y]==true)
        return false;
    return true;
}

void DFS(int x,int y){
    vis[x][y]=true;

    for(int i=0;i<8;i++){
        int tmpx=x+mov[i][0];
        int tmpy=y+mov[i][1];
        if(!islegal(tmpx,tmpy)) continue;
        DFS(tmpx,tmpy);
    }
    return ;
}


int main(){
    while(scanf("%d%d",&m,&n)==2&&m!=0){
        getchar();
        swap(m,n);
        for(int i=0;i<n;i++){
            for(int j=0;j<m;j++){
                cin>>mp[i][j];///不能用scanf("%c",&mp[i][j])读
            }
            getchar();
        }
        cnt=0;
        fill(vis[0],vis[0]+maxn*maxn,false);
        for(int i=0;i<n;i++){
            for(int j=0;j<m;j++){
                if(mp[i][j]=='@'&&vis[i][j]!=true){///要加上vis[][]判断是否访问
                    DFS(i,j);
                    cnt++;
                }
            }
        }
        printf("%d\n",cnt);
    }
}
```
