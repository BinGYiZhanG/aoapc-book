
### 输入：
第一行，n，n个亲属关系；m，m个问题。<br>
接下来n行，每行一个字符串,表明关系
* 如:```ABC```表示```A```的父母分别是```B```和```C```。<br>

接下来m行，询问 字符串关系
* 如```FA``` 的关系。<br>



### WA代码
```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
#include <map>
#include <algorithm>
#pragma warning(disable:4996)

using namespace std;
int N, M;
struct Node {
	int father, mother;
}node[30];
bool vis[110];//设置访问
char relation[4];
int a, b;

//得分两个方向向上找:
//a --> b和b --> a
int cnt;

void DFS(int st,int step,int ed) {
	if (cnt != -1)//找到了
		return;
	if (st == ed) {
		cnt = step;
		return;
	}
	if (node[st].father != -1 && vis[node[st].father] == false) {
		vis[node[st].father] = true;
		DFS(node[st].father, step + 1, ed);
		vis[node[st].father] = false;
	}

	if (node[st].mother != -1 && vis[node[st].mother] == false) {
		vis[node[st].mother] = true;
		DFS(node[st].mother, step + 1, ed);
		vis[node[st].mother] = false;
	}
	return ;

}


int main() {
	while (scanf("%d%d", &N, &M) == 2) {
		if (N == 0 && M == 0)
			break;
		for (int i = 0; i < N; i++) {
			scanf("%s", relation);
			
			if (relation[1] != '-')//父亲
				node[relation[0] - 'A' + 1].father = relation[1] - 'A' + 1;
			else
				node[relation[0] - 'A' + 1].father = -1;

			if (relation[2] != '-')//母亲
				node[relation[0] - 'A' + 1].mother = relation[2] - 'A' + 1;
			else
				node[relation[0] - 'A' + 1].mother = -1;
			
		}

		char chaxun[3];
		for (int i = 0; i < M; i++) {
			scanf("%s", chaxun);
			a = chaxun[0] - 'A' + 1, b = chaxun[1] - 'A' + 1;
			if (a == b) {
				printf("-\n");
				continue;
			}
			cnt = -1;

			memset(vis, false, sizeof(vis));
			bool flag = false;
			vis[a] = true;
			DFS(a, 0, b);//a -- > b找

			if (cnt == -1) {//没找着, b -- > a找
				flag = true;
				memset(vis, false, sizeof(vis));
				vis[b] = true;
				DFS(b, 0, a);

			}

			if (cnt == -1)//两人没关系
				printf("-\n");
			else {
				if (flag) {//a是b的长辈
					if (cnt == 1)//格式输出 
						cout << "parent" << endl;
					else if (cnt == 2)
						cout << "grandparent" << endl;
					else if (cnt == 3)
						cout << "great-grandparent" << endl;
					else
					{
						for (int i = 0; i < cnt - 3; i++)
							cout << "great-";
						cout << "great-grandparent" << endl;
					}
				}
				else {
					if (cnt == 1)
						cout << "child" << endl;
					else if (cnt == 2)
						cout << "grandchild" << endl;
					else if (cnt == 3)
						cout << "great-grandchild" << endl;
					else
					{
						for (int i = 0; i < cnt - 3; i++)
							cout << "great-";
						cout << "great-grandchild" << endl;
					}
				}
			}
		}


	}
}


```
