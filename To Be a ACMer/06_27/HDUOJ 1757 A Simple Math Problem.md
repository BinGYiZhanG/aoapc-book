[题目链接](http://acm.hdu.edu.cn/showproblem.php?pid=1757)<br>
思路:
![](https://github.com/BinGYiZhanG/aoapc-book/blob/master/To%20Be%20a%20ACMer/Images/06301615.png)
**注：** first矩阵是9,8,7....0，而非9,7,8....0，笔误!


### 本题需要当成模板题来掌握。
AC代码：
```cpp
#include <iostream>
#include <vector>
#include <cstdio>
#include <cstring>

using namespace std;

int k,M;
typedef long long ll;

///矩阵建立与快速幂乘法,需要熟练掌握
struct matrix{
    ll m[10][10];
    matrix(){
        memset(m,0,sizeof(m));
        for(int i=0;i<10;i++){
            m[i][i]=1;
        }
    }
};

matrix first;
matrix temp;
matrix mul(matrix a,matrix b){
    matrix ans;
    int i,j,k;
    for(i=0;i<10;i++){
        for(j=0;j<10;j++){
            ans.m[i][j]=0;
            for(k=0;k<10;k++){
                ans.m[i][j]+=a.m[i][k]*b.m[k][j]%M;
                ans.m[i][j]%=M;
            }
        }
    }
    return ans;
}

ll fast_mul(matrix a,matrix b,int c){
    matrix ans;

    while(c){
        if(c&1)
            ans=mul(b,ans);
        b=mul(b,b);
        c=c>>1;
    }
    ans=mul(ans,a);
    return ans.m[0][0];
}
///


void print(matrix a){
    int i,j;
    for(i=0;i<10;i++){
        for(j=0;j<10;j++){
            printf("%I64d ",a.m[i][j]);
        }
        printf("\n");
    }
    printf("\n");
    return ;
}

int main(){
    int i;
    for(int i=0;i<10;i++){
        first.m[i][0]=9-i;
        for(int j=1;j<10;j++){
            first.m[i][j]=0;
        }
    }

    while(~scanf("%d%d",&k,&M)){
        for(i=0;i<10;i++){
            scanf("%I64d",&temp.m[0][i]);///f(0)~f(9),矩阵第一行
            if(i)
                temp.m[i][i]=0;
            if(i<9)
                temp.m[i+1][i]=1;
        }

        if(k<10){
            printf("%d\n",k%M);
            continue;
        }

        ll ans=fast_mul(first,temp,k-9);
        printf("%I64d\n",ans%M);
    }
    return 0;
}

```

