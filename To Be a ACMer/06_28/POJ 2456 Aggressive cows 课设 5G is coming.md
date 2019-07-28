[POJ 2456 Aggressive cows](http://poj.org/problem?id=2456)
#### 题面:
This year is the first year of 5G. All major operators are stepping up construction of 5G.
Now there is a problem of site selection for base stations.In order to simplify the problem, only one-dimensional situation is considered.
There are nnn locations of the base stations to be selected that are distributed in a straight line, and mmm base stations are to be constructed.
Considering that the coverage of each base station is as large as possible and the signal distribution is even.
Therefore, it is necessary to place each base station as far as possible from other base stations, that is, to maximizemaximizemaximize the distance between the two nearest base stations.
#### 输入
Multiple sets of inputs
Number of groups of first behavior data T(1≤T≤3)T(1\leq T\leq 3)T(1≤T≤3)
In each set of data
The first line is the number of positions to be selected n(2≤n≤100000)n(2\leq n \leq 100000)n(2≤n≤100000)
The second line is the number of 5G base stations should to be built m(m≤n)m(m\leq n)m(m≤n)
The third line has n positive integer numbers, which are the coordinates of the candidate position. Guaranteed data not more than231−1 2^{31}-1231−1
#### 输出
The distance between the two nearest base stations is output.
* 如果基站数多了，应该少建基站，拉大距离，就是```lf=mid+1```
* 如果基站数少了，应该多建基站，减小距离，就是```rt=mid-1```

```cpp
#include <iostream>
#include <cstring>
#include <cstdio>
#include <algorithm>

using namespace std;

typedef long long ll;
const int maxn=100010;
ll pos[maxn];
int n,m;

bool check(ll dis){
    int cnt=1;
    ll distance=pos[0]+dis;
    for(int i=1;i<n;i++){
        if(pos[i]<=distance)    continue;///小于等于
        cnt++;
        distance=pos[i]+dis;///新建基站
    }
    return cnt>=m;///新建基站数，是否满足题意
}

int main(){
    int T;
    scanf("%d",&T);
    while(T--){
        scanf("%d%d",&n,&m);
        for(int i=0;i<n;i++){
            cin>>pos[i];
        }
        sort(pos,pos+n);
        ll Left=0,Right=pos[n-1]-pos[0],mid;
        while(Left<Right){
            mid=Left+(Right-Left)/2;
            if(check(mid))
                Left=mid+1;
            else
                Right=mid-1;
        }
        cout<<Left<<endl;
    }
    return 0;
}
```










