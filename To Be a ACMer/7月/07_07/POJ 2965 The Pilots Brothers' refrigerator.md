[题目链接](http://poj.org/problem?id=2965)

### 学习点:学会了如何生成表

![](https://github.com/BinGYiZhanG/aoapc-book/blob/master/To%20Be%20a%20ACMer/Images/07072140.png)
上图是对下面代码的解释
```cpp

/*
简单分析：根据输入要求，b代表黑棋(black)，w代表白棋(white)。因为总共才16个位置，且只有黑白两种表示，此时，可对每一次状态进行二进制压缩(其中b代表1,w代表0)，例如：
bwwb 
bbwb 
bwwb 
bwww
即可表示为1001 1101 1001 1000，其十进制值为40344。同时，计算可知根据黑白棋的摆放情况，总共有2^16种不同的状态。每一次经过有效的操作后，状态都会发生改变，此时，可借助二进制位运运算实现状态的改变，即对原有状态(相应的十进制表示)进行异或操作，以此来改变其对应二进制数的相关位置的值(1变0，0变1)。
例如：
先假设前一个状态为：
wwww 
wwww 
wwww 
wwww
即二进制表示为0000 0000 0000 0000，十进制对应为0。若此时选定左上角第一个棋子进行操作，根据规则，它右边和下边的也要同时进行变换(因为其左边和上边为空，不做考虑)，之后，相应的状态用二进制表示，应变为：1100 1000 0000 0000，十进制值为51200。这个过程相当于对十进制数51200进行对十进制数0的异或操作，即next=0^(51200)，而51200这个数则可以根据对十进制数1进行相应的左移操作得到。同时，我们知道，棋牌总共有16个位置，也就是说相应的不同的操作也有16种，即有16个不同的数经过异或操作用来改变前一个状态的值。那么，就先将这16个数枚出来吧，代码如下：
*/
int dir[4][2]={{1,0},{-1,0},{0,1},{0,-1}};
void init()
{
	int i,j,x,y,t,temp;
	for(i=0;i<4;++i)
	{
		for(j=0;j<4;++j)
		{
			temp = 0;
			temp ^= (1<<((3-i)*4+3-j));   //第一行代表16位的高4位，同理第一列也代表高位，所以棋盘(i,j)处在16位中的位置是((3-i)*4+3-j)
			//temp ^= (1<<(15 - ( i*4 + j )));
			for(t=0;t<4;++t)
			{
				x = i + dir[t][0];
				y = j + dir[t][1];
				if(x<0 || y<0 || x>3 || y>3)
					continue;
				temp ^= (1<<((3-x)*4+3-y));
			}
			cout<<temp<<" ";
		}
		cout<<endl;
	}

--------------------- 
作者：hackbuteer1 
来源：CSDN 
原文：https://blog.csdn.net/hackbuteer1/article/details/7392245 
版权声明：本文为博主原创文章，转载请附上博文链接！
```
### 本来相当成模板来看，但是超时了,

生成翻转函数
```cpp
#include <iostream>

using namespace std;

int main()
{
    for(int i=0;i<4;i++){
        int tmp=0,tmp1;
        for(int k=0;k<4;k++)
            tmp|=(1<<((3-i)*4+k));
            //printf("%d\n",(3-i)*4+k);
        tmp1=tmp;
        for(int j=0;j<4;j++){
            for(int k=0;k<4;k++){
                tmp|=(1<<(3-j+k*4));
                //printf("%d\n",3-j+k*4);
            }
            printf("%d\n",tmp);
            tmp=tmp1;
        }

    }
    return 0;
}

```

我的代码
[借鉴处](https://blog.csdn.net/hackbuteer1/article/details/7392245)
但是2965那两个代码没看懂,
```cpp
#include<iostream>
#include<queue>
#include<cstdio>
using namespace std;
#include<memory.h>
#include<cstring>

struct node{
    int x,y;
};

struct Node
{
	int state;
	int step;
	node pos[16];
};

bool visit[65536];

int change[16] =   //16种状态转换，对应4*4的翻子位置
{
63624,62532,61986,61713,
36744,20292,12066,7953,
35064,17652,8946,4593,
34959,17487,8751,4383
};

int mov[16][2]={{1,1},{1,2},{1,3},{1,4},{2,1},{2,2},{2,3},{2,4},{3,1},{3,2},{3,3},{3,4},{4,1},{4,2},{4,3},{4,4}};

Node bfs(int state)
{
	int i;
	memset(visit,false,sizeof(visit));    //标记每一个状态都未访问过
	queue<Node>q;
	Node cur,next;
	cur.state = state;
	cur.step = 0;
	q.push(cur);
	visit[state] = true;

	Node yummy;
	yummy.state=-1;
	yummy.step=-1;
	while(!q.empty())
	{
		cur = q.front();
		q.pop();
		//if(cur.state == 0 || cur.state == 0xffff)   //65535
		if(cur.state == 0)
			return cur;
		for(i=0;i<16;i++)
		{
			next.state = cur.state^change[i];
			for(int j=0;j<cur.step;j++){
                next.pos[j].x=cur.pos[j].x;
                next.pos[j].y=cur.pos[j].y;
			}
			next.step = cur.step + 1;
			if(visit[next.state])
				continue;
			//if(next.state == 0 || next.state == 0xffff)   //65535
			if(cur.state == 0)
				return next;
			visit[next.state] = true;
			next.pos[cur.step].x=mov[i][0];
			next.pos[cur.step].y=mov[i][1];
			q.push(next);
		}
	}
	return yummy;
	//return {};
}

int main(void)
{
	int i,j,state;
	char ch[5][5];
	while(scanf("%s",ch[0])!=EOF)
	{
		for(i = 1 ; i < 4 ; ++i)
			scanf("%s",ch[i]);
		state = 0;
		for(i = 0 ; i < 4 ; ++i)
		{
			for(j = 0 ; j < 4 ; ++j)
			{
				state <<= 1;
				if(ch[i][j] == '+')
					state += 1;
				//state ^= (1<<((3-i)*4+(3-j)));
			}
		}
		Node ans = bfs(state);
		if(ans.state == -1 && ans.step == -1)
			puts("Impossible");
		else{
			printf("%d\n",ans.step);
			for(int i=0;i<ans.step;i++){
                printf("%d %d\n",ans.pos[i].x,ans.pos[i].y);
			}

		}
	}
	return 0;
}
```

AC代码
[博客地址](https://blog.csdn.net/freezhanacmore/article/details/9406679)

```cpp
#include <iostream>
#include <cstring>
#include <cstdio>

using namespace std;

int mp[5][5];
int x[20],y[20];///临时路径

int ansX[20],ansY[20];///最终路径
int ans=33;

void Build(){
    char c;
    memset(mp,0,sizeof(mp));
    for(int i=0;i<4;i++){
        for(int j=0;j<4;j++){
            //scanf("%c",&c);
            cin>>c;
            mp[i][j]=(c=='-')?1:0;
        }
        getchar();///必须加上，否则读图错误
                ///如果用cin读的话，可以不加getchar()
    }
}

void flip(int s){
    int x1=s/4;         ///行
    int y1=s%4;         ///列

    for(int i=0;i<4;i++){
        mp[i][y1]=!mp[i][y1];
        mp[x1][i]=!mp[x1][i];
    }
    mp[x1][y1]=!mp[x1][y1];
}

bool complete(){///判断是否达到目标
    for(int i=0;i<4;i++)
        for(int j=0;j<4;j++)
            if(mp[i][j]==0)
                return false;
    return true;
}

void DFS(int s,int b){///遍历到第s个，翻转了b个
    if(complete()){
        if(ans>b){
            ans=b;
            for(int i=1;i<=ans;i++){
                ansX[i]=x[i];
                ansY[i]=y[i];
            }
        }
        return ;
    }

    if(s>=16)   return ;

    DFS(s+1,b);///不管第s个，直接往下找
    flip(s);///翻转第s个再往下找

    x[b+1]=s/4+1;///临时记录路径
    y[b+1]=s%4+1;

    DFS(s+1,b+1);///翻转第s个了再找下一个
    flip(s);///回溯

}

int main(){
    Build();
    /*
    for(int i=0;i<4;i++){
        for(int j=0;j<4;j++){
            printf("%d",mp[i][j]);
        }
        printf("\n");
    }
*/
    DFS(0,0);
    printf("%d\n",ans);
    for(int i=1;i<=ans;i++){
        printf("%d %d\n",ansX[i],ansY[i]);
    }

    return 0;
}

```



