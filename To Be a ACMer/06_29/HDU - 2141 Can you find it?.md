[题目链接](http://acm.hdu.edu.cn/showproblem.php?pid=2141)

### 此题要求的Memory limit 为10000 kB ，Time limit为3000 ms 显然不能用三个for，同样分为2个组
### 此题为binary_search()用法

```cpp
#include <iostream>
#include <cstdio>
#include <algorithm>

using namespace std;

typedef long long ll;

const int maxn=510;
ll a[maxn],b[maxn],c[maxn],sum1[maxn*maxn];///sum1数组记得设的大一点

int main(){
    int L,N,M;
    int kase=1;
    while(scanf("%d%d%d",&L,&N,&M)!=EOF){
        for(int i=0;i<L;i++){
            cin>>a[i];
        }
        for(int i=0;i<N;i++){
            cin>>b[i];
        }
        for(int i=0;i<M;i++){
            cin>>c[i];
        }
        int m=0;
        for(int i=0;i<L;i++){
            for(int j=0;j<N;j++){
                sum1[m++]=a[i]+b[j];
            }
        }
        sort(sum1,sum1+m);
        int S;
        printf("Case %d:\n",kase++);
        scanf("%d",&S);
        while(S--){
            ll tmp;
            cin>>tmp;
            bool flag=false;
            for(int i=0;i<M;i++){
                ll res=tmp-c[i];
                if(binary_search(sum1,sum1+m,res)){
                    flag=true;
                    break;
                }
            }
            if(flag)
                printf("YES\n");
            else
                printf("NO\n");
        }
    }
    return 0;
}



```












