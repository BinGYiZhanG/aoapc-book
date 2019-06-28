[题目链接](http://poj.org/problem?id=3253)
#### 题目翻译
农夫约翰想修理牧场周围的一小段篱笆。他测量了栅栏，发现他需要N(1≤N≤20,000)块木板，每块长度为整数Li(1≤Li≤50,000)。然后，他买了一块长木板，刚好能看到N块木板(即，它的长度是长度Li的和)。FJ忽略了“kerf”，即锯切时锯屑损失的额外长度;你也应该忽略它。
FJ悲哀地意识到他没有锯子来锯木头，于是他拿着这块长木板来到农民Don的农场，礼貌地问他是否可以借把锯子。
法默·唐是一个隐蔽的资本家，他不借给FJ一把锯子，而是提出要向法默·约翰收取木板上N-1个缺口的费用。切一块木头的费用正好等于它的长度。切一块长21英寸的木板要21美分。
然后让农夫唐决定砍木板的顺序和地点。帮助农民约翰决定他能花多少钱来制作N块木板。FJ知道他可以将木板切割成不同的顺序，这将导致不同的收费，因为中间木板的长度是不同的。

#### 输入
第一行:一个整数N，木板的数量
行2 . .N+1:每一行包含一个整数，描述所需板材的长度
#### 输出
第1行:一个整数:他必须花费的最小金额进行N-1削减

#### Sample Input

3
8
5
8

#### Sample Output

34

```cpp
#include <iostream>
#include <algorithm>
#include <cstdio>
#include <queue>
using namespace std;

typedef long long ll;
priority_queue<ll,vector<ll>,greater<ll> > q;

int main(){
    int n;
    scanf("%d",&n);
     while(!q.empty())
        q.pop();
    for(int i=0;i<n;i++){
        ll tmp;
        cin>>tmp;
        q.push(tmp);
    }

    ll sum=0;
    while(q.size()>1){
        ll fr=q.top();
        q.pop();
        ll se=q.top();
        q.pop();
        sum+=(fr+se);
        q.push(fr+se);
    }
    cout<<sum<<endl;
    return 0;
}
```









