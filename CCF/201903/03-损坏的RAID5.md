


### 然后需要处理条带和磁盘的关系了

```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
#include <vector>

using namespace std;

int n;///阵列中硬盘的数目
int s;///阵列的条带大小
int l;///现存的硬盘数目

char disk[1010][810];
char tmp[810];

int main(){
    scanf("%d%d%d",&n,&s,&l);
    for(int i=0;i<l;i++){
        int number;
        scanf("%d %s",&number,tmp);
        strcpy(disk[number],tmp);
    }
/*
    for(int i=0;i<l;i++){
        printf("%s\n",disk[i]);
    }
    */
    
    int m;
    scanf("%d",&m);
    for(int i=0;i<m;i++){
        int num;
        scanf("%d",&num);///读取的块的编号
        
    }
    
}
```








这个[题解](https://blog.csdn.net/wingrez/article/details/88676430)比较清晰

