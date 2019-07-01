### 我Runtime Error了15次,
### 数组开小了，特此记录下

```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
#include <algorithm>

using namespace std;

typedef long long ll;
const int maxn=100000;
char S[maxn],T[maxn];
ll next_[maxn];
ll n,m;

void getNext(char s[],ll len){
    ll j=-1;
    next_[0]=-1;
    for(ll i=1;i<len;i++){
        while(j!=-1&&s[i]!=s[j+1]&&j+1<len){
            j=next_[j];
        }
        if(s[i]==s[j+1]&&j+1<len){
            j++;
        }
        next_[i]=j;
    }
}

bool KMP(char text[],char pattern[]){
    fill(next_,next_+maxn,0);
    getNext(pattern,m);
    ll j=-1;
    for(ll i=0;i<n;i++){
        while(j!=-1&&text[i]!=pattern[j+1]&&j+1<m)
            j=next_[j];
        if(text[i]==pattern[j+1]&&j+1<m)
            j++;
        if(j==m-1)
            return true;
    }
    return false;
}

int main()
{
    while(scanf("%s%s",S,T)==2){
        n=strlen(S),m=strlen(T);
        if(KMP(S,T))
            printf("YES\n");
        else
            printf("NO\n");
    }
    return 0;
}

```


