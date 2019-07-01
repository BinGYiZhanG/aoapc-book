[题目链接](http://poj.org/problem?id=2632)

### 未完待续
```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
#include <vector>
#include <map>
using namespace std;

struct robot{
    int x;///记录机器人位置
    int y;
    char asp;///记录朝向
}rob[110];
int A,B;///B：列数，A：行数
int N,M;///机器人个数，指令个数
bool vis[110][110];
int number[110][110];///坐标  --->  机器人编号

bool islegal(int x,int y){
    if(x<0||x>=A||y<0||y>=B)
        return false;
    return true;
}

struct node{
    int x,y;
};
//map<char,node> mp;
int mov[4][2]={{0,-1},{0,1},{-1,0},{1,0}};
int asppos[4];

char aspects[4]={'N','W','S','E'};///从 N 开始，逆时针

void CMD(){
    bool flag=true;///是否需要继续执行指令，默认 需要继续执行指令
    for(int i=0;i<M;i++){///执行指令
        int num;///机器人编号
        char action;///动作
        scanf("%d %c",&num,&action);
        if(action=='F'){///说明是前进
            int movter;///前进步数
            scanf("%d",&movter);
            for(int i=1;i<=movter;i++){///机器人num号开始移动了
                node tmp;
                tmp.x=rob[num].x+mov[asppos[rob[num].asp]][0];
                tmp.y=rob[num].y+mov[asppos[rob[num].asp]][1];
                if(!islegal(tmp.x,tmp.y)){
                    printf("Robot %d crashes into the wall\n",num);
                    flag=false;
                    break;
                }
                if(vis[tmp.x][tmp.y]==true){///说明两个机器人撞上了
                    int beizhuang;
                    beizhuang=number[tmp.x][tmp.y];
                    printf("Robot %d crashes into robot %d\n",num,beizhuang);
                    flag=false;
                    break;
                }
            }
        }
        if(action=='L'){
            int repeat;///记录转向次数
            scanf("%d",&repeat);
            for(int i=0;i<repeat;i++){
                if(rob[i].asp=='N')
                    rob[i].asp='W';
                if(rob[i].asp=='W')
                    rob[i].asp='S';
                if(rob[i].asp=='S')
                    rob[i].asp='E';
                if(rob[i].asp=='E')
                    rob[i].asp='N';
            }
        }
        if(action=='R'){
            int repeat;
            scanf("%d",&repeat);
            for(int i=0;i<repeat;i++){
                if(rob[i].asp=='N')
                    rob[i].asp='E';
                if(rob[i].asp=='E')
                    rob[i].asp='S';
                if(rob[i].asp=='S')
                    rob[i].asp='W';
                if(rob[i].asp=='W')
                    rob[i].asp='N';
            }
        }

        if(!flag)
            break;
    }
    if(flag)
        printf("OK\n");
}

int main(){
    int K;
    scanf("%d",&K);
    while(K--){
            /*
        mp['E'].x=0,mp['E'].y=1;
        mp['W'].x=0,mp['W'].y=-1;
        mp['N'].x=-1,mp['N'].y=0;
        mp['S'].x=1,mp['S'].y=0;
        */
        asppos['W']=0,asppos['E']=1,asppos['N']=2,asppos['S']=3;
        scanf("%d%d",&B,&A);
        scanf("%d%d",&N,&M);
        for(int i=1;i<=N;i++){
            scanf("%d %d %c",&rob[i].x,&rob[i].y,&rob[i].asp);
            vis[rob[i].x][rob[i].y]=true;///表示机器人在这个位置上
            number[rob[i].x][rob[i].y]=i;///映射机器人编号
        }
        CMD();
    }
}

```
