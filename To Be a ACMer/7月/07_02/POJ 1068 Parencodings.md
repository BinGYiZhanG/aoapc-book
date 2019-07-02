
[题目链接](http://poj.org/problem?id=1068)

### AC代码
```cpp
#include <iostream>
#include <string>
#include <cstdio>
#include <algorithm>

using namespace std;



int main()
{
    int T;
    scanf("%d",&T);
    while(T--){
        int n;
        string str;
        int rightcnt=0;///统计右括号数
        scanf("%d",&n);
        int pretmp,tmp;
        for(int i=0;i<n;i++){
            if(i==0){
                scanf("%d",&tmp);
                for(int i=0;i<tmp;i++)
                    str+='(';
                str+=')';
                rightcnt++;
                pretmp=tmp;
            }
            else{
                scanf("%d",&tmp);
                if(pretmp<tmp)///加左括号'('
                    for(int i=0;i<tmp-pretmp;i++)
                        str+='(';

                str+=')';
                rightcnt++;
                pretmp=tmp;
            }
        }
        //cout<<str<<endl;
        //cout<<rightcnt<<endl;
        int cnt=0;

        for(int i=0;i<str.size();i++){
            if(str[i]==')'){
                int tmpleft=0,tmpright=1;///统计配对的括号数，tmpleft为左括号数，tmpright为右括号数
                for(int j=i-1;j>=0;j--){///统计的配对括号数
                    if(str[j]==')')
                        tmpright++;
                    if(str[j]=='(')
                        tmpleft++;
                    if(tmpleft==tmpright)
                        break;
                }
                if(cnt==0)
                    printf("%d",tmpleft);
                else
                    printf(" %d",tmpleft);
                cnt++;
            }
        }
        printf("\n");
    }
    return 0;
}

```
