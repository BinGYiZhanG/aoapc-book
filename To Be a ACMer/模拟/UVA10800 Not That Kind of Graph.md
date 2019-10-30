### Sample Input
```
1
RCRFCRFFCCRRC
```
### Sample Output

* Case #1:
```
|        _
|  _/\_/\  /
| /    \__/
+---------------
```
* 用3种字符绘图，R（绘制'/'，光标右上移动），F（光标右下移动，绘制'\'），C（绘制'-'，光标右移）。

* [海岛题解](https://blog.csdn.net/tigerisland45/article/details/80195948)


```

#include <bits/stdc++.h>

using namespace std;

const int N = 50;
char s[N];
char board[N + N + 2][N + 4];

int main()
{
    int n, caseno = 0, len;

    scanf("%d", &n);
    while(n--) {
        scanf("%s", s);

        // 填充底板
        memset(board, ' ', sizeof(board));

        // 画图
        int maxrow = N, minrow = N + 1, row = N;
        for(int i = 0; s[i]; i++) {
            if(s[i] == 'F') {///光标右下移动
                board[++row][i + 2] = '\\';
                maxrow = max(maxrow, row);
            } else if(s[i] == 'C') {///光标右移
                board[row][i + 2] = '_';
                minrow = min(minrow, row);
            } else if(s[i] == 'R') {///光标右上移动
                minrow = min(minrow, row);
                board[row--][i + 2] = '/';
                //minrow = min(minrow, row);
            }
            //len = i + 3;
            len=i+2;
        }

        /// 画坐标轴
        board[maxrow + 1][0] = '+';
        for(int i = 1; i <= len; i++)
            board[maxrow + 1][i] = '-';
        for(int i = minrow; i <= maxrow; i++)
            board[i][0] = '|';

        /// 去末尾空格

        maxrow++;
        for(int i = minrow; i <= maxrow; i++) {
            int j = N + 3;
            while(board[i][j] == ' ') {
                board[i][j] = '\0';
                j--;
            }
        }

        // 输出结果
        printf("Case #%d:\n", ++caseno);
        for(int i = minrow; i <= maxrow; i++)
            puts(board[i]);
        putchar('\n');
    }

    return 0;
}



```
