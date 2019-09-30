### IP前缀与前缀列表

* ```1.2.0.0/8```不是合法的IP前缀，因为IP地址```1.2.0.0```实际上是十六进制```0x01020000```,其低24位不都是0
  * 为什么是低24位，而不是低16位？
  * 因为前缀长度```len```,是```ip```的```32-len```二进制位为0,而此```ip```地址，低24位不为0
  
### IP地址和IP前缀的匹配关系

* ```101.6.6.6```与
  * ```101.6.6.0/24```匹配，低8位为0
  * ```101.6.6.0/23```匹配，低9位为0
  * ```101.6.0.0/16```匹配，低16位为0
  * ```101.0.0.0/8```匹配，低8位为0
  * ```101.6.0.0/24```不匹配。低8位不为0
* ```101.6.6.0/24```的匹配集包含了从```101.6.6.0```开始，到```101.6.6.255```为止的所有```ip```地址
* ```101.6.6.128/25```的匹配集包含了从```101.6.6.128```开始，到```101.6.6.255```为止的所有```ip```地址
* ```101.6.6.0/24,101.6.6.128/25```的匹配集包含了从```101.6.6.0```开始，到```101.6.6.255```为止的所有```ip```地址
* ```101.6.6.6/32```的匹配集中只有一个元素:```101.6.6.6```
* ```0.0.0.0/0```的匹配集是全体```ip```地址


### 等价前缀列表

* 两个前缀列表等价，是指这两个前缀列表的匹配集相等。例如：
  * 前缀列表```101.6.6.0/24,101.6.6.128/25```与前缀列表```101.6.6.0/24```等价
  * 前缀列表```101.6.6.0/24,101.6.7.0/24```与前缀列表```101.6.6.0/23```等价
  
### 题目描述

* 给出一个前缀列表，找到与之等价的包含```ip```前缀数目最少的前缀列表
* 几种简写形式的```ip```前缀:
  * 标准型：形如```a3,a2,a1,a0/len```。例如:```101.6.6.0/24```
  * 省略后缀型：只写出```ip```地址的高位部分位段，没有写出的位段认为是```0```,但是```ip```地址至少要写一段，例如：
    * ```101.6.6/23```意为```101.6.6.0/23```
    * ```101/8```意为```101.0.0.0/8```
    * ```1/32```意为```1.0.0.0/32```
  * 省略长度型：当前前缀长度为```8,16,24,32```时，可以省略斜线和前缀长度不写
    * ```ip```地址只相应地写出前```1,2,3或4```段，例如：
      * ```101.6.6.0```意为```101.6.6.0/32```
      * ```101.6```意为```101.6.0.0/16```
      * ```1```意为```1.0.0.0/8```
      
      
### 输入格式：
* 第一行```n（n<1000000）```,表示输入的前缀列表有```n```条```ip```前缀
* 接下来```n```行，每行一个合法的```ip```前缀，```ip```前缀可能是标准型，省略后缀型，省略长度型中的任意一种

### 输出形式：

* 输出与输入前缀列表等价的包含```ip```前缀数目最少的前缀列表。
* 每个```ip```前缀占一行
* 用标准型输出
* 输出的```ip```前缀按```ip```地址从小到大，前缀长度从小到大的顺序输出



