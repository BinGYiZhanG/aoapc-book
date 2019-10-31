* 段落   
  * 一般情况下，连续多行输入构成一个段落
  * 转换规则是在段落的第一行行首插入 `<p>`，在最后一行行末插入 `</p>`
* 标题   
  * 每个标题区块只有一行，由若干个 `#` 开头，接着一个或多个空格，然后是标题内容，直到行末
  * `# Heading` 转换为 `<h1>Heading</h1>`，`## Heading` 转换为 `<h2>Heading</h2>`，以此类推。标题等级最深为 6。
* 无序列表 
  * 无序列表由若干行组成，每行由 `*` 开头，接着一个或多个空格，然后是列表项目的文字，直到行末
  * 在最开始插入一行 `<ul>`，最后插入一行 `</ul>`
  * `* Item` 转换为 `<li>Item</li>`

* 行内
  * `_Text_` 转换为 `<em>Text</em>`
  * `[Text](Link)` 转换为 `<a href="Link">Text</a>`
  
### 题解

* 我自己写的，只是对于段落（没处理明白），标题，无序列表进行了处理，但是对于行内要三个分支分别加处理，是在麻烦

```
#include <iostream>
#include <string>
using namespace std;

int main()
{
    string line;
    bool star_is=false;///检测 * 是否存在
    int para_is=0;
    while(getline(cin,line)){
        if(line[0]=='#'){///标题
            if(star_is){
                cout<<"</ul>"<<endl;
                star_is=false;
            }
            if(para_is){
                para_is=0;
                if(para_is==1)
                    cout<<"</p>\n";
                else
                    cout<<"\n</p>\n";
            }
            int cnt=1;///记录'#'个数
            while(line[cnt++]=='#');///cnt-1为#个数
            int nullspace=cnt-1;
            while(line[nullspace++]==' ');
            //printf("nullspace:%d\n",nullspace);nullspace-1为标题字符串的开始
            string out_str=line.substr(nullspace-1,(int)line.size()-nullspace+1);///输出标题
            //cout<<out_str<<endl;
            cout<<"<h"<<cnt-1<<">"<<out_str<<"</h"<<cnt-1<<">"<<endl;
        }
        else if(line[0]=='*'){///无序列表
            if(para_is){
                para_is=0;
                if(para_is==1)
                    cout<<"</p>\n";
                else
                    cout<<"\n</p>\n";
            }
            if(star_is==false){///第一次出现 * ，要输出<ul>
                int cnt=1;
                while(line[cnt++]==' ');
                ///cout<<"cnt:"<<cnt<<endl;cnt-1是字符串开始的下标位置
                string out_str=line.substr(cnt-1,(int)line.size()-cnt+1);

                cout<<"<ul>\n<li>"<<out_str<<"</li>\n";
                star_is=true;
            }else{///不是第一次出现 * 了
                int cnt=1;
                while(line[cnt++]==' ');
                ///cout<<"cnt:"<<cnt<<endl;cnt-1是字符串开始的下标位置
                string out_str=line.substr(cnt-1,(int)line.size()-cnt+1);

                cout<<"<li>"<<out_str<<"</li>\n";
            }
        }
        else{///段落
            if(star_is){
                cout<<"</ul>"<<endl;
                star_is=false;
            }
            if(para_is==0){///第一次出现
                cout<<"<p>"<<line;
                para_is++;
            }else{///不是第一次出现
                cout<<"\n"<<line;
                para_is++;
            }
        }
    }

    return 0;
}


```

* 优质题解，第一步处理完之后，生成字符串，然后再处理（行内处理），生成最终结果
  * 60分代码,自己改了一下

