[题目链接](http://poj.org/problem?id=2996)

### 题意
模拟棋盘输出
### 基本完工了，可以读入输入，并且输出，但是没有处理好输出，<br>
### 白棋是小行优先输出，黑棋是大行优先输出，行相同，则按列顺序输出

```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
#include <algorithm>
#include <string>
using namespace std;

struct chess{
    int x,y;
    char name;
    bool flag;
}white[32],black[32];
int white_cnt=0,black_cnt=0;
string line;

void Input(){
    for(int i=0;i<16;i++){
        //getline(cin,line);
        if(i%2==0)
            getline(cin,line);
        else{
            getline(cin,line);
            for(int j=0;j<33;j++){
                char tmp=line[j];
                //scanf("%c",&tmp);
                if(tmp=='K'){///白棋  ----   K
                    white[white_cnt].x=(i+1)/2;///根据规律
                    white[white_cnt].y=(j+2)/4;///根据规律
                    white[white_cnt].name=tmp;
                    white[white_cnt].flag=true;
                    white_cnt++;
                }
                if(tmp=='Q'){///白棋  ----   Q
                    white[white_cnt].x=(i+1)/2;///根据规律
                    white[white_cnt].y=(j+2)/4;///根据规律
                    white[white_cnt].name=tmp;
                    white[white_cnt].flag=true;
                    white_cnt++;
                }
                if(tmp=='R'){///白棋  ----   R
                    white[white_cnt].x=(i+1)/2;///根据规律
                    white[white_cnt].y=(j+2)/4;///根据规律
                    white[white_cnt].name=tmp;
                    white[white_cnt].flag=true;
                    white_cnt++;
                }
                if(tmp=='B'){///白棋  ----   B
                    white[white_cnt].x=(i+1)/2;///根据规律
                    white[white_cnt].y=(j+2)/4;///根据规律
                    white[white_cnt].name=tmp;
                    white[white_cnt].flag=true;
                    white_cnt++;
                }
                if(tmp=='N'){///白棋  ----   N
                    white[white_cnt].x=(i+1)/2;///根据规律
                    white[white_cnt].y=(j+2)/4;///根据规律
                    white[white_cnt].name=tmp;
                    white[white_cnt].flag=true;
                    white_cnt++;
                }
                if(tmp=='P'){///白棋  ----   P
                    white[white_cnt].x=(i+1)/2;///根据规律
                    white[white_cnt].y=(j+2)/4;///根据规律
                    white[white_cnt].name=tmp;
                    white[white_cnt].flag=true;
                    white_cnt++;
                }

                if(tmp=='k'){///黑棋  ----   K
                    black[black_cnt].x=(i+1)/2;
                    black[black_cnt].y=(j+2)/4;
                    black[black_cnt].name=tmp;
                    black[black_cnt].flag=true;
                    black_cnt++;
                }
                if(tmp=='q'){///黑棋  ----   Q
                    black[black_cnt].x=(i+1)/2;
                    black[black_cnt].y=(j+2)/4;
                    black[black_cnt].name=tmp;
                    black[black_cnt].flag=true;
                    black_cnt++;
                }
                if(tmp=='r'){///黑棋  ----   R
                    black[black_cnt].x=(i+1)/2;
                    black[black_cnt].y=(j+2)/4;
                    black[black_cnt].name=tmp;
                    black[black_cnt].flag=true;
                    black_cnt++;
                }
                if(tmp=='b'){///黑棋  ----   B
                    black[black_cnt].x=(i+1)/2;
                    black[black_cnt].y=(j+2)/4;
                    black[black_cnt].name=tmp;
                    black[black_cnt].flag=true;
                    black_cnt++;
                }
                if(tmp=='n'){///黑棋  ----   N
                    black[black_cnt].x=(i+1)/2;
                    black[black_cnt].y=(j+2)/4;
                    black[black_cnt].name=tmp;
                    black[black_cnt].flag=true;
                    black_cnt++;
                }
                if(tmp=='p'){///黑棋  ----   P
                    black[black_cnt].x=(i+1)/2;
                    black[black_cnt].y=(j+2)/4;
                    black[black_cnt].name=tmp;
                    black[black_cnt].flag=true;
                    black_cnt++;
                }
            }
        }
    }
    getchar();
}

///白棋是小行优先
int search_white(char tmp){
    int i;
    for(i=0;i<white_cnt;i++){
        if(white[i].flag==false)    continue;///已经访问过了
        if(white[i].name==tmp){
            white[i].flag=false;
            break;
        }
    }
    if(i==white_cnt)///说明没找着
        return -1;
    else{
        if(tmp!='P')
            printf("%c%c%d",tmp,'a'+white[i].y-1,8-white[i].x+1);
        else
            printf("%c%d",'a'+white[i].y-1,white[i].x);
        return 1;
    }
}

void Output_white(){
    printf("White: ");
    int cnt=0;
    if(cnt>=white_cnt)
        return ;
    for(int i=0;i<1;i++){///K 只有一个
       // printf("K");
        if(search_white('K')==-1);
        else {
            if(cnt==white_cnt-1);
            else printf(",");
            cnt++;
        }///存在，则输出','
    }
    if(cnt>=white_cnt)
        return ;
    for(int i=0;i<1;i++){///Q 只有一个
     //   printf("Q");
        if(search_white('Q')==-1);
        else {
            if(cnt==white_cnt-1);
            else printf(",");
            cnt++;
        }///存在，则输出','
    }
    if(cnt>=white_cnt)
        return ;
    for(int i=0;i<2;i++){///R 至多有两个
      //  printf("Q");
        if(search_white('R')==-1);
        else {
            if(cnt==white_cnt-1);
            else printf(",");
            cnt++;
        }///存在，则输出','
    }
    if(cnt>=white_cnt)
        return ;
    for(int i=0;i<2;i++){///B 至多有两个
       // printf("Q");
        if(search_white('B')==-1);
        else {
            if(cnt==white_cnt-1);
            else printf(",");
            cnt++;
        }///存在，则输出','
    }
    if(cnt>=white_cnt)
        return ;
    for(int i=0;i<2;i++){///N 至多有两个
      //  printf("Q");
        if(search_white('N')==-1);
        else {
            if(cnt==white_cnt-1);
            else printf(",");
            cnt++;
        }///存在，则输出','
    }
    if(cnt>=white_cnt)
        return ;
    for(int i=0;i<8;i++){///P 至多有八个
       // printf("Q");
        if(search_white('P')==-1);
        else {
            if(cnt==white_cnt-1);
            else printf(",");
            cnt++;
        }///存在，则输出','
    }
    if(cnt>=white_cnt)
        return ;
}


int main()
{
    Input();
    printf("white_cnt:%d,black_cnt:%d\n",white_cnt,black_cnt);
    Output_white();
    return 0;
}


```




