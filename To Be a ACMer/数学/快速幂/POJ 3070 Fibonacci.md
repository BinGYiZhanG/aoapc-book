[题目链接](http://poj.org/problem?id=3070)

题意：计算大数的斐波那契数列

#### 相当于模板题
构造出满足符合状态转移的基础矩阵
Github貌似不能贴数学公式，我只能用图片形式了,
![](https://github.com/BinGYiZhanG/aoapc-book/blob/master/To%20Be%20a%20ACMer/Images/06271127png.png)
贴不出照片,
```cpp
#include<cstdio>  
#include<cstring>  
#include<cstdlib>  
#include<cmath>  
#include<iostream>  
#include<algorithm>  
#include<vector>  
#include<map>  
#include<set>  
#include<queue>  
#include<string>  
#include<bitset>  
#include<utility>  
#include<functional>  
#include<iomanip>  
#include<sstream>  
#include<ctime>  
using namespace std;
 
#define MAXN 2
#define mod int(1e4)  
struct Matrix
{
	int mat[MAXN][MAXN];
	Matrix() {}
	Matrix operator*(Matrix const &b)const
	{
		Matrix res;
		memset(res.mat, 0, sizeof(res.mat));
		for (int i = 0 ;i < MAXN; i++)
			for (int j = 0; j < MAXN; j++)
				for (int k = 0; k < MAXN; k++)
					res.mat[i][j] = (res.mat[i][j]+this->mat[i][k] * b.mat[k][j])%mod;
		return res;
	}
};
Matrix pow_mod(Matrix base, int n)
{
	Matrix res;
	memset(res.mat, 0, sizeof(res.mat));
	for (int i = 0; i < MAXN; i++)
		res.mat[i][i] = 1;
	while (n > 0)
	{
		if (n & 1) res = res*base;
		base = base*base;
		n >>= 1;
	}
	return res;
}
int main()
{
#ifdef CDZSC  
	freopen("i.txt", "r", stdin);
	//freopen("o.txt","w",stdout);  
	int _time_jc = clock();
#endif  
	Matrix base;
	for (int i = 0; i < MAXN; i++)
		for (int j = 0; j < MAXN; j++)
			base.mat[i][j] = 1;
	base.mat[1][1] = 0;
	int n;
	while (~scanf("%d", &n)&&n!=-1)
	{
		Matrix ans = pow_mod(base, n);
		printf("%d\n", ans.mat[1][0]);
	}
	return 0;
}
```
**参考：**<br>
[POJ 3070(矩阵快速幂）](https://blog.csdn.net/qq_24489717/article/details/51120679)<br>
[[POJ3070]Fibonacci sequence——矩阵+快速幂](https://blog.csdn.net/ccf15068475758/article/details/52846726)
