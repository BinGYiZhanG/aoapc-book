左图展示左右对称，因为根据一条竖直线（画出的虚线）来折叠是可能的，，并且切割成两个相等的部分。右图没有一条所谓的竖直线可以把图分成左右对称的部分。<br>
<br>
写一个程序判断图是否可以分成左右对称的两部分。点都是独一无二的。<br>
### 输入：
T个测试用例。<br>
第一行,T；<br>
第一行，N，点的总数；<br>
x,y范围都在[-10000,10000]内<br>


### WA代码
* //只判断x坐标
*	//存在小数判断
*	//排序有问题，
*	//如果100个数据，只有两种x坐标，排序是左边从下到上，0...N/2,右边从下到上N/2+1..N-1
*	//比较也会出现问题，不是对称比较
*	//如果每个数据的x不同，则对称比较
```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
#include <cmath>
#include <algorithm>
#include <fstream>
#include <string>
#pragma warning(disable:4996)

using namespace std;

int N;

struct Node {
	int x, y;
}node[1010];

bool cmp(Node a, Node b) {
	if(a.x!=b.x)
		return a.x < b.x;
	return a.y < b.y;
}

//

int main() {
	int T;
	scanf("%d", &T);
	string file = "OOOO1111" ;
	file += ".txt";
	ofstream out(file);
	while (T--) {
		scanf("%d",&N);
		//if (!out)	return 0;
		for (int i = 0; i < N; i++) {
			scanf("%d%d", &node[i].x, &node[i].y);
		}
		sort(node, node + N, cmp);
		bool flag = true;//默认是对称图
		if (N % 2 == 0) {//如果点数是偶数
			//只判断x坐标
			//存在小数判断
			//排序有问题，
			//如果100个数据，只有两种x坐标，排序是左边从下到上，0...N/2,右边从下到上N/2+1..N-1
			//比较也会出现问题，不是对称比较
			//如果每个数据的x不同，则对称比较
			double mid = (node[0].x + node[N - 1].x)*1.0 / 2;//N=4,N/2=2,0与3
			for (int i = 1; i < N / 2; i++) {//1与2,
				double tmpmid = (node[i].x + node[N - 1 - i].x)*1.0 / 2;
				//printf("tmpmid:%lf,mid:%lf\n", tmpmid, mid);
				if (tmpmid != mid) {
					flag = false;
					break;
				}
			}
			if (flag == false) {
				printf("NO\n");
				out << "NO" << endl;
		
				continue;
			}
			//还有一种情况：
			//所有点都在一条直线上，所以对称
			if (node[0].x == node[N - 1].x) {//说明点都在一条直线上
				printf("YES\n");
				out << "YES" << endl;
			
				continue;
			}
			//判断y坐标
			//前N/2个点和后N/2个点对称比较,N=4,N/2=2,
			for (int i = 0; i < N / 2; i++) {//0与3,1与2,
				//if (node[i].y != node[N - i - 1].y) {
				//printf("node[%d].y:%d,node[%d].y:%d\n", i, node[i].y, N/2 + i, node[N/2 + i].y);
				if (node[i].y != node[N/2+i].y) {
					flag = false;
					break;
				}
			}
			if (flag == false) {
				printf("NO\n");
				out << "NO" << endl;
			
				continue;
			}

		}
		else {//点数是奇数
			//只判断x坐标
			double mid = node[N / 2].x*1.0;//N=5，N/2=2
			for (int i = 0; i < N/2; i++) {//0与4,1与3，
				double tmpmid = (node[i].x + node[N - i - 1].x)*1.0 / 2;
				if (tmpmid != mid) {
					flag = false;
					break;
				}
			}
			if (node[0].x == node[N - 1].x) {//说明点都在一条直线上
				printf("YES\n");
				out << "YES" << endl;
		
				continue;
			}
			//判断y坐标N=5,N/2=2,
			for (int i = 0; i < N / 2; i++) {//0与3,1与2，
				//if (node[i].y != node[N - i - 1].y) {
				printf("node[%d].y:%d,node[%d].y:%d\n", i, node[i].y, N/2+i+1,node[N/2+i+1].y);
				if (node[i].y != node[N / 2 + i+1].y) {
					flag = false;
					break;
				}
			}

			if (flag == false) {
				printf("NO\n");
				out << "NO" << endl;
			
				continue;
			}
		}
		printf("YES\n");
		out << "YES" << endl;
	}
	out.close();
	return 0;
}
```
