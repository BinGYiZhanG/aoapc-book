[题目链接](http://poj.org/problem?id=1001)

### 说实话，真的舒服，虽说还没做出来

```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
using namespace std;

typedef long long ll;

char str[10];

struct bign{
    int d[100];
    int len;
    bign(){
        memset(d,0,sizeof(d));
        len=0;
    }
};

bign change(){
    bign a,res;
    res.len=a.len=strlen(str);
    for(int i=0;i<a.len;i++){
        if(str[a.len-i-1]=='.') continue;
        a.d[i]=str[a.len-i-1]-'0';
    }

    for(int i=a.len-1;i>=0;i--){
        res.d[res.len-i-1]=a.d[i];
    }
    return res;
}

void print(bign a){
    //for(int i=a.len-1;i>=0;i--){
    for(int i=0;i<a.len;i++){
        printf("%d",a.d[i]);
    }
    printf("\n");
}

bign multi(bign a,bign b){
    bign c;
    int i,j;
    int carry=0;
    int ans=0;
    c.len=100;
    for(i=0;i<a.len;i++){
        carry=0;
        for(j=0;j<b.len;j++){
            ans=(a.d[i]*b.d[j]+c.d[i+j])%10;
            carry=(a.d[i]*b.d[j]+c.d[i+j])/10;
            c.d[i+j]=ans;
        }
        if(carry){
            c.d[i+j]=carry;
        }
    }
    c.len=i+j;
    for(int k=c.len-1;k>=0;k--){
        if(c.d[k]==0)
            c.len--;
    }
    return c;
}


int main()
{
    int n;
    while(scanf("%s%d",str,&n)){
        int len=strlen(str);
        int comma=-1;
        for(int i=0;i<len;i++){
            if(str[i]=='.'){
                comma=i;
                break;
            }
        }
       // comma=comma+1;
        for(int i=comma;i<len-1;i++){
            str[i]=str[i+1];
        }
        if(comma!=-1)
            str[len-1]='\0';
        bign num = change();
        print(num);

        bign res=multi(num,num);
        print(res);


    /*
        ll num=0;
        for(int i=0;i<len;i++){
            if(str[i]=='.')
                continue;
            num=num*10+(str[i]-'0');
        }

        //cout<<num<<endl;

        ll dot_pos=len-comma;
        //cout<<dot_pos<<endl;
        for(int i=1;i<n;i++){
            int tmp=dot_pos*2;
            ll tmpnum=num*num;
            dot_pos=tmp;
            num=tmpnum;
        }
        //cout<<dot_pos<<endl;
        cout<<num<<endl;
    */

    }
    return 0;
}

```
