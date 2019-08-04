### 大数乘法
```cpp
#include<iostream>
#include<cstring>
using namespace std;

const int size=50; //大数位数

void mult(char* A,char* B)
{
    int a[size+1]={0};
    int b[size+1]={0};
    int pa=0,pb=0,pc;
    int c[2*size+1]={0};

    int i,j;
    int lena=strlen(A);
    int lenb=strlen(B);

    for(i=lena-1;i>=0;i--)
        a[pa++]=A[i]-'0';
    for(j=lenb-1;j>=0;j--)
        b[pb++]=B[j]-'0';
    for(pb=0;pb<lenb;pb++) {
        for(pa=0;pa<=lena;pa++) {
            c[pa+pb]+=(a[pa]*b[pb]);
            c[pa+pb+1]+=c[pa+pb]/10;
            c[pa+pb]%=10;
            }
        }
    pc=lena+lenb-1;
    while((c[pc]==0)&&(pc>0)){
        pc--; }
    for(i=pc;i>=0;i--)
        cout<<c[i];
    cout<<endl;
    return;
}
int main()
{
    char a[size+1];
    char b[size+1];
    cin>>a>>b;
    mult(a,b);
    return 0;
}
```
