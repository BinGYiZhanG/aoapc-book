[题目链接](http://poj.org/problem?id=1035)

你，作为一个新的拼写项目的发展团队中的一员，正在写一个使用在他们的形式下一个所有正确单词的字典检查所给单词的正确性.
如果字典漏了，随后他将被在以下操作中获取的正确单词代替:<br>
* 从单词中删除一个字母<br>
* 用任意字母一个代替单词里的字母<br>
* 向单词里插入任意一个字母<br>
你的任务是写一个程序发现从所给单词字典里发现所有可能的替换。<br>
输入：<br>
输入文件的第一部分包含来自字典的所有单词，每一个单词出现在他自己的行上，这部分以单个的字符"#"结束作为分隔行，所有的单词都是不同的，在字典里至多有10000个单词，<br>
文件的下一部分包含所有被检查的单词，每一个单词包含在他的新行里，这一部分也是一个字符“#”结束，至多有50个单词要被检查。
在输入文件的所有单词只包含小写字母，并且每个单词不超过15个字符，
输出：<br>
按照输入文件的第二部分的单词出现次序来写入输出文件，如果单词是正确的，写“is correct”,如果这个单词不是正确的，首先写出这个单词，随后写出字符“:”,随后写出他的可能的替换,这个替换应该以在字典中单词出现的次序作为依据（输入文件的第一部分），如果单词没有替换，则只写“:”。



### 输出未考虑顺序，
```cpp
#include <iostream>
#include <cstdio>
#include <string>
#include <cstring>
#include <vector>

using namespace std;

vector<string> first;

bool Search(string str){
    bool flag=false;
    int len=first.size();
    for(int i=0;i<len;i++){
        if(first[i]==str){
            flag=true;
            break;
        }
    }
    return flag;
}

int main()
{
    string str;
    while(cin>>str&&str[0]!='#'){
        first.push_back(str);
    }
    while(cin>>str&&str[0]!='#'){

        if(Search(str)){
            cout<<str<<" is correct";
        }
        else{
            cout<<str<<":";
            ///删除一个字母
            int len=str.length();
            for(int i=0;i<=len;i++){///是=，而非<
                string tmp;
                tmp=str.substr(0,i-1)+str.substr(i);
                if(Search(tmp))
                    cout<<" "<<tmp;
            }
            ///用任意字母代替单词里的字母
            for(int i=0;i<=len;i++){
                for(char ch='a';ch<='z';ch++){
                    string tmp;
                    tmp=str.substr(0,i-1)+ch+str.substr(i);
                    if(Search(tmp))
                        cout<<" "<<tmp;
                }
            }
            ///向单词里插入一个字母
            for(int i=0;i<=len;i++){
                for(char ch='a';ch<='z';ch++){
                    string tmp;
                    tmp=str.substr(0,i)+ch+str.substr(i);
                    if(Search(tmp))
                        cout<<" "<<tmp;
                }
            }
        }
        printf("\n");
    }
    return 0;
}

/*不能这么写，有顺序要求
#include <iostream>
#include <cstdio>
#include <string>
#include <set>

using namespace std;

set<string> st;


int main()
{
    string str;
    while(cin>>str&&str[0]!='#'){
        st.insert(str);
    }


   */




```














