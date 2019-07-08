[题目链接](http://poj.org/problem?id=1503)

### 我的WA代码

```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
#include <cmath>

using namespace std;

struct bign{
    int d[110];
    int len;
    bign(){
        memset(d,0,sizeof(d));
        len=0;
    }
};

bign change(char str[]){
    bign a;
    a.len=strlen(str);
    for(int i=0;i<a.len;i++){
        a.d[i]=str[a.len-1-i]-'0';
    }
    return a;
}

void print(bign a){
    for(int i=a.len-1;i>=0;i--){
        printf("%d",a.d[i]);
    }
    printf("\n");
}

bign add(bign a,bign b){
    bign c;
    c.len=0;
    int carry=0,ans=0;
    for(int i=0;i<a.len||i<b.len;i++){
        ans=(a.d[i]+b.d[i]+carry)%10;
        carry=(a.d[i]+b.d[i]+carry)/10;
        c.d[c.len++]=ans;
    }
    if(carry){
        c.d[c.len++]=carry;
    }
    return c;
}

int main()
{
    char str[110];
    bign res;
    int cnt=0;
    //res.len=0;
    while(scanf("%s",str)==1&&str[0]!='0'){
        if(cnt==0){
            res=change(str);
            //continue;
        }
        else{
            bign num=change(str);
            //print(num);
            res=add(res,num);
            //print(res);
        }
        cnt++;
    }
    print(res);

    return 0;
}

```
