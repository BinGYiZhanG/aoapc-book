[题目链接](http://poj.org/problem?id=3349)
 
### 题目大意

* 判断两片雪花是否相同，雪花臂的长度按照顺时针或者逆时针方向给出

* 1 Hash做法<br>
[代码思路](http://poj.org/showmessage?message_id=349869)
```cpp

#include <iostream>
#include <cstdio>
#include <algorithm>
#include <vector>
using namespace std;

const int maxn=100010;
typedef long long ll;

struct node{
    int num[6];
}s[maxn];

vector<ll> a[maxn];

void Hash(int i){
    ll sum=s[i].num[0]+s[i].num[1]+s[i].num[2]+s[i].num[3]+s[i].num[4]+s[i].num[5];
    sum%=maxn;
    a[sum].push_back(i);
}

bool judge(int x,int y){
    for(int i=0;i<6;i++){
        if(s[y].num[i]==s[x].num[0]){///存在相等
            int cnt=0;///记录相等的结果
            int posx=1;///x数组的第1个元素
            int posy=i+1;///先 正向 向后 遍历，看是否相等
            while(s[x].num[posx]==s[y].num[posy]){
                posx++;
                posy++;
                cnt++;
                if(posy>5)
                    posy=0;
            }
            if(cnt>=5) return true;///不应该根据pox来判断配对是否成功,而应该根据配对的元素个数
            cnt=0;
            posx=1;/// 反向 向左 遍历
            posy=i-1;
            if(posy<0)  posy=5;
            while(s[x].num[posx]==s[y].num[posy]){
                posx++;
                posy--;
                cnt++;
                if(posy<0)
                    posy=5;
            }
            if(cnt>=5) return true;
        }
    }
    return false;
}

bool judge(int x,int y){
    for(int i=0;i<6;i++){
        if(s[x].num[i]==s[y].num[0]){

            int cnt=0;///记录个数
            int posx=i+1,posy=1;
            while(s[x].num[posx]==s[y].num[posy]){
                posx++,posy++;
                cnt++;
                if(posx>5)
                    posx=0;
            }
            if(cnt>=5)  return true;
            cnt=0;
            posx=i-1,posy=1;
            if(posx<0)
                posx=5;
            while(s[x].num[posx]==s[y].num[posy]){
                posx--,posy++;
                cnt++;
                if(posx<0)
                    posx=5;
            }
            if(cnt>=5)  return true;
        }
    }

    return false;
}



int main(){
    int n;
    scanf("%d",&n);
    for(int i=0;i<n;i++){
        scanf("%d%d%d%d%d%d",&s[i].num[0],&s[i].num[1],&s[i].num[2],&s[i].num[3],&s[i].num[4],&s[i].num[5]);
        Hash(i);
    }

    for(int i=0;i<maxn;i++){
        if(a[i].size()>1){///这是雪花,至少有两片要进行 是否相同 判断
            for(int j=0;j<a[i].size()-1;j++){
                for(int k=j+1;k<a[i].size();k++){
                    if(judge(a[i][j],a[i][k])){
                        printf("Twin snowflakes found.\n");
                        return 0;
                    }
                }
            }
        }
    }
    printf("No two snowflakes are alike.\n");
    return 0;
}


```




