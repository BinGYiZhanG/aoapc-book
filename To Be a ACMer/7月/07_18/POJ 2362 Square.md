#### 描述
给出一组不同长度的木柴，他们能够尾连尾的形成一个方格吗？
#### 输入
N，测试用例个数
M，范围：4~20，每根木柴的长度是1~100000
#### 输出
如果可以组成正方形，输出“yes”；否则输出“no”

### AC代码，在讨论区找到的
```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
#include <algorithm>
using namespace std;

int number;
int stick[10001]={0};
bool vis[10001]={false};
int length=0;

bool cmp(int a,int b){
    return a>b;
}

bool DFS(int tempLength,int tempTimes,int index){
    int now=-1;
    for(int i=index;i<number;i++){
        if(stick[i]==now&&tempLength!=length){
            continue;
        }
        if(!vis[i]&&stick[i]<=tempLength){
            now=stick[i];
            vis[i]=true;
            if(tempLength==stick[i]){
                if(tempTimes==1){
                ///为什么是1，因为外围那个循环已经确定了这是最后一次循环
                    return true;
                }
                else if(DFS(length,tempTimes-1,0)){
                    return true;
                }
                else{
                ///回溯
                    vis[i]=false;
                    return false;
                }
            }
            else if(tempLength>stick[i]){
                if(DFS(tempLength-stick[i],tempTimes,i)){
                    return true;
                }
                else{
                ///迟迟没懂
                    vis[i]=false;
                    if(tempLength==length)///尤其这步
                        return false;
                }
            }
        }
    }
    return false;
}

int main(){
    int Case;
    scanf("%d",&Case);
    for(int testcnt=0;testcnt<Case;testcnt++){
        scanf("%d",&number);
        int sum=0;
        memset(vis,0,sizeof(vis));
        for(int i=0;i<number;i++){
            scanf("%d",&stick[i]);
            sum+=stick[i];
        }
        if(sum%4!=0||number<4)
            printf("no\n");
        else{
            length=sum/4;
            sort(stick,stick+number,cmp);///升序排列
            if(stick[0]>length)
                printf("no\n");
            else if(DFS(length,4,0))
                printf("yes\n");
            else
                printf("no\n");
        }
    }
    return 0;
}

```
