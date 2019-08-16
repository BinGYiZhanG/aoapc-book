农场主约翰是一个惊人的会计奇才，他意识到经营农场的钱可能会用光。他已经计算并记录了在接下来的N天(1≤N≤100,000)他每天需要花费的确切金额(1≤moneyi≤10,000)。<br>
FJ希望为连续的M个财政周期(1≤M≤N)创建一个预算，称为“fajomonths”。每个fajomonths包含一组连续的1天或更长时间。每一天都包含在一个月之中。<br>
FJ的目标是安排fajomonth，使花费最高的fajomonth的花费最小化，从而确定他每月的花费限额。<br>

### 输入
* Line 1:N,M
* Lines2...N+1:Line i+1 包含农场主花费在第i天的金钱数

### 输出
Line 1:农场主约翰能够生存的最小可能每月限制


### 记录
* 虽然正解有问题，但是```f()```还是学到了，注释掉的是自己写的那部分，明显错误

```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
#include <algorithm>

using namespace std;

const int maxn=100010;
int a[maxn];
int n,m;

/*
bool f(int limit){
    int cnt=0,tol=0;
    for(int i=0;i<n;i++){
        if(tol<=limit)///代码明显错误,带入数据验证即可
            tol+=a[i];
        else
        {
            cnt++;
            tol+=a[i];
        }
    }
    return cnt<=m;
}
*/

bool f(int limit){
    int cnt=1,tol=0;
    for(int i=0;i<n;i++){
        if(tol+a[i]<=limit)
            tol+=a[i];
        else
        {
            cnt++;
            tol=a[i];
        }
    }
    return cnt<=m;
}


int main(){
    scanf("%d%d",&n,&m);
    int maxn_=0,low_=0x3f3f3f3f;
    for(int i=0;i<n;i++){
        scanf("%d",a+i);
        maxn_+=a[i];
        low_=min(low_,a[i]);
    }

    //int cnt=0;///记录有几个月，应该等于m
    int left=low_,right=maxn_,mid;
    int cnt=0;
    while(left<right){
        mid=(right+left)/2;
        if(f(mid)==false){
            left=mid+1;
        }
        else
            right=mid;
        cnt++;
    }
    printf("%d  %d\n",mid,cnt);
    return 0;
}

```






