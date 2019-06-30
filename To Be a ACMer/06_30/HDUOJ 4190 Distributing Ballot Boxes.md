[题目链接](http://acm.hdu.edu.cn/showproblem.php?pid=4190)

### 和5G那道题一样
```cpp
#include <iostream>
#include<stdio.h>
#include<string.h>
#include<math.h>
#define MAXN 500003
using namespace std;
 
int arr[MAXN];
int n,m;
 
//判断mid这个数是否符合要求，如果返回值为false表示投票箱不够
bool getMaxValue(int mid)
{
    int i;
    int sum=0;
    for(i=0;i<n;i++)
    {
        if(arr[i]<=mid)
            sum+=1;
        else if(arr[i]>mid)
        {
            sum+=ceil(arr[i]*1.0/mid);//上取整
        }
    }
    if(sum<=m)
        return true;
    else//投票箱有剩余
        return false;
 
}
 
 
 
int binarySearch(int l,int r)
{
	int mid;
	while(l<r)
	{
		mid=(l+r)/2;
		if(getMaxValue(mid))
			r=mid;
		else
			l=mid+1;
	}
	return r;
}
 
 
 
int main()
{
    int max;
    while(true)
    {
        scanf("%d%d",&n,&m);
        if(n==-1 && m==-1)
            break;
        memset(arr,-1,sizeof(arr));
        max=-1;
        for(int i=0;i<n;i++)
        {
            scanf("%d",&arr[i]);
            if(arr[i]>max)
                max=arr[i];
        }
        if(n==m)
            printf("%d\n",max);
        else if(n<m)
        {
            int val=binarySearch(1,max);
            printf("%d\n",val);
        }
    }
 
    return 0;
}
```

[博客地址](https://blog.csdn.net/CSDN515/article/details/7794129)







