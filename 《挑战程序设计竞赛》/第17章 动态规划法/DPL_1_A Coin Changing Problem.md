寻找兑换n美分的最少硬币数(m)<br>

### 输入
```
n m
d1 d2 ... dm
```
### 输出：
打印最少硬币数
限制：
* $1 \leq n \leq 50000$
* $1 \leq m \leq 20$
* $1 \leq denomination \leq 10000$
* denominations是不一样的并且包含1

### Sample Input 1
```
55 4
1 5 10 50
```
### Sample Output 1
```
2
```

### Sample Input 2
```
65 6
1 2 7 8 12 50
```

### Sample Output 2
```
3
```


### 一直编译错误```compile error```
```cpp
#include<iostream>
#include<algorithm>
using namespace std;

const int MMAX = 20;
const int NMAX = 50000;
const int INFTY = (1 << 29 );

int main() {
    int n,m;
    int C[21];
    int T[NMAX + 1];

    cin >> n >> m;

    for (int i=1;i<=m;i++) {
        cin>>C[i];
    }

    for ( int i = 0;i<NMAX;i++){
        T[i]=INFTY;
    }

    T[0] = 0;
    for (int i=1;i<=m;i++) {
        for (int j=0;j+C[i]<=n;j++){
            T[j+C[i]]=min(T[j+C[i]],T[j]+1);
        }
    }

    printf("%d\n",T[n]);
    return 0;
}

```
