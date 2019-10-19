
![](https://github.com/BinGYiZhanG/aoapc-book/blob/master/CCF/Images/20180705211647539.png)
![](https://github.com/BinGYiZhanG/aoapc-book/blob/master/CCF/Images/20180705211716836.png)
![](https://github.com/BinGYiZhanG/aoapc-book/blob/master/CCF/Images/20180705211740856.png)

### [海岛题解，直接遍历](https://blog.csdn.net/tigerisland45/article/details/81697594#commentsedit)

### 本题有两个坑（目前还是不理解）
* 规则:/aaa/和地址/aaa不能匹配
* 规则:/ aaa 和地址/ 可以匹配



```
#include <iostream>
#include <cctype>

using namespace std;

const int maxn=100;
string p[maxn],r[maxn],s;

bool match(string& s,string& t,bool flag){
    int lent=t.size();
    int lens=s.size();
    int ps=0,pt=0;
    while(ps<lens&&pt<lent){
        if(t[pt]==s[ps])
            ps++,pt++;
        else{

            /// 匹配<xxx>，xxx 代表 int,str,path其中一个
            if(t[pt++] != '<')///本来pt指向<，++后指向<后一个字符
                return false;
            if(flag)///控制输出
                cout << ' ';

            if(t[pt]=='i'){///匹配<int>
                bool ok=false;
                while(s[ps]&&isdigit(s[ps])){
                    if(s[ps]!='0')///去掉前导零
                        ok=true;
                    if(flag&&ok)///第一次只是匹配所以不输出
                        cout<<s[ps];
                    ps++;
                }
                if(!ok)
                    return false;
                pt+=4;///跳4个因为<int>，从i开始时4个字符
            }
            else if(t[pt]=='s'){///匹配<str>
                bool ok=false;
                while(s[ps]&&s[ps]!='/'){
                    ok=true;
                    if(flag)
                        cout<<s[ps];
                    ps++;
                }
                if(!ok)
                    return false;
                pt+=4;
            }
            else if(t[pt]=='p'){///匹配<path>
                if(flag)///第二次匹配
                    while(s[ps])
                        cout<<s[ps++];
                return true;
            }
        }
    }

    return pt==lent && ps==lens;
}


int main()
{
    int n,m;
    cin>>n>>m;
    for(int i=0;i<n;i++)
        cin>>p[i]>>r[i];
    for(int i=0;i<m;i++){
        cin>>s;

        bool flag=true;
        for(int j=0;j<n&&flag;j++){///只进行一次url匹配
            if(match(s,p[j],false)){
                flag=false;
                cout<<r[j];
                match(s,p[j],true);
            }
        }
        if(flag)///
            cout<<"404";
        cout<<endl;
    }

    return 0;
}


```


