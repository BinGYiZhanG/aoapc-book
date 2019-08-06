### 思路:
* 记录枚举每种字符串，记录起点来复制，
* 

地理项目是IBM和国家地质局分析来自数以百千记的贡献者的DNA的一个研究伙伴关系，<br>
作为一个IBM研究员，你被分配写一个程序来发现所有相同的部分。<br>
一个DNA序列是以氮为基础在这个分子里的发现顺序，<br>
输入<br>

输出<br>
输出最长相等子序列，如果最长相等子序列的少于三个肌腱，则输出“no significant commonalities”，如果存在相等的长度，那么输出一开始出现的那个，

### Sample Input
```
3
2
GATACCAGATACCAGATACCAGATACCAGATACCAGATACCAGATACCAGATACCAGATA
AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
3
GATACCAGATACCAGATACCAGATACCAGATACCAGATACCAGATACCAGATACCAGATA
GATACTAGATACTAGATACTAGATACTAAAGGAAAGGGAAAAGGGGAAAAAGGGGGAAAA
GATACCAGATACCAGATACCAGATACCAAAGGAAAGGGAAAAGGGGAAAAAGGGGGAAAA
3
CATCATCATCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCCC
ACATCATCATAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA
AACATCATCATTTTTTTTTTTTTTTTTTTTTTTTTTTTTTTTTTTTTTTTTTTTTTTTTT
```
### Sample Output
```
no significant commonalities
AGATAC
CATCATCAT
```


### 由于得判断多个序列，所以暂时写不出来,
### 暴力即可

[借鉴处](https://blog.csdn.net/lyy289065406/article/details/6647262)
一个一个判断的，但是从len=1的子字符串开始,进行检测
```cpp
#include <iostream>
#include <cstring>
#include <cstdio>

using namespace std;

char str[15][65];

int main(){
    int n,m;
    scanf("%d",&n);
    while(n--){
        scanf("%d",&m);
        for(int i=0;i<m;i++){
            scanf("%s",str[i]);
        }
       // for(int i=0;i<m;i++){
       //     printf("%s\n",str[i]);
       // }

        char obj[65];///所有DNA的公共串
        int StrLen=0;///最长公共串的长度
        int length=1;///当前枚举的公共串长度

        for(int i=0;;i++){
            ///截取str[0][]中以pi为起点，长度为length的子串dna[]
            char dna[65];
            int pi=i;
            if(pi+length>60){///枚举到最后了
                length++;
                i=-1;///相当于从头开始
                if(length>60)
                    break;
                continue;
            }
            int j;
            for(j=0;j<length;j++){
                dna[j]=str[0][pi++];
            }
            dna[j]='\0';

            ///检查其他str[][]是否都存在字符串dna[]
            bool flag=true;
            for(int k=1;k<m;k++){
                if(!strstr(str[k],dna)){///存在一个DNA不含有dna[]
                    flag=false;
                    break;
                }
            }
            ///确认最大公共串
            if(flag){
                if(StrLen<length){
                    StrLen=length;
                    strcpy(obj,dna);
                }
                else if(StrLen==length){
                    if(strcmp(obj,dna)>0){///存在相同长度的公共串时，去最小字典序的串
                        strcpy(obj,dna);
                    }
                }
            }
        }

        if(StrLen<3)
			cout<<"no significant commonalities"<<endl;
		else
			cout<<obj<<endl;
    }
    return 0;
}
```







