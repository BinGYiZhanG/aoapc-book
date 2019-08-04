一种新的编程语言D++的创建者已经发现，不管他们对超长int类型的限制是什么，有时候程序员需要操作更大的数字。1000个数的限制太小了...你应该发现两个数最大是1000000位的乘积。
### 输入：
第一行，N，整数长度（为了保证他们的长度相同，可以添加前导零）。这些数按列给出。<br>
接下来N行每行包含2个数，中间带一个空格。每个被给的数不小于1，他们的和的长度不大于N。

### 输出：
输出文件应该包含确切的N个数在一行上代表两个数的和。<br>

```cpp
#include <iostream>
#include <cstring>
#include <string>

using namespace std;

const int size_=1000000;
int n;

int a[size_+1];
int b[size_+1];

void add(char* A,char* B,char* ans){
    memset(a,0,sizeof(a));
    memset(b,0,sizeof(b));
    int pa=0,pb=0;

    int lena=strlen(A);
    int lenb=strlen(B);

    ///倒序

    for(int i=lena-1;i>=0;i--)
        a[pa++]=A[i]-'0';

    for(int j=lenb-1;j>=0;j--)
        b[pb++]=B[j]-'0';

    int len=lena>lenb?lena:lenb;
    char* c=new char[len+1];///倒序的ans

    int w=0;
    for(int k=0;k<len;k++){
        int tmp=a[k]+b[k]+w;
        c[k]=tmp%10+'0';
        w=tmp/10;
    }
    len--;

    for(w=0;len>=0;len--)
        ans[w++]=c[len];

    ans[w]='\0';

    delete c;
    return ;
}

char A[size_+1];
char B[size_+1];
char ans[size_+1];

int main(){
    int i;
    while(cin>>n){
        getchar();
        for(i=0;i<n;i++){
            A[i]=getchar();
            getchar();
            B[i]=getchar();
            getchar();
        }
        A[i]=B[i]='\0';

        add(A,B,ans);
        cout<<ans<<endl;
    }
    return 0;
}
```
