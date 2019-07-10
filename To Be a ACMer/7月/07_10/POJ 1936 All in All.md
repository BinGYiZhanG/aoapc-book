[题目链接](http://poj.org/problem?id=1936)

知识点:
* 清空char数组
```cpp
memset(str1,'\0',sizeof(str1));
```

[借鉴处](https://blog.csdn.net/lyy289065406/article/details/6647292)

```cpp
#include <iostream>
#include <cstdio>
#include <cstring>

using namespace std;

int main()
{
    char str1[100010],str2[100010];
    while(scanf("%s%s",str1,str2)==2){
        int len1=strlen(str1),len2=strlen(str2);
        int i=0,j=0;
        while(true){
            if(i==len1){
                printf("Yes\n");
                break;
            }
            else if(i<len1&&j==len2){
                printf("No\n");
                break;
            }
            if(str1[i]==str2[j]){
                i++;
                j++;
            }
            else
                j++;
        }
        memset(str1,'\0',sizeof(str1));
        memset(str2,'\0',sizeof(str2));
    }

    return 0;
}

```
