[题目链接](http://acm.hdu.edu.cn/showproblem.php?pid=5311)

### 类型：DFS

```cpp
#include <iostream>
#include <cstdio>
#include <cstdlib>
#include <cstring>
using namespace std;

char str[110],a[]="anniversary";
int len;
bool DFS(int pa,int p,int cnt){
    if(cnt>3)
        return false;
    if(cnt<=3&&pa>=11)  return true;///<=3，原因：l1，r1，l2,r2，l3,r3均可以相等
    for(int i=p;i<len;i++){
        int p1=i,p2=pa;
        while(str[p1]==a[p2]&&p1<len&&p2<11)
            p1++,p2++;
        if(p1>i&&DFS(p2,p1,cnt+1))///
            return true;
    }
    return false;
}


int main(){
    int T;
    scanf("%d",&T);
    while(T--){
        scanf("%s",str);
        len=strlen(str);
        if(DFS(0,0,0))
            puts("YES");
        else
            puts("NO");
    }
    return 0;
}




```