```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
#include <string>
#include <algorithm>
#include <list>

using namespace std;

struct IP{
    string ip="";
    int length=-1;
};

IP stringToIp(string& input){
    IP ip;
    string s="";
    vector<int> pow2={1,2,4,8,16,32,64,128};///2的0~7次幂
    for(int i=0;i<=(int)input.size();i++){
        if(i==(int)input.size()||!isdigit(input[i])){
        ///迷了
        ///到达字符串末尾或当前字符不是数字字符
            int k=stoi(s);///将字符串s转换为整数
            for(int ii=7;ii>=0;ii--){///求出当前整数的二进制表示
                if(k>=pow2[ii]){
                    ip.ip+="1";
                    k-=pow2[ii];
                }else
                    ip.ip+="0";
            }
            s="";
            if(input[i]=='/'){///遇到/字符，其后面的整数就代表了前缀长度
                ip.length=stoi(input.substr(i+1));
                break;
            }
        }else
            s+=input[i];
    }
    if(ip.length==-1)///输入的IP地址中不包含前缀长度
        ip.length=ip.ip.size();///前缀长度即为2进制字符串长度
    while(ip.ip.size()<32)///IP地址小于32位，在末尾补0
        ip.ip+="0";
    return ip;
}

///前缀列表101.6.6.0/24,101.6.6.128/25与前缀列表101.6.6.0/24等价
bool isChildCollection(IP&a,IP&b){//判断IP地址b是不是IP地址a的匹配集的子集
    if(a.length>b.length)
        return false;
    for(int i=0;i<a.length;++i)///在前缀长度范围内,相同
        if(a.ip[i]!=b.ip[i])
            return false;
    return true;///并且b的前缀长度大于a的，
}

///第一步合并，移除匹配集是前一IP地址子集的IP地址
void Merge1(list<IP>& ipAddress){
    auto i=ipAddress.begin(),j=ipAddress.begin();
    //cout<<"ip i的地址"<<(*i).ip<<" ip i的前缀长度"<<(*i).length<<endl;
    //cout<<"ip j的地址"<<(*j).ip<<" ip j的前缀长度"<<(*j).length<<endl;
    for(++j;j!=ipAddress.end();){
        if(isChildCollection(*i,*j)){
            j=ipAddress.erase(j);
        }else{///因为先排序了
            ++i;
            ++j;
        }
    }
}

///前缀列表101.6.6.0/24,101.6.7.0/24与前缀列表101.6.6.0/23等价
bool unionCollection(IP&a,IP&b){///判断IP地址a和b的匹配集的并集是否等于a'的匹配集
    if(a.length!=b.length)
        return false;
    for(int i=0;i<a.length-1;++i)
        if(a.ip[i]!=b.ip[i])
            return false;
    return a.ip[a.length-1]!=b.ip[a.length-1];///
}

void Merge2(list<IP>&ipAddress){//第二步合并，同级合并
    auto i=ipAddress.begin(),j=ipAddress.begin();
    for(++j;j!=ipAddress.end();){
        if(unionCollection(*i,*j)){
            j=ipAddress.erase(j);
            --(*i).length;///a'为一个新的IP前缀，其IP地址与a相同，而前缀长度比a少1
            ///如果a'合法且a的匹配集与b的匹配集的并集等于a'的匹配集，则将a与b从列表中移除
            ///并将a'插入到列表中a,b的位置
            if(i!=ipAddress.begin()){///如果a'之前存在元素，则接下来应当从a'的前一个元素开始考虑,否则继续从a'开始考虑
                --i;
                --j;
            }
        }else{
            ++i;
            ++j;
        }
    }
}

int main(){
    int N;
    cin>>N;
    list<IP>ipAddress;
    while(N--){
        string input;
        cin>>input;
        ipAddress.push_back(stringToIp(input));
    }
    ipAddress.sort([](const IP&a,const IP&b){
        if(a.ip!=b.ip)
            return a.ip<b.ip;
        return a.length<b.length;
    });
    Merge1(ipAddress);//第一步合并
    Merge2(ipAddress);//第二步合并
    for(auto&i:ipAddress){//输出IP地址
        for(int j=0;j<4;++j){//求出每8位2进制字符串代表的整数并输出
            int k=0;
            for(int ii=0;ii<8;++ii)
                k=k*2+(i.ip[ii+j*8]-'0');
            printf("%d%s",k,j<3?".":"/");
        }
        printf("%d\n",i.length);//输出前缀长度
    }
    return 0;
}


```

  

