
* 首先对于基本的查询，不会
```
int main()
{
    string line="\"firstName\": \"John\",";
    int comma2=line.find("\""),
    comma3=line.find("\""),
    comma4=line.find("\"");
    printf("comma2:%d,comma3:%d,comma4:%d\n",comma2,comma3,comma4);

    return 0;
    
}


```


* [方法：转成一个长字符串](https://blog.csdn.net/banana_cjb/article/details/78780869)


```

/*
#include <iostream>
#include <map>
#include <string>
#include <cstdio>
using namespace std;

map<string,string> out_str;
map<string,map<string,string> > out_object;

int main(){
    int n,m;
    bool Is_object;
    string line;
    scanf("%d%d",&n,&m);
    getchar();
    for(int i=0;i<n;i++){
        getline(cin,line);
        if(line=="{"||line=="}"||line=="},")
            continue;
        else{
            if(Is_object){

            }

            ///普通行：提取键值，
            string key,value;
            int comma2=line.find("\""),
            comma3=line.find("\""),
            comma4=line.find("\"");


        }
    }
}
*/

#include <iostream>
#include <string>
#include <map>

using namespace std;

map<string,string> mp;
void format(string &s){
    for(int i=0;i<s.size();i++)
        if(s[i]=='\\')  s.erase(s.begin()+i);
}

///输入的json是一长串字符,
void deal(string &json,string &add){
    string key,value;
    for(int i=0;i<json.size();i++){
        if(json[i]=='"'){
            int j=json.find(":",i+1);///找到":"的位置，从第i+1的位置向后找
            ///一,
            ///"(i+1)string(j-1)"(j):"string",
            ///所以截取长度是:j-i-2
            key=json.substr(i+1,j-i-2);///取得键值key
            if(add=="")
                key=add+key;
            else
                key=add+"."+key;
            ///"string":"(j+1)string"
            if(json[j+1]=='"'){///json形式是:<string,string>
                ///二，
                ///接着 一 来说，分为两种情况:
                ///1,"string":{(j+1)"string":"string"}
                ///2,"string":"(j+1)string"
                ///这个if相当于情况2
                if(json.find(",",j+1)!=string::npos)///相当于情况2的字符串又分为:"string":"string1","string":"string2"
                    i=json.find(",",j+1);///"string":"(j+1)s(j+2)tring1"(j-1),(i)"string2"
                else///这相当于到了json字符串的最后
                    i=json.size()-1;
                value=json.substr(j+2,i-j-3);///不清楚为什么是i-j-3???
                format(key);
                format(value);
            }///相当于json[j+1]='{'
            ///相当于情况1
            else{///value为对象,要通过递归实现
                ///括号匹配
                int cnt=1;
                i=j+2;///j+1 是'{'，j+2，正好跳过了第一个object的'{',所有下面的匹配是'}'
                while(cnt!=0){///"{"与"}"得配对,,
                    if(json[i]=='{')
                        ++cnt;
                    else if(json[i]=='}')
                        --cnt;
                    ++i;
                }
                value=json.substr(j+1,i-j-1);///为什么不是j+2 j+1:是为了满足截取{"string":"string"}的条件
                deal(value,key);
            }
            mp[key]=value;
        }
    }
}

int main(){
    int n,m;
    scanf("%d%d",&n,&m);
    string s,json;
    string::iterator it;
    getchar();
    for(int i=0;i<n;i++){
        getline(cin,s);
        for(it=s.begin();it!=s.end();)
            if(isspace(*it))
                it=s.erase(it);
            else
                ++it;
        json+=s;
    }

    string add;
    deal(json,add);
    for(int i=0;i<m;i++){
        cin >> s;
		if (mp.find(s) != mp.end()){
			if (mp[s][0] == '{')
				cout << "OBJECT" << endl;
			else
				cout << "STRING " << mp[s] << endl;;
		}
		else
			cout << "NOTEXIST" << endl;
    }
}


```

