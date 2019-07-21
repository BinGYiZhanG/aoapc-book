### 任务：
写一个学生行为管理系统（SPMS）
### 概念：
在SPMS中，至多有100个学生，每个学生都有一个SID，一个CID，一个姓名（name）和四科成绩（Chinese，Mathematics，English andProgramming）
* SID（学生ID）是一个10位数字
* CID（班级ID）是一个正数，不超过20
* 姓名是一个不超过10个字母和数字的字符串，以大写字母作为开头，姓名不能包含空格
* 每个得分（score）是非负的并且不超过100
### 主菜单：
当你进入SPMS时，主菜单应该像这样被展示：
```
Welcome to Student Performance Management System (SPMS).

1 - Add
2 - Remove
3 - Query
4 - Show ranking
5 - Show Statistics
0 - Exit
```
### 添加一个学生（Adding a Student）

如果你从主菜单上选择1，在屏幕应该打印的信息是：
```
Please enter the SID, CID, name and four scores. Enter 0 to finish.
```
然后程序等待用户输入。输入行总是合法的（没有不合法的SID，CID，或者name，确切的四个score等等），但是SID或许已经存在，在这种情况下，简单地忽视它，并且打印```Duplicated SID.```
<br>
另一方面，多个学生拥有同样的姓名。<br>
您应该一直打印上面的消息，直到用户输入一个0。在那之后再次打印菜单。<br>
### 移除一个学生（Removing a Student）
如果你从主菜单上选择2，在屏幕应该打印的信息是：
```
Please enter SID or name. Enter 0 to finish.
```
然后程序等待用户输入，移除在数据库中所有与SID或name匹配的学生，打印如下信息（xx可能等于0）:<br>
```
xx student(s) removed.
```

您应该一直打印上面的消息，直到用户输入一个0。在那之后再次打印菜单。<br>

### 询问学生（Showing the Ranklist）

如果你从主菜单上选择3，在屏幕应该打印的信息是：
```
Please enter SID or name. Enter 0 to finish.

```

然后程序等待用户输入。如果没有学生匹配```SID```或者```name```，那什么也不做，否则打印出所有匹配的学生，以他们加入数据库的顺序。格式和“adding a student”的输入格式相同，但是有3列被添加，rank（第1列），总分（第2列），平均分（第3列）
最高总分的学生（考虑全部班级）```rank```为1，如果有两个```rank```为2的学生，那么下一个```rank```为4。<br>
您应该一直打印上面的消息，直到用户输入一个0。在那之后再次打印菜单。<br>

### 展示排名单

如果你从主菜单上选择4，在屏幕应该打印的信息是：
```cpp
Showing the ranklist hurts students’ self-esteem. Don’t do that.
```
然后主菜单被再次打印。<br>

### 展示统计数据（Showing Statistics）

如果你从主菜单上选择5，在屏幕应该打印的信息是：
```
Please enter class ID, 0 for the whole statistics.

```
当一个class ID被进入时，打印如下统计数据，“passed”意味着一个分数至少60。<br>
```
Chinese
Average Score: xx.xx
Number of passed students: xx
Number of failed students: xx
Mathematics
Average Score: xx.xx
Number of passed students: xx
Number of failed students: xx
English
Average Score: xx.xx
Number of passed students: xx
Number of failed students: xx
Programming
Average Score: xx.xx
Number of passed students: xx
Number of failed students: xx
Overall:
Number of students who passed all subjects: xx
Number of students who passed 3 or more subjects: xx
Number of students who passed 2 or more subjects: xx
Number of students who passed 1 or more subjects: xx
Number of students who failed all subjects: xx
```

然后主菜单被打印。<br>
### 退出SPMS（Exiting SPMS）

如果你从主菜单上选择0，程序应该终止。<br>
课程分数和总分都是整数，但是平均分应该将其格式化为一个实数，小数点后正好有两位数字。<br>

## 输入：
这里有一个简单的测试用例，以0作为结束。整个输入是合法的，输入的大小不超过10KB
## 输出：
打印出问题描述中所述的所有内容。你应该能用键盘和屏幕在你的电脑上玩这个小程序。然而，当输入和输出没有混合在一起时，就像在键盘屏幕的情况下一样，它们看起来很愚蠢。
### 提示:
在格式化浮点数(如平均分)时，防止浮点错误的一个好方法是添加一个小数字(如本问题中的1e-5)。否则，如果浮点错误为80.31499999，则80.315将被打印为80.31…

