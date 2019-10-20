### 思路
![](https://github.com/BinGYiZhanG/aoapc-book/blob/master/To%20Be%20a%20ACMer/Images/POJ1503.jpg)


```cpp
#include <iostream>
#include <cstdio>
#include <cstring>

using namespace std;

const int large=1000;
char sum_tmp[large];
char digit_tmp[large];

int plus_(int j,int carry_bit){
    int cnt;
    cnt=(sum_tmp[j]-'0')+(digit_tmp[j]-'0')+carry_bit;
    sum_tmp[j]=cnt%10+'0';
    if(cnt<10)  return 0;
    else    return 1;
}

int main(){
    int length,i,j,k;
    int max_=0,carry_bit=0;
    char digit[large],sum[large];

    memset(sum_tmp,'0',sizeof(sum_tmp));

    for(i=-1;strcmp(digit,"0");){
        i++;
        gets(digit);
        length=strlen(digit)-1;

        memset(digit_tmp,'0',sizeof(digit_tmp));

        for(k=0,j=length;j>=0;--j,++k)
            digit_tmp[k]=digit[j];///倒置

        if(max_<length)
            max_=length;

        for(carry_bit=0,j=0;j<=max_;j++)
            carry_bit=plus_(j,carry_bit);

        if(carry_bit==1)        ///最高位进位检查
            sum_tmp[++max_]='1';

        for(i=max_,j=0;i>=0;--i,++j){
            if(i==max_&&sum_tmp[i]=='0'){
                --max_;
                continue;
            }
            sum[j]=sum_tmp[i];///倒置
        }
        sum[j]='\0';
    }
    printf("%s\n",sum);
    return 0;
}

```
