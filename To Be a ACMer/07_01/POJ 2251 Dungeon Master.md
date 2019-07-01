
```cpp
#include<iostream>
#include<cstdio>
#include<cstring>
#include<cstdlib>
#include<algorithm>

using namespace std;

char mp[35][35][35];
int mov[3][4][2]={{-1,0,1},{-1,1,0},{-1,0,-1},{-1,-1,0},
                {0,0,1},{0,1,0},{0,0,-1},{0,-1,0},
                 {1,0,1},{1,1,0},{1,0,-1},{1,-1,0}
                };
bool vis[35][35][35];
int L,R,C;
int cnt;
struct node{
    int x,y,z;
}st,ed;

bool islegal(int x,int y,int z){
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
    while(scanf("%d%d%d",&L,&R,&L)==3){
        getchar();
        for(int i=0;i<L;i++){
            for(int j=0;j<n;j++){
                for(int k=0;k<m;k++){
                    scanf("%c",mp[i][j][k]);
                    if(mp[i][j][k]=='S'){
                        st.x=i;
                        st.y=j;
                        st.z=k;
                    }
                    if(mp[i][j][k]=='E'){
                        ed.x=i;
                        ed.y=j;
                        ed.z=k;
                    }
                }
                getchar();
            }
        }

        cnt=0;
        fill(vis[0],vis[0]+22*22,false);
        DFS(st);
        printf("%d\n",cnt);
    }
    return 0;
}
```