## Sample Input：
```
1
0011223344 1 John 79 98 91 100
0022334455 1 Tom 59 72 60 81
0011223344 2 Alice 100 100 100 100
2423475629 2 John 60 80 30 99
0
3
0022334455
John
0
5
1
2
0011223344
0
5
0
4
0

```

## Sample Output:

```
Welcome to Student Performance Management System (SPMS).
1 - Add
2 - Remove
3 - Query
4 - Show ranking
5 - Show Statistics
0 - Exit
Please enter the SID, CID, name and four scores. Enter 0 to finish.
Please enter the SID, CID, name and four scores. Enter 0 to finish.
Please enter the SID, CID, name and four scores. Enter 0 to finish.
Duplicated SID.
Please enter the SID, CID, name and four scores. Enter 0 to finish.
Please enter the SID, CID, name and four scores. Enter 0 to finish.
Welcome to Student Performance Management System (SPMS).
1 - Add
2 - Remove
3 - Query
4 - Show ranking
5 - Show Statistics
0 - Exit
Please enter SID or name. Enter 0 to finish.
2 0022334455 1 Tom 59 72 60 81 272 68.00
Please enter SID or name. Enter 0 to finish.
1 0011223344 1 John 79 98 91 100 368 92.00
3 2423475629 2 John 60 80 30 99 269 67.25
Please enter SID or name. Enter 0 to finish.
Welcome to Student Performance Management System (SPMS).
1 - Add
2 - Remove
3 - Query
4 - Show ranking
5 - Show Statistics
0 - Exit
Please enter class ID, 0 for the whole statistics.
Chinese
Average Score: 69.00
Number of passed students: 1
Number of failed students: 1
Mathematics
Average Score: 85.00
Number of passed students: 2
Number of failed students: 0
English
Average Score: 75.50
Number of passed students: 2
Number of failed students: 0
Programming
Average Score: 90.50
Number of passed students: 2
Number of failed students: 0
Overall:
Number of students who passed all subjects: 1
Number of students who passed 3 or more subjects: 2
Number of students who passed 2 or more subjects: 2
Number of students who passed 1 or more subjects: 2
Number of students who failed all subjects: 0
Welcome to Student Performance Management System (SPMS).
1 - Add
2 - Remove
3 - Query
4 - Show ranking
5 - Show Statistics
0 - Exit
Please enter SID or name. Enter 0 to finish.
1 student(s) removed.
Please enter SID or name. Enter 0 to finish.
Welcome to Student Performance Management System (SPMS).
1 - Add
2 - Remove
3 - Query
4 - Show ranking
5 - Show Statistics
0 - Exit
Please enter class ID, 0 for the whole statistics.
Chinese
Average Score: 59.50
Number of passed students: 1
Number of failed students: 1
Mathematics
Average Score: 76.00
Number of passed students: 2
Number of failed students: 0
English
Average Score: 45.00
Number of passed students: 1
Number of failed students: 1
Programming
Average Score: 90.00
Number of passed students: 2
Number of failed students: 0
Overall:
Number of students who passed all subjects: 0
Number of students who passed 3 or more subjects: 2
Number of students who passed 2 or more subjects: 2
Number of students who passed 1 or more subjects: 2
Number of students who failed all subjects: 0
Welcome to Student Performance Management System (SPMS).
1 - Add
2 - Remove
3 - Query
4 - Show ranking
5 - Show Statistics
0 - Exit
Showing the ranklist hurts students’ self-esteem. Don’t do that.
Welcome to Student Performance Management System (SPMS).
1 - Add
2 - Remove
3 - Query
4 - Show ranking
5 - Show Statistics
0 - Exit
```


