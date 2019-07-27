* 在跑动的过程中，若发现“恐怖分子”，特警队员可以选择用枪击毙他，来得到写在“恐怖分子”胸前的得分，但是前提是他使用的子弹类型必须和“恐怖分子”类型相同，否则，即使击毙了“恐怖分子”，也得不到分数；当然选择不击毙他也是可以的，这样他不会从那个“恐怖分子”身上得到分数。
* 允许特警队员放空枪，这样可以消耗掉型号不对的子弹而不至于杀死“恐怖分子”（当然每个特警队员都不会愚蠢到不装消音装置就放空枪，以至于吓跑“恐怖分子”），等待枪口出现正确型号的子弹击毙他得分。

### 输入：
* 第一行，N，子弹和恐怖分子的类型数,
* 第二行，各种恐怖分子类型的一行字母
* 第三行，与上一行对应位置恐怖分子类型的得分数，每个分数之间恰好有一个空格
* 第四行，开始时枪膛子弹序列（左边的先打出）
* 第五行，恐怖分子出现的序列（左边的先出现）
### 输出：
* 对于每一个测试数据，输出最多得到的分数

### 最长上升子序列

```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
#include <map>
#include <algorithm>
#pragma warning(disable:4996)

using namespace std;
const int maxn = 2005;

char ter_leixing[maxn],zidan[maxn], terrerist[maxn];
int N;
int dp[maxn][maxn];
map<char, int> mp;

int main()
{
	while (scanf("%d",&N)==1) {
		mp.clear();
		scanf("%s", ter_leixing);
		for (int i = 0; i < N; i++) {
			scanf("%d", &mp[ter_leixing[i]]);
		}
		scanf("%s", zidan);
		scanf("%s", terrerist);
		/*
		int sum = 0;
		for (int i = 0; i < N; i++) {
			if (zidan[i] == terrerist[i]) {
				sum += scr[i];
			}
		}
		printf("%d\n",sum);
		*/
		int a_len = strlen(zidan);
		int b_len = strlen(terrerist);
		memset(dp, 0, sizeof(dp));
		for (int i = 0; i < a_len; i++) {
			for (int j = 0; j < b_len; j++) {
				if (zidan[i] == terrerist[j])
					dp[i + 1][j + 1] = dp[i][j] + mp[zidan[i]];
				else
					dp[i + 1][j + 1] = max(dp[i][j + 1], dp[i + 1][j]);
			}
		}
		cout << dp[a_len][b_len] << endl;
	}
	return 0;
}
```





