
## 01字符串不会读入

```cpp
#include <iostream>
#include <cstdio>
#include <cstring>

using namespace std;
int what[1010];
int goruns[1010];
int main()
{
    int n;
    
    scanf("%d",&n);
    scanf("%s",what);
    int len=strlen(what);
    for(int i=0;i<len;i++){
        scanf("%d",&goruns[i]);
    }
    int maoruns=0,meiruns=0;
    int i=0;
    while(true){
        if(what[i]=='0')///学妹赢了
            meiruns+=goruns[i];
        else
            
    }
    
    return 0;
}

```