```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
#include <cmath>
#include <string>
#include <set>
#include <algorithm>

using namespace std;

const int EPS=1e-5;
struct student{
    string SID,name;
    int CID;
    int score[5];
    double avg;///平均分
    int rank_;///排名
    bool flag;///记录该人是否被删除,false，代表被删除，或者从未被添加；true，代表没被删除
    bool operator = (const )
}stu[110],tmpstu[110];
int stu_cnt=0;///记录总人数
set<string> SIDset;
void Init(){
    for(int i=0;i<110;i++){
        stu[i].SID=stu[i].name="";
        stu[i].CID=-1;
        stu[i].score[0]=stu[i].score[1]=stu[i].score[2]=stu[i].score[3]=stu[i].score[4]=-1;
        stu[i].avg=-1;
        stu[i].rank_=-1;
        stu[i].flag=false;

    }
}

void ShowMainMenu(){
    printf("Welcome to Student Performance Management System (SPMS).\n\n");
    printf("1 - Add\n");
    printf("2 - Remove\n");
    printf("3 - Query\n");
    printf("4 - Show ranking\n");
    printf("5 - Show Statistics\n");
    printf("0 - Exit\n");
}

void Add_a_Student(){
    string sid;
    //while(cin>>sid&&sid[0]!='0'){///遇到0退出
    for(;;){
        printf("Please enter the SID, CID, name and four scores. Enter 0 to finish.\n");
        cin>>sid;
        if(sid=="0")    break;
        if(SIDset.find(sid)==SIDset.end()){///如果SID没被添加过
            SIDset.insert(sid);
            cin>>stu[stu_cnt].CID>>stu[stu_cnt].name>>stu[stu_cnt].score[0]>>stu[stu_cnt].score[1]>>stu[stu_cnt].score[2]>>stu[stu_cnt].score[3];
            stu[stu_cnt].score[4]=stu[stu_cnt].score[0]+stu[stu_cnt].score[1]+stu[stu_cnt].score[2]+stu[stu_cnt].score[3];
            stu[stu_cnt].avg=stu[stu_cnt].score[4]/4.0+EPS;
            stu[stu_cnt].SID=sid;
            stu[stu_cnt].flag=true;
            stu_cnt++;
        }
        else{
            string name;
            int cid,tmpscr[4];///只是为了读入重复数据而已
            cin>>cid>>name>>tmpscr[0]>>tmpscr[1]>>tmpscr[2]>>tmpscr[3];
            printf("Duplicated SID.\n");
        }
    }
}

int Search_SID_or_name(string str,int way){///way=1;搜索name；way=0,搜索SID
    int cnt=0;
    if(way){
        for(int i=0;i<stu_cnt;i++){
            if(stu[i].name==str){
                stu[i].flag=false;
                cnt++;
            }
        }
    }
    else{
        for(int i=0;i<stu_cnt;i++){
            if(stu[i].SID==str){
                stu[i].flag=false;
                cnt++;
            }
        }
    }
    return cnt;
}

void Remove_a_Student(){
    string str;
    for(;;){
        printf("Please enter SID or name. Enter 0 to finish.\n");
        int cnt=0;
        cin>>str;


        if(str=="0") break;
        if(isupper(str[0])){///姓名以大写字母开头，所以判断首字母
            cnt=Search_SID_or_name(str,1);
        }
        else{
            cnt=Search_SID_or_name(str,0);
        }
        printf("%d student(s) removed.\n",cnt);
    }
}

bool cmp(student a,student b){
    if(a.flag!=b.flag)   return a.flag>b.flag;
    else if(a.score[4]!=b.score[4])     return a.score[4]>b.score[4];

}

void Create_Ranklist(){
    sort(stu,stu+110,cmp);
    stu[0].rank_=1;
    for(int i=1;i<stu_cnt;i++){
        if(stu[i].score[4]==stu[i-1].score[4]){
            stu[i].rank_=stu[i-1].rank_;
        }
        else{
            stu[i].rank_=i+1;
        }
    }
}

void search_sid_name(string ,int way){
///way=1,搜索姓名；way=0,搜索sid
    if(way){
        for()
    }
}

void Show_the_Ranklist(){
    string str;
    Create_Ranklist();
    for(;;){
        printf("Please enter SID or name. Enter 0 to finish.\n");
        cin>>str;

        if(str=="0")    break;
        if(isupper(str[0])){///姓名
            
        }
        else{///SID

        }
    }
}

int main(){
    Init();
    int cmd;
    ///while(scanf("%d",&cmd)==1&&cmd!=0){
    for(;;){
        ShowMainMenu();
        scanf("%d",&cmd);
        if(cmd==0)  break;
        if(cmd==1)  Add_a_Student();
        if(cmd==2)  Remove_a_Student();
        if(cmd==3);
        if(cmd==4)  printf("Showing the ranklist hurts students’ self-esteem. Don’t do that.\n");
        if(cmd==5);
    }
    return 0;
}


```

