* 古罗马帝国有一个强大的政府制度，包含各式各样的部门，一个秘密的服务部门。重要文件以加密的形式在各省和首都之间发送，以防止窃听。当时最流行的密码是置换密码和递归密码。
* 替换密码将每个字母的所有出现都改为其他字母。对于所有字母的替换一定是不同的。对于某些字母，替换字母可能与原字母一致。
* 例如：应用字母替换来改变所有的字母，对于所有从‘A’到‘Y’的字母替换成其在字母表的下一个字母，对于‘Z’替换成‘A’，所以‘VICTORIOUS’转换为‘WJDUPSJPVT’
* 排列密码应用在对于一些排列到信息的字母。例如应用排列```{2,1,5,4,3,7,6,10,9,8}```到信息```VICTORIOUS```，来得到信息```IVOTCIRSUO```

* 人们很快注意到置换密码和排列密码都是相等弱的，但是如果结合起来时，他们将会是健壮的。因此，对于最重要的信息首先应该使用替换密码解密，并且结果再使用排列密码加密。
* 加密信息```VICTORIOUS```使用上述混合密码描述给到信息```JWPUDJSTVP```
* 考古学家最近在一块石板上发现了这条信息。乍一看,看起来完全没有意义，所以有人建议用一些替换和置换密码对消息进行加密。他们已经推测出加密的原始信息的可能文本，现在他们想要检查他们的推测。他们需要一个电脑程序来做这件事，所以你必须写一个。

#### 输入：

* 第一行，加密过的串
* 第二行，原始串

#### 输出：

* 输出“YES”或者“NO”


```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
#include <cstdlib>

using namespace std;

int cmp(const void *a,const void *b){
    return *(int *)a - *(int *)b;
}

int main()
{
    char s1[200],s2[200];
    while(scanf("%s%s",s1,s2)==2){
        int n=strlen(s1);
        int cnt1[26]={0},cnt2[26]={0};
        for(int i=0;i<n;i++) cnt1[s1[i]-'A']++;
        for(int i=0;i<n;i++) cnt2[s2[i]-'A']++;
        qsort(cnt1,26,sizeof(int),cmp);
        qsort(cnt2,26,sizeof(int),cmp);
        int ok=1;
        for(int i=0;i<26;i++)
            if(cnt1[i]!=cnt2[i])    ok=0;
        if(ok) printf("YES\n");
        else printf("NO\n");
    }
    return 0;
}
```