```
#include <iostream>
#include <string>
using namespace std;

const int maxn=300;
string ans[maxn];

///60分代码
string process(string val){
    string link="",tmp="";
    for(int i=0;i<(int)val.length();i++){
        if(val[i]=='_'){
            val=val.replace(val.find("_"),1,"<em>");
            val=val.replace(val.find("_"),2,"</em>");
        }
        if(val[i]=='['){///发现超链接，写对了
            val.erase(i,1);
            while(val[i]!=']')
                tmp+=val[i],val.erase(i,1);
            val.erase(i,2);
            while(val[i]!=')')
                link+=val[i],val.erase(i,1);
            val.erase(i,1);
            string res="<a href=\""+link+"\">"+tmp+"</a>";
            val.insert(i,res);
            tmp=link="";
        }
    }
    return val;
}

///100分代码
string focus(string value){//处理行内
   string a="";	string link="";
     for(int i=0;i<value.length();++i){//逐个处理
     	if(value[i]=='_'){
     		value.erase(i,1);
     		while(value[i]!='_')a+=value[i],value.erase(i,1);
     		value.erase(i,1);//去掉偶数个"_";
			 value.insert(i,"</em>");
			 value.insert(i,a);
			 value.insert(i,"<em>");
			 a="";
		 }

     	if(value[i]=='[')//发现链接，这个写对了
		 {
	        value.erase(i,1);
            while(value[i]!=']')
                a+=value[i],value.erase(i,1);
            value.erase(i,2);
            while(value[i]!=')')
                link+=value[i],value.erase(i,1);
            value.erase(i,1);
            string res="<a href=\""+link+"\">"+a+"</a>";
            value.insert(i,res);
            a=link="";
		}


	 }
	return value;
}

int main(){
    int k=0;
    for(int i=0;i<maxn;i++)
        ans[i]="";
    string line;
    bool para_is=false,star_is=false;
    while(getline(cin,line)){
        if(line==""){///如果是空行
            if(star_is){
                star_is=false;
                ans[k++]="</ul>";
            }
            if(para_is){
                para_is=false;
                ans[k-1]+="</p>";
            }
        }
        else if(line[0]=='#'){///标题
            int cnt=1;///记录'#'个数
            while(line[cnt++]=='#');///cnt-1为#个数
            int nullspace=cnt-1;
            while(line[nullspace++]==' ');
            //printf("nullspace:%d\n",nullspace);nullspace-1为标题字符串的开始
            string out_str=line.substr(nullspace-1,(int)line.size()-nullspace+1);///输出标题
            //cout<<out_str<<endl;
            string qianzhui="<h"+to_string(cnt-1)+">",houzhui="</h"+to_string(cnt-1)+">";
            ans[k++]=qianzhui+out_str+houzhui;
            //cout<<ans[k-1]<<" "<<k<<endl;
            //cout<<res<<endl;

        }
        else if(line[0]=='*'){///无序列表
            if(!star_is){///第一次出现无序列表
                star_is=true;
                ans[k++]+="<ul>";
            }
            int cnt=1;
            while(line[cnt++]==' ');
            ///cout<<"cnt:"<<cnt<<endl;cnt-1是字符串开始的下标位置
            string out_str=line.substr(cnt-1,(int)line.size()-cnt+1);
            ans[k++]="<li>"+out_str+"</li>";
            //string res="<li>"+out_str+"</li>";
            //cout<<res<<endl;
            //cout<<"<ul>\n<li>"<<out_str<<"</li>\n";
        }
        else {///段落
            if(!para_is){///第一次出现
                para_is=true;
                ans[k]+="<p>";
            }
            ans[k++]+=line;
        }

        //for(int i=0;i<k;i++){
        //    cout<<ans[i]<<endl;
        //}
    }
    if(star_is){
        ans[k++]+="</ul>";
        star_is=false;
    }
    if(para_is){
        ans[k-1]+="</p>";
        para_is=false;
    }
    for(int i=0;i<k;i++)
        cout<<process(ans[i])<<endl;

    return 0;
}


```

* 本题知识点
* replace用法:
```
replace用法:
 /*用法一： （本题用了）
 *用str替换指定字符串从起始位置pos开始长度为len的字符 
 *string& replace (size_t pos, size_t len, const string& str); 
 */  
int main()  
{  
    string line = "this@ is@ a test string!";  
    line = line.replace(line.find("@"), 1, ""); //从第一个@位置替换第一个@为空  
    cout << line << endl;     
    return 0;  
}  

 /*用法二： 
 *用str替换 迭代器起始位置 和 结束位置 的字符 
 *string& replace (const_iterator i1, const_iterator i2, const string& str); 
 */  
int main()  
{  
    string line = "this@ is@ a test string!";  
    line = line.replace(line.begin(), line.begin()+6, "");  //用str替换从begin位置开始的6个字符  
    cout << line << endl;     
    return 0;  
}  

 /*用法三： 
 *用substr的指定子串（给定起始位置和长度）替换从指定位置上的字符串 
 *string& replace (size_t pos, size_t len, const string& str, size_t subpos, size_t sublen); 
 */  
int main()  
{  
    string line = "this@ is@ a test string!";  
    string substr = "12345";  
    line = line.replace(0, 5, substr, substr.find("1"), 3); //用substr的指定子串（从1位置数共3个字符）替换从0到5位置上的line  
    cout << line << endl;     
    return 0;  
}  

```

* 输入EOF，```while(getline())```就是输入EOF结束循环,
  * 1、在windows下面，输入Ctrl+Z，然后输入回车键；
  * 2、在Linux下面，输入Ctrl+D，然后输入回车键。


* ```int```转```string```
  * ```to_string()```函数
```
1.
 
int a = 10;
char *intStr = itoa(a);
string str = string(intStr);
2.
 
int a = 10;
stringstream ss;
ss << a;
string str = ss.str();
3. C++11  （推荐，如果支持的话）
 
#include <string> 
 
std::string s = std::to_string(42);
4. C++ 98即可   （不支持C++11就用这个或者2，233 ）
 
#include <sstream>
 
#define SSTR( x ) static_cast< std::ostringstream & >( \
        ( std::ostringstream() << std::dec << x ) ).str()
5. Boost
 
#include <boost/lexical_cast.hpp>
 
int num = 4;
```


