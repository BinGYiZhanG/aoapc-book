* [题目](https://www.luogu.org/problem/P1078)
* 在于建图，每个国家的文化可能不同，不同文化的国家可能不可达

```
#include<bits/stdc++.h>
using namespace std;
int n,k,m,s,t,c[120],g[120][120],f[120][120],aa,bb,cc;
int main(){
    cin>>n>>k>>m>>s>>t;
    for(register int i=1;i<=n;i++)
        for(register int j=1;j<=n;j++)
            f[i][j]=21743822;
    for(register int i=1;i<=n;i++){
        cin>>c[i];
    }
    for(register int i=1;i<=k;i++){
        for(register int j=1;j<=k;j++){
            cin>>g[i][j];
        }
    }
    for(register int i=1;i<=m;i++){
        cin>>aa>>bb>>cc;
        if(!g[c[bb]][c[aa]]&&c[bb]!=c[aa])f[aa][bb]=min(f[aa][bb],cc);
        if(!g[c[aa]][c[bb]]&&c[bb]!=c[aa])f[bb][aa]=min(f[bb][aa],cc);
    }
    if(c[s]==c[t]){
        cout<<-1;
        return 0;
    }
    for(register int i=1;i<=n;i++){
        for(register int j=1;j<=n;j++){
            if(i!=j)
                for(register int k=1;k<=n;k++){
                    if(j!=k&&i!=k){
                        if(f[i][k]+f[k][j]<f[i][j]){
                            f[i][j]=f[i][k]+f[k][j];
                        }
                    }
                }
        }
    }
    if(f[s][t]==21743822)cout<<-1;
    else cout<<f[s][t];
}
```
