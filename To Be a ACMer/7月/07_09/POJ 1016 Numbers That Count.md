
### 翻译
“Kronecker's Knumbers”是一家生产在标签使用的塑料数字（），这个所有者和单个雇主，追踪多少数字类型使用通过保持一个生产手册,例如
关于数字,数字不会重复出现在手册里，他写手册以一种压缩的方式,
自创数字，他想要发现哪个是自创数字，或者引导一个子串数字通过迭代应用，

未完待续
## 还差判断loop部分,hash值一直一样，得找找原因
```cpp
#include <iostream>
#include <cstring>
#include <cstdio>
#include <cmath>
#include <string>
#include <sstream>
using namespace std;

//typedef long long ll;
int hash_[20];

int transform_(char *tmp,int num,int st){
    int a[85];
    int cnt=0;
    while(num){
        a[cnt++]=num%10;
        num=num/10;
    }
 //   for(int i=cnt-1;i>=0;i--){
 //       printf("%d",a[i]);
 //   }
    for(int i=st,j=cnt-1;j>=0;j--){
        tmp[i++]=(a[j]+'0');
    }
   // printf("%d\n",cnt);
    return cnt;
}

void Hash(char *tst,int id){
    int len=strlen(tst);
    for(int i=0;i<len;i++){
        hash_[id]+=(len-i)*(tst[i]-'0');
    }
    printf("%d\n",hash_[id]);
}

int search_(){///查找该hash下是否有相等的，
                ///也就是判断是否有loop
    for(int i=0;i<15;i++){
        for(int j=i+1;j<15;j++){
            if(hash_[i]==hash_[j]&&hash_[i]!=0)
                return j-i;///直接返回loop值
        }
    }
    return -1;
}

int main()
{
    char str[85];
    int numbers[10];
    while(scanf("%s",str)==1&&str[0]!='-'){
        memset(hash_,0,sizeof(hash_));
        char tmp[85];
        memset(numbers,0,sizeof(numbers));

        int len=strlen(str);
        for(int i=0;i<len;i++){
            numbers[str[i]-'0']++;
        }
     //   for(int i=1;i<10;i++){
       //     printf("%d %d\n",i,numbers[i]);
      //  }

        int st=0;
        int tmpst=0;
        for(int i=1;i<10;i++){
            if(numbers[i]!=0){
                tmpst=transform_(tmp,numbers[i],st);
                st+=tmpst;
                tmp[st++]=(i+'0');
                //printf("%d %d %d \n",i,st,tmpst);
            }
        }
        tmp[st]='\0';
        //cout<<tmp<<endl;
        if(strcmp(tmp,str)==0){
            printf("%s is is self-inventorying\n",str);
        }
        else{
            Hash(str,0);
            Hash(tmp,1);
            printf("%s %s\n",str,tmp);
            printf("%d %d\n",hash_[0],hash_[1]);
            int cnt=1;
            while(cnt<=15){///这已经是第2次迭代了
                char tmpstr[80];
                int tmpnumbers[10];
                memset(tmpnumbers,0,sizeof(tmpnumbers));
                int len=strlen(tmp);
                for(int i=0;i<len;i++){
                    tmpnumbers[tmp[i]-'0']++;
                }
             //   for(int i=1;i<10;i++){
               //     printf("%d %d\n",i,numbers[i]);
              //  }

                st=0;
                tmpst=0;
                for(int i=1;i<10;i++){
                    if(tmpnumbers[i]!=0){
                        tmpst=transform_(tmpstr,tmpnumbers[i],st);
                        st+=tmpst;
                        tmpstr[st++]=(i+'0');
                        //printf("%d %d %d \n",i,st,tmpst);
                    }
                }
                tmpstr[st]='\0';
                Hash(tmpstr,cnt+1);
                //printf("%s %s\n",tmpstr,tmp);
                if(strcmp(tmpstr,tmp)==0){///判断step
                    printf("%s is self-inventorying after %d steps\n",str,cnt);
                    break;
                }
                if(search_()!=-1){
                    //for(int i=0;i<15;i++){
                    //    printf("%d\n",hash_[i]);
                    //}
                    printf("%s enters an inventory loop of length %d\n",str,search_());
                    break;
                }
                strcpy(tmp,tmpstr);///复制
                cnt++;
            }
        }
    }
    return 0;
}


````
