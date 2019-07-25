第i个Fibonacci数f(i)可以以如下形式递归定义：
* $f(0)=0，f(1)=1$
* $f(i+2)=f(i+1)+f(i)$对于每一个$i\geq 0$

你的任务是计算这个序列的一些值。

### 输入
t，测试用例数。<br>
a，b，n（$0\leq a$,$b\leq2^{64}$, $a,b$不全为0,  $1\leq n \leq1000$）

### 输出
输出$f(a^{b})$除以n的余数。

### 模板：
* 求$a^{b}$

```cpp
#include <iostream>
#include <cstdio>
#include <cstring>

using namespace std;


const int maxn=1000+5;
typedef unsigned long long ULL;

int f[maxn][maxn*5],period[maxn];


///求a^b
int pow_mod(ULL a,ULL b,int n){
    if(!b)  return 1;
    int k=pow_mod(a,b/2,n);
    k=k*k%n;
    if(b%2) k=k*a%n;
    return k;
}

int solve(ULL a,ULL b,int n){
    if(a==0||n==1)  return 0;
    int p=pow_mod(a%period[n],b,period[n]);
    return f[n][p];
}

int main(){
    for(int n=2;n<=1000;n++){
        f[n][0]=0;f[n][1]=1;
        for(int i=2;;i++){
            f[n][i]=(f[n][i-1]+f[n][i-2])%n;
            if(f[n][i-1]==0&&f[n][i]==1){///找周期
                period[n]=i-1;
                break;
            }
        }
    }

    ULL a,b;
    int n,T;
    scanf("%d",&T);
    while(T--){
        cin>>a>>b>>n;
        cout<<solve(a,b,n)<<endl;
    }
    return 0;
}


```
