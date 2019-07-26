```cpp
#include <iostream>
#include <cstdio>
#include <algorithm>
#pragma warning(disable: 4996)
using namespace std;

const int maxn = 1000010;
int L, n;
int x[maxn];

void solve() {
	//计算最短时间
	int minT = 0;
	for (int i = 0; i < n; i++) {
		minT = max(minT, min(x[i], L - x[i]));
	}

	//计算最长时间
	int maxT = 0;
	for (int i = 0; i < n; i++) {
		maxT = max(maxT, max(x[i],L-x[i]));
	}

	printf("%d %d\n", minT, maxT);
}



int main() {
	int T;
	scanf("%d",&T);
	while (T--) {
		scanf("%d%d", &L, &n);
		for (int i = 0; i < n; i++) {
			scanf("%d", x + i);
		}
		solve();
	}
	return 0;
}
```
