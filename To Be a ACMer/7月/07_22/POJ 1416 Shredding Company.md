### 描述
您刚刚被派去负责为碎纸机公司开发一种新的碎纸机，虽然“普通”碎纸机只是将纸撕碎成小块，使内容变得不可读，但这种新的碎纸机需要具备以下不寻常的基本特征。<br>
* 1，碎纸机将目标号码和一张写有号码的纸作为输入。
* 2，它把纸撕成碎片，每个碎片上都有一个或多个数字。
* 3，每一块纸上所写的数字之和是最接近目标数字的数字，而不需要经过它。
例如，假定目标数字是50，纸条上有数字12346，碎纸机将会把纸条分成4片，一片上是1，一片上是2，一片上是34，一片上是6,。这是因为他们的和是43（=1+2+34+6）是所有不超过50的组合数之和中最接近目标数50的。
例如一个纸片为1,23，4，和6的结合物不是合法的，因为他们的和是34（=1+23+4+6）是小于之前的结合物的43的，结合物12,34,6也是不合法的，因为他们的和是52（=12+34+6）
大于目标数50。<br>

#### 这里有三条特殊的规则：
* 1，如果目标数和纸片上的数相同，则纸片不会被裁剪。
例如，如果目标数是100，并且纸片上的数也是100，那么纸片将不被裁剪。
* 2，如果做任何组合的和都不能使和小于或者等于目标数，那么错误将会被打印在屏幕上。例如，如果目标数是1，而纸片上的数是123，做任何合法的结合都是不可能的，因为最小的组合数之和1,2,3，和是6，大于目标数，因此，错误被打印。
* 3，如果有不止一种可能的组合，其中的和最接近目标数而没有超过目标数，则在显示器上打印“拒绝”。例如，如果目标数是15，而纸上的数字是111，那么有两种可能的组合，可能的和最大为12:(a) 1和11和(b) 11和1;因此被拒绝打印。为了开发这样一个碎纸机，您首先决定编写一个简单的程序来模拟上述特性和规则。给定两个数字，其中第一个是目标数字，第二个是要粉碎的纸张上的数字，您需要找出碎纸机应该如何“切碎”第二个数字。

### 输入：
输入包含多组测试数据，在一行上的形式，如下：<br>

```
tl num1
t2 num2
...
tn numn
0 0 
```
每个测试用例包含两个整数：（1），第一个数是目标数；（2），第二个数是在纸上要粉碎的数。<br>

两个整数的第一个数字都不能是0，例如，123是允许的，但0123是不允许的。您可以假设两个整数的长度都不超过6位。由两个0组成的一行表示输入的结束。

### 输出：
对应的输出有三种形式：
```
sum part1 part2 ...
rejected
error 
```
在第一类中，partj和sum有如下含义:
* 1.每一部分都是一张碎纸上的数字。partj的顺序对应于纸张上原始数字的顺序。
* 2.sum是被分解后的数字之和，即， sum = part1 + part2 +…
每个数字应该用一个空格隔开。<br>
如果无法进行任何组合，则打印“error”;如果不止一种可能的组合，则打印“rejected”，<br>
没有额外的字符（包括空格）被允许在每一行的开头，或者每一行的结尾。<br>



### 两个不懂的地方
* num==-1
* n_cnt=i

```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
#include <algorithm>
#pragma warning(disable: 4996)
using namespace std;

typedef pair<int,int> P;
int N,M;
int len;
char s[12];
int pw[]={1,10,100,1000,10000,100000,1000000};

///左闭右开区间,[from,to)
int get_num(int from,int to){
    if(from==to)
        return 0;
    int t=M;
    t/=pw[from];
    t%=pw[to-from];
    return t;
}

P Path[12][12];
int res;
P res_p;
bool uni;

///我始终没懂这是如何进行裁剪的，
///参数说明
///n_cnt:
///cur_cnt:
///cur_to:裁剪终点
///cur_from:裁剪起点
///cur_num:记录和
bool DFS(int n_cnt,int cur_cnt,int cur_to,int cur_from,int cur_num){
    if(cur_cnt==n_cnt){
        if(cur_num<=N&&cur_to==len){
            if(cur_num>res){
                res=cur_num;
                uni=true;
                Path[cur_from][cur_to].first=-1;
                Path[cur_from][cur_to].second=-1;
                return true;
            }else if(cur_num==res){
                uni=false;
                return false;
            }
        }
        return false;
    }
    if(cur_num>N)
        return false;
    bool flag=false;
    for(int i=cur_to+1;i<=len;i++){
        int num=get_num(cur_to,i);
        if(num!=-1){
            if(DFS(n_cnt,cur_cnt+1,i,cur_to,num+cur_num)){
                Path[cur_from][cur_to].first=cur_to;
                Path[cur_from][cur_to].second=i;
                flag=true;
            }
        }
    }
    return flag;
}


void print(P p){
    p=Path[p.first][p.second];
    if(p.first!=-1&&p.second!=-1){
        print(p);
        printf("%d ",get_num(p.first,p.second));
    }
}

int main(){
    while(scanf("%d %s",&N,s)==2){
        if(N==0&&s[0]=='0')
            break;
        len=strlen(s);
        M=atoi(s);///字符串的整数形式
        res=-1;
        uni=false;
        for(int i=1;i<=len;i++){
            DFS(i,0,0,0,0);
        }
        if(res==-1){
            printf("error\n");
            continue;
        }
        if(!uni){
            printf("rejected \n");
            continue;
        }
        printf("%d ",res);
        print(res_p);
        printf("\n");
    }
}



```













