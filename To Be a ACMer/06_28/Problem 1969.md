

### 注：
#### 1，Re:这道题我想喷了。WS无数次。原来是圆周率不够精确
3.14159265358979323846  AC
3.14159265358  WS  
无限鄙视

#### 2，输出必须是printf %.4 ，其他形式（包括cout！！）都是错的

#### 3，PI要写成acos(-1.0)(常识)

#### 4，find（）函数返回类型不是double让我WA无数次

本题，我没有思路，也不会做，只是检测一下二分查找

```cpp
#include<cstdio>
#include<cstring>
#include<cmath>
#define PI acos(-1.0)
double a[10000+11];
int n,f;
bool Check(double x)			//关键是这个子函数 
{
	int num=0;
	for(int i=0;i<n;i++)
	{
		num+=(int)(a[i]/x);				//计算可以切出的大小为x的馅饼的个数 
		if(num>=f)					//一旦满足num>=f说明x这个大小满足条件 ，就可以返回true 
			return true;
	}
	return false;
}
int main()
{
	int t;
	scanf("%d",&t);
	while(t--)
	{
		scanf("%d%d",&n,&f);
		f++;
		double lb=0,ub=0;
		for(int i=0;i<n;i++)
		{
			scanf("%lf",&a[i]);
			a[i]=PI*a[i]*a[i];
			if(a[i]>ub)
				ub=a[i];
		}
		while(ub-lb>1e-5)	//划精度范围 
		{
			double mid=(lb+ub)/2.0;
			if(Check(mid))	//因为要使切得的馅饼大小尽可能的大，所以当mid满足条件时，看比它大的有没有符合的 
				lb=mid;		//所以就要找mid的 右侧部分，右侧部分的右端点不变，左端点变成了mid; 
			else
				ub=mid;		//mid不满足条件，找较小的，在左侧。左端点不变，右端点变成mid; 
		}
		printf("%.4lf\n",lb);		//四位小数 
	}
	return 0;
}
```

[博客链接](https://blog.csdn.net/Greenary/article/details/77884293)
