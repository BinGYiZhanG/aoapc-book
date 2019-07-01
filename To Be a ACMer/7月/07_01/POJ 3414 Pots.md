[题目链接](http://poj.org/problem?id=3414)

### 倒水问题
当做模板题来看吧

[博客链接1](https://www.cnblogs.com/xuesu/p/3992538.html)
![](https://github.com/BinGYiZhanG/aoapc-book/blob/master/To%20Be%20a%20ACMer/Images/07011850.png)


```cpp
#include <cstdio>
#include <cstring>
#include <queue>
using namespace std;
const int maxn=101;
int n,m;
typedef unsigned long long ull;
int A,B,C;
int vis[maxn][maxn];
int ans[maxn][maxn][maxn*maxn];
struct node{
    int a,b;
    node (int  ta,int tb):a(ta),b(tb){}
};
void printop(int op){
    switch(op){
    case 0:
        puts("FILL(1)");
        break;
    case 1:
        puts("FILL(2)");
        break;
    case 2:
        puts("POUR(1,2)");
        break;
    case 3:
        puts("POUR(2,1)");
        break;
    case 4:
        puts("DROP(1)");
        break;
    case 5:
        puts("DROP(2)");
        break;
    }
}
void op(int &a,int &b,int op){
    switch(op){
    case 0:
        a=A;
        break;
    case 1:
        b=B;
        break;
    case 2:
        if(b+a<=B){
            b+=a;
            a=0;
        }
        else {
            a-=B-b;
            b=B;
        }
        break;
    case 3:
        if(b+a<=A){
            a+=b;
            b=0;
        }
        else {
            b-=A-a;
            a=A;
        }
        break;
    case 4:
        a=0;
        break;
    case 5:
        b=0;
        break;
    }
}
void bfs(){
    queue <node> que;
    que.push(node(0,0));
    vis[0][0]=0;
    while(!que.empty()){
        node tp=que.front();que.pop();
        int ta=tp.a;
        int tb=tp.b;
        if(tp.a==C||tp.b==C){
            printf("%d\n",vis[tp.a][tp.b]);
            for(int i=0;i<vis[ta][tb];i++){
                int op=ans[ta][tb][i];
                printop(op);
            }
            return ;
        }
        for(int i=0;i<6;i++){
            int ta=tp.a;
            int tb=tp.b;
            op(ta,tb,i);
            if(vis[ta][tb]==-1){
                vis[ta][tb]=vis[tp.a][tp.b]+1;
                for(int j=0;j<vis[tp.a][tp.b];j++){///ans数组是用来记录操作的
                    ans[ta][tb][j]=ans[tp.a][tp.b][j];
                }
                ans[ta][tb][vis[tp.a][tp.b]]=i;
                que.push(node(ta,tb));
            }
        }
    }
    puts("impossible");
}
int main(){
    scanf("%d%d%d",&A,&B,&C);
        memset(vis,-1,sizeof(vis));
        bfs();
    return 0;
}


```










