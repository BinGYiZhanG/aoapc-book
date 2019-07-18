
[题目链接](http://poj.org/problem?id=1011)

[参看博客](https://www.cnblogs.com/zqy123/p/4921564.html)


```cpp
#include <iostream>
#include <cstdio>
#include <cstring>

using namespace std;

int sticks[70],book[70];
///存储木棍的长度，判断是否访问
int n,len,num;
///n：木棍的总数
///len：合并后每根木棍的长度
///num：合并后的木棍数目

///快排：从大到小
void quicksort(int left,int right){
    if(left>right)
        return ;
    int temp=sticks[left],i=left,j=right;
    while(i!=j){
        while(sticks[j]<=temp&&j>i)
            j--;
        while(sticks[i]>=temp&&j>i)
            i++;
        if(i<j){
            int t=sticks[i];
            sticks[i]=sticks[j];
            sticks[j]=t;
        }
    }
    sticks[left]=sticks[i];
    sticks[i]=temp;
    quicksort(left,i-1);
    quicksort(i+1,right);
}

///cur:正在合并的木棍的长度
///k：木棍的下标
///cnt：合并好的木棍数
int dfs(int cur,int k,int cnt){

    if(cnt==num)///完成要求的情况
        return 1;
    if(cur==len)///合并好一根木棍
        return dfs(0,0,cnt+1);
    int i,pre=0;///i是木棍的下标，pre保存重复木棍
    for(i=k;i<n;i++){
        if(book[i]==0&&sticks[i]+cur<=len&&sticks[i]!=pre){///1
            pre=sticks[i];
            book[i]=1;
            if(dfs(sticks[i]+cur,i+1,cnt))///2
                break;
            book[i]=0;
            if(k==0)///3
                return 0;
        }
    }
    if(i==n)
        return 0;
    else
        return 1;
}

int main(){
    while(scanf("%d",&n)==1&&n){
    ///不能写while(scanf("%d",&n)!=EOF)
        int sum=0;///总长度
        for(int i=0;i<n;i++){
            scanf("%d",&sticks[i]);
            sum+=sticks[i];
        }
        quicksort(0,n-1);
///从大到小排序，因为合并后木棍的长度一定大于原来最长的
        for(len=sticks[0];len<=sum/2;len++){
///剪枝，从最大的长度开始枚举，这里大于sum/2归并为了合成一根木棍的情况
            if(sum%len==0){
            ///长度是总长因数才符合要求
                num=sum/len;
                memset(book,0,sizeof(book));
                if(dfs(0,0,0))
                    break;
            }
        }
        if(len>sum/2)///一根木棍的情况
            printf("%d\n",sum);
        else
            printf("%d\n",len);
    }
}

```
