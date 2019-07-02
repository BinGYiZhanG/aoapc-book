
## 巨巨就是巨巨，tql，

[题目链接](http://poj.org/problem?id=3087)

#### 我以为得用栈做，
[巨巨地址](https://blog.csdn.net/yexiaohhjk/article/details/46505645)
我AC不了，只能学习别人代码.

#### mmp,我tm读错题了，我以为洗牌是随机的

```cpp
#include<iostream>
#include<cstdio>
#include<cstring>
#include<map>
using namespace std;
int main()
{
    int t=0,T;
    scanf("%d",&T);
    while((t++)<T)
    {
        char s1[150],s2[150],s3[310];
        int n;
        scanf("%d",&n);
        scanf("%s",s1);
        scanf("%s",s2);
        scanf("%s",s3);
        map<string,bool>book;
        int step=0;
        while(true)
        {
            char s[310];
            int ps=0;
            for(int i=0;i<n;i++)
            {
                s[ps++]=s2[i];
                s[ps++]=s1[i];
            }
            s[ps]='\0';
            step++;
            if(!strcmp(s,s3))
            {
                printf("%d %d\n",t,step);
                break;
            }
            if(book[s]==true&&strcmp(s,s3))
            {
                 printf("%d -1\n",t);
                 break;
            }
            book[s]=true;
            for(int i=0;i<n;i++)
                s1[i]=s[i];
                s1[n]='\0';
            for(int i=n,j=0;i<2*n;i++,j++)
                s2[j]=s[i];
                s2[n]='\0';
        }
    }
    return 0;
}

```
