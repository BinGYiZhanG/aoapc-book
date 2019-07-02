[题目链接](http://poj.org/problem?id=2996)

### 题意
模拟棋盘输出

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

}white[32],black[32];
int white_cnt=0,black_cnt=0;
string line;

void Input(){
    for(int i=0;i<16;i++){
        if(i%2==0)
            getline(cin,line);
        else{
            for(int j=0;j<33;j++){
                char tmp;
                scanf("%c",&tmp);
                if(tmp=='K'){///白棋  ----   K
                    white[white_cnt].x=(i+1)/2;///根据规律
                    white[white_cnt].y=(j+2)/4;///根据规律
                    white[white_cnt].name=tmp;
                    white_cnt++;
                }
                if(tmp=='Q'){///白棋  ----   Q
                    white[white_cnt].x=(i+1)/2;///根据规律
                    white[white_cnt].y=(j+2)/4;///根据规律
                    white[white_cnt].name=tmp;
                    white_cnt++;
                }
                if(tmp=='R'){///白棋  ----   R
                    white[white_cnt].x=(i+1)/2;///根据规律
                    white[white_cnt].y=(j+2)/4;///根据规律
                    white[white_cnt].name=tmp;
                    white_cnt++;
                }
                if(tmp=='B'){///白棋  ----   B
                    white[white_cnt].x=(i+1)/2;///根据规律
                    white[white_cnt].y=(j+2)/4;///根据规律
                    white[white_cnt].name=tmp;
                    white_cnt++;
                }
                if(tmp=='N'){///白棋  ----   N
                    white[white_cnt].x=(i+1)/2;///根据规律
                    white[white_cnt].y=(j+2)/4;///根据规律
                    white[white_cnt].name=tmp;
                    white_cnt++;
                }
                if(tmp=='P'){///白棋  ----   P
                    white[white_cnt].x=(i+1)/2;///根据规律
                    white[white_cnt].y=(j+2)/4;///根据规律
                    white[white_cnt].name=tmp;
                    white_cnt++;
                }

                if(tmp=='k'){///黑棋  ----   K
                    black[black_cnt].x=(i+1)/2;
                    black[black_cnt].y=(j+2)/4;
                    black[black_cnt].name=tmp;
                    black_cnt++;
                }
                if(tmp=='q'){///黑棋  ----   Q
                    black[black_cnt].x=(i+1)/2;
                    black[black_cnt].y=(j+2)/4;
                    black[black_cnt].name=tmp;
                    black_cnt++;
                }
                if(tmp=='r'){///黑棋  ----   R
                    black[black_cnt].x=(i+1)/2;
                    black[black_cnt].y=(j+2)/4;
                    black[black_cnt].name=tmp;
                    black_cnt++;
                }
                if(tmp=='b'){///黑棋  ----   B
                    black[black_cnt].x=(i+1)/2;
                    black[black_cnt].y=(j+2)/4;
                    black[black_cnt].name=tmp;
                    black_cnt++;
                }
                if(tmp=='n'){///黑棋  ----   N
                    black[black_cnt].x=(i+1)/2;
                    black[black_cnt].y=(j+2)/4;
                    black[black_cnt].name=tmp;
                    black_cnt++;
                }
                if(tmp=='p'){///黑棋  ----   P
                    black[black_cnt].x=(i+1)/2;
                    black[black_cnt].y=(j+2)/4;
                    black[black_cnt].name=tmp;
                    black_cnt++;
                }
            }
        }
    }
}

int search_white(char tmp){
    int i;
    for(i=0;i<white_cnt;i++)
        if(white[i].name==tmp)
            break;
    if(i==white_cnt)///说明没找着
        return -1;
    else{
        printf("%c%c%d",tmp,'a'+white[i].y-1,white[i].x);
        return 1;
    }
}

void Output(){
    printf("White: ");
    
}

int main()
{
    Input();
    OutPut();
    return 0;
}

```




