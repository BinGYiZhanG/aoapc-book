[题目链接](http://poj.org/problem?id=2785)
## 本题是关于lower_bound与upper_bound的用法:
### lower_bound(begin,end,index):
#### 在数组中的[begin，end)前闭后开区间内，返回大于或等于index的第一个元素位置，如果都小于index，则返回end。
### upper_bound(begin,end,index)：
#### 在数组中的[begin，end)前闭后开区间内，返回大于index的第一个元素位置，如果都小于index，则返回end。

```cpp
#include <iostream>
#include <cstdio>
#include <algorithm>

using namespace std;

const int maxn=4010;
int A[maxn],B[maxn],C[maxn],D[maxn];
int sum1[maxn*maxn];

int main(){
    int n;
    scanf("%d",&n);
    for(int i=0;i<n;i++){
        scanf("%d%d%d%d",&A[i],&B[i],&C[i],&D[i]);
    }
    int m=0;
    for(int i=0;i<n;i++){
        for(int j=0;j<n;j++){
            sum1[m++]=A[i]+B[j];
        }
    }
    long long ans=0;
    sort(sum1,sum1+m);
    for(int i=0;i<n;i++){
        for(int j=0;j<n;j++){
            int k=-(C[i]+D[j]);
            ans+=upper_bound(sum1,sum1+m,k)-lower_bound(sum1,sum1+m,k);
            ///如果等于0，则说明均大于，说明误解
            ///而如果非0，则说明upper_bound找的是第一个大于该元素的位置，而lower_bound找的第一个等于该元素的位置,
            ///由lower_bound可知，存在这个一个k，使得k+A[]+B[]=0
        }
    }
    cout<<ans<<endl;
}

```
