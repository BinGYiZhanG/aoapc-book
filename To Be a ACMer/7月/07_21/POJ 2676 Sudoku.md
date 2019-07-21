### 描述：
数独是一个非常简单的任务。如图所示，一个9行9列的方桌被分割成9个较小的正方形3x3。在一些单元格中，是从1到9的十进制数字。其他单元格是空的。目标是用从1到9的十进制数字填充空单元格，每个单元格一个数字，这样在每一行、每一列和每一个标记为3x3的子正方形中，所有从1到9的数字都会出现。编写一个程序来解决给定的数独任务。

### 输入：

输入数据将从测试用例的数量开始。对于每个测试用例，后面有9行，对应于表的行。每一行都给出了一个与这一行中的单元格对应的精确的9位小数串。如果单元格为空，则用0表示。

### 输出：

对于每个测试用例，程序都应该以与输入数据相同的格式打印解决方案。根据规则，空的单元格必须被填满。如果解决方案不是唯一的，那么程序可以打印其中任何一个。

### Sample Input：
```
1
103000509
002109400
000704000
300502006
060000050
700803004
000401000
009205800
804000107
```
### Sample Output：
```
143628579
572139468
986754231
391542786
468917352
725863914
237481695
619275843
854396127
```


### 我真垃圾，做了几个小时，还是没做出来
```cpp
#include <iostream>
#include <cstdio>
#include <cstring>

using namespace std;

int mp[10][10];
char line[11];
bool legal(){

    bool vis[10];

    ///1，判断9个方块
    for(int g=0;g<7;g+=3)///遍历行
    for(int k=0;k<7;k+=3){///遍历列
    memset(vis,false,sizeof(vis));
    for(int i=1+g;i<=3+g;i++){
        for(int j=1+k;j<=3+k;j++){
            if(vis[mp[i][j]]==true&&mp[i][j]!=0)
                return false;
            else
                vis[mp[i][j]]=true;
        }
    }
    }

    ///2，遍历行
    for(int i=1;i<=9;i++){
    memset(vis,false,sizeof(vis));
    for(int j=1;j<=9;j++){
        if(vis[mp[i][j]]==true&&mp[i][j]!=0)
            return false;
        else
            vis[mp[i][j]]=true;
    }
    }

    ///3，遍历列
    for(int j=1;j<=9;j++){
    memset(vis,false,sizeof(vis));
    for(int i=1;i<=9;i++){
        if(vis[mp[i][j]]==true&&mp[i][j]!=0)
            return false;
        else
            vis[mp[i][j]]=true;
    }
    }

    return true;
}

///定义一个vis数组，设置访问：
///vis_num[1][1~9]:方块的数字1~9是否访问
///vis_num[2][1~9]:一行的数字1~9是否访问
///vis_num[3][1~9]:一列的数字1~9是否访问

bool vis_num[4][10];

int mov[4][2]={{1,0},{0,-1},{-1,0},{0,1}};

bool yuejie(int x,int y){
    if(mp[x][y]!=0&&x<1&&x>9&&y<1&&y>9)
        return false;///填充过了，或者越界了，返回false
    return true;
}

void DFS(int x,int y){
    if(legal())return ;///如果填满就返回
    if(x==9&&y==9)  return ;///访问完了
    
    for(int i=0;i<4;i++){
        int posx=x+mov[i][0];
        int posy=y+mov[i][1];
        if(yuejie(posx,posy))   continue;
        vis[1][]
    }
    
}

int main()
{
    int n;
    scanf("%d",&n);
    while(n--){
        memset(mp,0,sizeof(mp));
        for(int i=1;i<=9;i++){
            scanf("%s",line);
            for(int j=0;j<9;j++){
                mp[i][j+1]=line[j]-'0';
            }
        }
/*
        for(int i=1;i<=9;i++){
            for(int j=1;j<=9;j++){
                printf("%d",mp[i][j]);
            }
            printf("\n");
        }
        */
        
        
        printf("%d\n",legal());
    }
    return 0;
}
```











