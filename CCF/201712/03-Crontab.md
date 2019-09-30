* Crontab文件由若干行组成，每行是一条配置信息，格式如下：
  * ```<minutes> <hours> <day of month> <month> <day of week> <command>```
  * 前5项用于描述时间：
    * ```<minutes>```:分钟数，取值范围为```0~59```
    * ```<hours>```:小时数，取值范围是```0~23```
    * ```<day of month>```:月份中的天数，取值范围是```1~31```
    * ```<month>```:月份，取值范围是```1~12```，或```Jan~Dec```
    * ```<day of week>```,星期几，取值范围是```0~6```,或者```Sun~Sat```
  * 星号```*```表示可以取任何值
  * 逗号```,```表示可以取多个不同的值,减号```-```表示一段连续的取值范围
  * 星号只能单独出现，减号和逗号可以配合出现
  
* 编程输出这段时间内的任务调度执行情况  

### 样例输入
```
3 201711170032 201711222352
0 7 * * 1,3-5 get_up
30 23 * * Sat,Sun go_to_bed
15 12,18 * * * have_dinner
```



* 模拟太长,模拟到月份```<month>```和```<day of week>```之后，出现歧义


```cpp

#include <iostream>
#include <cstring>
#include <cstdio>
#include <string>
#include <vector>
#include <cmath>
#include <map>

using namespace std;

typedef long long ll;
///如何来记录时间
/*用结构体肯定是不可以的，因为时间超出数组范围
struct Day{
    int minutes;
    int hours;
    int day_month;
    int month;
    int day_week;
};
*/

int n;
string stTime,edTime;///起始时间，终止时间
string line[21];
vector<string> cmd[21];
map<string,int> month_int;
map<string,int> weekday_int;

void init(){
    month_int["Jan"]=1;month_int["Feb"]=2;month_int["Mar"]=3;month_int["Apr"]=4;
    month_int["May"]=5;month_int["Jun"]=6;month_int["Jul"]=7;month_int["Aug"]=8;
    month_int["Sep"]=9;month_int["Oct"]=10;month_int["Nov"]=11;month_int["Dec"]=12;

    weekday_int["Sun"]=0;weekday_int["Mon"]=1;weekday_int["Tue"]=2;weekday_int["Wed"]=3;
    weekday_int["Thu"]=4;weekday_int["Fri"]=5;weekday_int["Sat"]=6;
}



///0-平年，1-闰年
int month_days[2][13]={{0,31,28,31,30,31,30,31,31,30,31,30,31},{0,31,29,31,30,31,30,31,31,30,31,30,31}};

int get_weekday(int year,int month,int day){
///原理：计算与1970-1-1相隔多少天，然后对7取余
    int sum_day=0;
    if(year>1970){///如果不是1970年
        for(int i=1970;i<year;i++)
        {
            if(i%400==0||(i%4==0&&i%100!=0))///闰年
                sum_day+=366;
            else
                sum_day+=365;
        }
        bool flag=(year%400==0||(year%4==0&&year%100!=0));///判断该年是闰年还是平年
        for(int i=1;i<month;i++){
            sum_day+=month_days[flag][i];
        }
        sum_day+=day;
    }
    else{///如果是1970年
        //bool flag=(year%400==0||(year%4==0&&year%100!=0));///判断该年是闰年还是平年
        for(int i=1;i<month;i++){
            sum_day+=month_days[0][i];
        }
        sum_day+=day;
    }

    return (sum_day+3)%7;///因为 1970-1-1 是星期四
}

int main()
{
    string tmp;
    init();
    cin>>n>>stTime>>edTime;
    getchar();
    for(int i=1;i<=n;i++){
        getline(cin,line[i]);
       // int cnt=0;
        for(int j=0;j<(int)line[i].size();j++){
            if(line[i][j]!=' ')
                tmp+=line[i][j];
            else{
                cmd[i].push_back(tmp);
                tmp="";
            }
        }
        cmd[i].push_back(tmp);
        tmp="";
    }
/*
    for(int i=1;i<=n;i++){
        for(int j=0;j<(int)cmd[i].size();j++){
            cout<<" 第"<<j<<"个："<<cmd[i][j];
        }
        cout<<endl;
    }
*/

    int st_year=atoi(stTime.substr(0,4).c_str());
    int st_month=atoi(stTime.substr(4,2).c_str());
    int st_day=atoi(stTime.substr(6,2).c_str());
    int st_hour=atoi(stTime.substr(8,2).c_str());
    int st_minute=atoi(stTime.substr(10,2).c_str());

    ll st_time=st_year*pow(10,8)+st_month*pow(10,6)+st_day*pow(10,4)+st_hour*pow(10,2)+st_minute;///将开始时间转换成整数

    //cout<<"st_time "<<st_time<<endl;
    int ed_year=atoi(edTime.substr(0,4).c_str());
    int ed_month=atoi(edTime.substr(4,2).c_str());
    int ed_day=atoi(edTime.substr(6,2).c_str());
    int ed_hour=atoi(edTime.substr(8,2).c_str());
    int ed_minute=atoi(edTime.substr(10,2).c_str());

    ll ed_time=ed_year*pow(10,8)+ed_month*pow(10,6)+ed_day*pow(10,4)+ed_hour*pow(10,2)+ed_minute;///将开始时间转换成整数
    //cout<<"ed_time "<<ed_time<<endl;
    //ll tmp=209912312359;
    //cout<<"tmp "<<tmp<<endl;///可以表示最后的时间
    //cout<<"now_year "<<now_year<<" now_month "<<now_month<<" now_day "<<now_day<<" now_hour "<<now_hour<<" now_minute "<<now_minute<<endl;
/*
///将日期转换成星期

    ll st_day_week=get_weekday(st_year,st_month,st_day);
    ll ed_day_week=get_weekday(ed_year,ed_month,ed_day);

    cout<<"st_day_week "<<st_day_week<<" ed_day_week "<<ed_day_week<<endl;

*/
    for(ll i=st_time;i<ed_time;i++){
        //ll now_year=i/pow(10,8);
        ll now_year=i/100000000;
        //ll now_month=i/pow(10,6)%pow(10,2);
        ll now_month=i/1000000%100;
        //ll now_day=i/pow(10,4)%pow(10,2);///相当于day of month
        ll now_day_month=i/10000%100;
        //ll now_hour=i/pow(10,2)%pow(10,2);
        ll now_hour=i/100%100;
        //ll now_minute=i%pow(10,2);
        ll now_minute=i%100;
        ll now_day_week=get_weekday(now_year,now_month,now_day_month);


        for(int j=1;j<=n;j++){

            int flag1=false;
            if(cmd[j][0]=="*")///如果是 *
                flag1=true;
            else if(cmd[j][0].find(",")!=string::npos&&cmd[j][0].find("-")==string::npos){///如果只有有逗号
                string tmp1;
                int int_tmp1;
                for(int k=0;k<(int)cmd[j][0].size();k++){///可能有多个逗号
                    if(cmd[j][0][k]==','){///1,2,3
                        int_tmp1=atoi(tmp1.c_str());
                        if(int_tmp1==now_minute)
                            flag1=true;
                        int_tmp1=0;
                        tmp1="";
                    }else{
                        tmp1+=cmd[j][0][k];
                    }
                }

                for(int p=0;p<(int)tmp1.size();p++)
                    int_tmp1=int_tmp1*10+tmp1[p]-'0';
                if(int_tmp1==now_minute)
                    flag1=true;
            }
            else if(cmd[j][0].find(",")==string::npos&&cmd[j][0].find("-")!=string::npos){///如果只有横线
                int pos_line=cmd[j][0].find("-");
                int st_int=atoi(cmd[j][0].substr(0,pos_line).c_str()),ed_int=atoi(cmd[j][0].substr(pos_line).c_str());

                if(now_minute>=st_int&&now_minute<=ed_int)
                    flag1=true;

            }
            else if(cmd[j][0].find(",")!=string::npos&&cmd[j][0].find("-")!=string::npos){///如果横线，逗号二者都有
            ///1,3-4
            ///1,3-4,5
            ///3-4,5
            ///2-3,4-5
            ///1-2,3,4-5
            ///
                bool book[7];
                memset(book,false,sizeof(book));
                for(int k=0;k<(int)cmd[j][0].size();k++){///先把出现过的数字置为true
                    if(isdigit(cmd[j][0][k])){
                        book[cmd[j][0][k]-'0']=true;
                    }
                }
                for(int k=0;k<(int)cmd[j][0].size();k++){///遍历寻找横线'-'
                    if(cmd[j][0][k]=='-'){
                        int tmp_int_st=cmd[j][0][k-1]-'0';
                        int tmp_int_ed=cmd[j][0][k+1]-'0';
                        for(int p=tmp_int_st;p<=tmp_int_ed;p++)
                            book[p]=true;
                    }
                }

                flag1=book[now_minute];

            }
            else {///如果只有数字
                int now_int_minute=0;
                for(int k=0;k<(int)cmd[j][0].size();k++){
                    now_int_minute=now_int_minute*10+(cmd[j][0][k]-'0');
                }
                if(now_int_minute>=0&&now_int_minute<=59)
                    flag1=true;
            }

            if(flag1)
                printf("匹配上了\n");
            else
                printf("未匹配上\n");


            if(flag1){///如果时间对上了

                int flag2=false;
                if(cmd[j][1]=="*")///如果是 *
                    flag2=true;
                else if(cmd[j][1].find(",")!=string::npos&&cmd[j][1].find("-")==string::npos){///如果只有有逗号
                    string tmp1;
                    int int_tmp1;
                    for(int k=0;k<(int)cmd[j][1].size();k++){///可能有多个逗号
                        if(cmd[j][1][k]==','){///1,2,3
                            int_tmp1=atoi(tmp1.c_str());
                            if(int_tmp1==now_minute)
                                flag1=true;
                            int_tmp1=0;
                            tmp1="";
                        }else{
                            tmp1+=cmd[j][1][k];
                        }
                    }

                    for(int p=0;p<(int)tmp1.size();p++)
                        int_tmp1=int_tmp1*10+tmp1[p]-'0';
                    if(int_tmp1==now_minute)
                        flag2=true;
                }
                else if(cmd[j][1].find(",")==string::npos&&cmd[j][1].find("-")!=string::npos){///如果只有横线
                    int pos_line=cmd[j][1].find("-");
                    int st_int=atoi(cmd[j][1].substr(0,pos_line).c_str()),ed_int=atoi(cmd[j][1].substr(pos_line).c_str());

                    if(now_minute>=st_int&&now_minute<=ed_int)
                        flag2=true;

                }
                else if(cmd[j][1].find(",")!=string::npos&&cmd[j][1].find("-")!=string::npos){///如果横线，逗号二者都有
                ///1,3-4
                ///1,3-4,5
                ///3-4,5
                ///2-3,4-5
                ///1-2,3,4-5
                ///
                    bool book[7];
                    memset(book,false,sizeof(book));
                    for(int k=0;k<(int)cmd[j][1].size();k++){///先把出现过的数字置为true
                        if(isdigit(cmd[j][1][k])){
                            book[cmd[j][1][k]-'0']=true;
                        }
                    }
                    for(int k=0;k<(int)cmd[j][1].size();k++){///遍历寻找横线'-'
                        if(cmd[j][1][k]=='-'){
                            int tmp_int_st=cmd[j][1][k-1]-'0';
                            int tmp_int_ed=cmd[j][1][k+1]-'0';
                            for(int p=tmp_int_st;p<=tmp_int_ed;p++)
                                book[p]=true;
                        }
                    }

                    flag2=book[now_hour];

                }
                else{///如果只有数字
                    int now_int_hour=0;
                    for(int k=0;k<(int)cmd[j][1].size();k++){
                        now_int_hour=now_int_hour*10+(cmd[j][1][k]-'0');
                    }
                    if(now_int_hour>=0&&now_int_hour<=23)
                        flag2=true;
                }


                if(flag2){///如果小时也对上了

                    int flag3=false;
                    if(cmd[j][2]=="*")///如果是 *
                        flag3=true;
                    else if(cmd[j][2].find(",")!=string::npos&&cmd[j][2].find("-")==string::npos){///如果只有有逗号
                        string tmp1;
                        int int_tmp1;
                        for(int k=0;k<(int)cmd[j][2].size();k++){///可能有多个逗号
                            if(cmd[j][2][k]==','){///1,2,3
                                int_tmp1=atoi(tmp1.c_str());
                                if(int_tmp1==now_minute)
                                    flag1=true;
                                int_tmp1=0;
                                tmp1="";
                            }else{
                                tmp1+=cmd[j][1][k];
                            }
                        }

                        for(int p=0;p<(int)tmp1.size();p++)
                            int_tmp1=int_tmp1*10+tmp1[p]-'0';
                        if(int_tmp1==now_minute)
                            flag3=true;
                    }
                    else if(cmd[j][2].find(",")==string::npos&&cmd[j][2].find("-")!=string::npos){///如果只有横线
                        int pos_line=cmd[j][2].find("-");
                        int st_int=atoi(cmd[j][2].substr(0,pos_line).c_str()),ed_int=atoi(cmd[j][2].substr(pos_line).c_str());

                        if(now_minute>=st_int&&now_minute<=ed_int)
                            flag3=true;

                    }
                    else if(cmd[j][2].find(",")!=string::npos&&cmd[j][2].find("-")!=string::npos){///如果横线，逗号二者都有
                    ///1,3-4
                    ///1,3-4,5
                    ///3-4,5
                    ///2-3,4-5
                    ///1-2,3,4-5
                    ///
                        bool book[7];
                        memset(book,false,sizeof(book));
                        for(int k=0;k<(int)cmd[j][2].size();k++){///先把出现过的数字置为true
                            if(isdigit(cmd[j][2][k])){
                                book[cmd[j][2][k]-'0']=true;
                            }
                        }
                        for(int k=0;k<(int)cmd[j][2].size();k++){///遍历寻找横线'-'
                            if(cmd[j][2][k]=='-'){
                                int tmp_int_st=cmd[j][2][k-1]-'0';
                                int tmp_int_ed=cmd[j][2][k+1]-'0';
                                for(int p=tmp_int_st;p<=tmp_int_ed;p++)
                                    book[p]=true;
                            }
                        }

                        flag3=book[now_hour];

                    }




                    else{///如果只有数字
                        int now_int_day_month=0;
                        for(int k=0;k<cmd[j][2].size();k++){
                            now_int_day_month=now_int_day_month*10+(cmd[j][2][k]-'0');
                        }
                        if(now_int_day_month>=1&&now_int_day_month<=31)
                            flag3=true;
                    }

                    if(flag3){///如果月份中的天数也对上了
                    ///对于要匹配的月份或者星期几，有没有可能字母形式和数字形式同时出现
                        

                    }
                }


            }

        }
    }


    return 0;
}

```

