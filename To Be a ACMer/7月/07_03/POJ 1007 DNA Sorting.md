
[题目链接](http://poj.org/problem?id=1007)

### 我的WA代码：用map做的，
```cpp
#include <iostream>
#include <cstdio>
#include <algorithm>
#include <string>
#include <map>

using namespace std;

map<int,string> mp;

int main()
{
    int n,m,cnt;
    scanf("%d%d",&n,&m);
    for(int i=0;i<m;i++){
        string str;
        cin>>str;
        cnt=0;
        for(int j=0;j<n-1;j++){
            for(int k=j+1;k<n;k++){
                if(str[j]>str[k])
                    cnt++;
            }
        }
        mp[cnt]=str;
    }

    map<int,string>::iterator it;
    for(it=mp.begin();it!=mp.end();it++){
        cout<<it->second<<endl;
    }

    return 0;
}
```

AC代码:
[结构体做法--冒泡排序 ](https://blog.csdn.net/a799581229/article/details/50759152)
```cpp
#include<stdio.h>
#include<string.h>
 
#define M 200
struct dna
{
	char str[M];
	int ans;
};
struct dna d[M];
struct dna t;
void main()
{
	int n,m,i,j,k;
	scanf("%d%d",&n,&m);
	for(i=0;i<m;i++)
	{
		scanf("%s",d[i].str);
		d[i].ans=0;
		for(j=0;j<n;j++)
		{
			for(k=j;k<n;k++)
			if(d[i].str[j]>d[i].str[k])
				d[i].ans++;
		}
	}
 
	for(i=0;i<m;i++)
		for(j=i;j<m;j++)
		{
			if(d[i].ans>d[j].ans)
			{
				t=d[i];
				d[i]=d[j];
				d[j]=t;
			}
		}
 
	for(i=0;i<m;i++)
	{
		printf("%s\n",d[i].str);
	}
	
		
}
```
[快排qsort](https://blog.csdn.net/lyy289065406/article/details/6647305)
```cpp
//Memory Time 
//252K   16MS 
 
#include<iostream>
#include<algorithm>
using namespace std;
 
typedef class dna
{
	public:
		int num;  //逆序数
		char sq[110];  //DNA序列
}DNAStr;
 
int InversionNumber(char* s,int len)
{
	int ans=0;  //s逆序数
	int A,C,G;  //各个字母出现次数，T是最大的，无需计算T出现次数
	A=C=G=0;
	for(int i=len-1;i>=0;i--)
	{
		switch(s[i])
		{
		    case 'A':A++;break;  //A是最小的，无逆序数
			case 'C':
				 {
					 C++;
					 ans+=A;  //当前C后面出现A的次数就是这个C的逆序数
					 break;
				 }
			case 'G':
				{
					G++;
					ans+=A;
					ans+=C;
					break;
				}
			case 'T':
				{
					ans+=A;
					ans+=C;
					ans+=G;
					break;
				}
		}
	}
	return ans;
}
 
int cmp(const void* a,const void* b)
{
	DNAStr* x=(DNAStr*)a;
	DNAStr* y=(DNAStr*)b;
	return (x->num)-(y->num);
}
 
int main(void)
{
	int n,m;
	while(cin>>n>>m)
	{
		DNAStr* DNA=new DNAStr[m];
		for(int i=0;i<m;i++)
		{
			cin>>DNA[i].sq;
			DNA[i].num = InversionNumber(DNA[i].sq,n);
		}
		qsort(DNA,m,sizeof(DNAStr),cmp);
		for(int j=0;j<m;j++)
			cout<<DNA[j].sq<<endl;
	}
	return 0;
}

```

