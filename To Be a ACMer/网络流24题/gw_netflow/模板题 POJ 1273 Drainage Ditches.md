
### 这道题存在重边的情况，自己找的代码还不能完成对重边情况的处理
### 将MAX范围改为10010,也是不行的
```cpp

#include <iostream>
#include <cstdio>
#include <cstdlib>
#include <cstring>
#include <vector>
#include <queue>
#include <algorithm>
#include <climits>
using namespace std;

struct edge {
//	char source[4], dest[4];
	int capacity, s, d;
//	int dindex(void) {
//		int index = 0;
//		index = ((dest[0] - 'A') * 26 + dest[1] - 'A') * 26 + dest[2] - 'A';
//		return index;
//	}
//	int sindex(void) {
//		int index = 0;
//		index = ((source[0] - 'A') * 26 + source[1] - 'A') * 26 + source[2] - 'A';
//		return index;
//	}
//	void read(void) {
//		scanf("%s %s %d", source, dest, capacity);
//		return;
//	}
};

const int MAX = 26 * 26 * 26;

bool BFS(vector<edge> arr[], int route[], int source, int dest);
int Edmonds_Karp(vector<edge> arr[], int source, int dest);

int main(void) {

    int n,m;
    scanf("%d%d",&n,&m);
	edge tmp;
	vector<edge> *arr;

	arr = new vector<edge>[MAX];
	for (int i = 0; i < n; i++) {
		scanf("%d %d %d", &tmp.s, &tmp.d, &tmp.capacity);
		bool flag=true;
		for(int j=0;j<(int)arr[tmp.s].size();j++){///考虑重边的情况
            if(arr[tmp.s][j].d==tmp.d){
                arr[tmp.s][j].capacity+=tmp.capacity;
                flag=false;
            }
		}
		if(flag)
            arr[tmp.s].push_back(tmp);
	}

	printf("%d", Edmonds_Karp(arr, 1, m));
	delete[] arr;
	return 0;
}

bool BFS(vector<edge> arr[], int route[], int source, int dest) {
	bool *visit = (bool *)calloc(MAX, sizeof(bool));
	int i, j;
	queue<int> q;
	q.push(source);
	visit[source] = true;
	while (!q.empty()) {
		i = q.front();
		q.pop();
		if (i == dest) {
			break;
		}
		for(int k=0;k<(int)arr[i].size();k++){
			j = arr[i][k].d;
			if (!visit[j] && arr[i][k].capacity > 0) {
				q.push(j);
				route[j] = i;
				visit[j] = true;
			}
		}
	}
	free(visit);
	return i == dest ? true : false;
}

int Edmonds_Karp(vector<edge> arr[], int source, int dest) {
	int *route, i, j, max_, f;
	vector<edge>::iterator vit;
	route = new int[MAX];
	max_ = 0;
	for (i = 0; i < MAX; i++) {
		route[i] = -1;
	}
	while (BFS(arr, route, source, dest)) {
		f = INT_MAX;
		for (i = dest; i != source;) {
			j = route[i];
			for (vit = arr[j].begin(); vit != arr[j].end(); vit++) {
				if (vit->d == i) {
					f = min(f, vit->capacity);
					break;
				}
			}
			i = j;
		}
		for (i = dest; i != source;) {
			j = route[i];
			for (vit = arr[j].begin(); vit != arr[j].end(); vit++) {
				if (vit->d == i) {
					vit->capacity -= f;
					break;
				}
			}
			i = j;
		}
		max_ += f;
		for (i = 0; i < MAX; i++) {
			route[i] = -1;
		}
	}
	delete[] route;
	return max_;
}
```
