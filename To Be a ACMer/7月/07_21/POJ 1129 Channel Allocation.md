### 描述：
当一个广播站在一个很大范围进行广播时，重复者习惯于转播信号以便每一个接受这能够有一个强信号。然而，每一个转发器使用的频道一定要是仔细挑选过的以便相邻的转发器不能打断其他人。如果相邻的转发器使用不同的频道，这种情况是可满足的。<br>
因为无线广播频率光谱是一种及其宝贵的资源，一个给定的中继器网络所需要的信道数量应该最小化。你应该写一个程序来读入一个转发器网络的描述并且决定所需信道的最小数量。
### 输入:
输入包括若干转发器网络的映射。每个映射都以包含转发器数量的行开始。这是在1和26之间，转发器由字母表中以A开头的连续大写字母表示。例如，是个转发器有名字A，B，，I和J.0个转发器的网络表示输入结束。<br>

接下来的转发器是一系列毗邻关系，每一行的形式为：<br>
* A:BCDH <br>
这表明转发器B，C，D和H与转发器A毗邻，第一行描述那些与转发器A毗邻的，第二行描述与转发器B毗邻的，等等以致全部转发器。<br>
如果一个转发器没有任何毗邻的转发器，它的形式如下：<br>
* A:
转发器以字母序列出。<br>

需要指出的是，邻接关系是一种对称的关系，如果A毗邻B，那么B也毗邻A。此外，由于转发器位于一个平面上，连接相邻转发器形成的图没有任何交叉的线段。

### 输出：
对于每个映射(除了最后一个没有转发器的映射)，打印一行包含所需要的最小通道数，这样相邻的通道就不会相互干扰。示例输出显示了这一行的格式。当只需要一个通道时，请注意通道的单复数形式。

### Solution
### [DFS](https://blog.csdn.net/non_cease/article/details/7313613)
```cpp
#include <iostream>
#include <cstdio>
#include <cstring>
using namespace std;
 
#define M 26
 
int n, ans, color[M]; 
bool map[M][M], isFind;
 
bool ok(int x, int c) {   //判断是否存在相邻节点颜色相同
     for (int i = 0; i < n; i++)
        if (map[x][i] && c == color[i])
            return false;
     return true;
}
 
void DFS(int id, int total) {   //当前搜索到下标为id的节点，此时总共用的色彩数为total
     if (isFind) return;
     if (id >= n) { isFind = true; return; }  //当所有节点都被着色后，返回
 
     for (int i = 1; i <= total; i++) {
         if (ok(id, i)) {
            color[id] = i;
            DFS(id+1, total);
            color[id] = 0;
         }
     }
     if (!isFind) {    //当用total种颜色无法完成时，则增加一种颜色进行着色
        ans++;
        DFS(id, total+1);
     }
}
 
int main()
{
    int i, j;
    char s[M];
 
    while (scanf ("%d", &n) && n) {
          getchar();
          memset (map, false, sizeof (map));
          memset (color, 0, sizeof (color));
          for (i = 0; i < n; i++) {
               gets(s);
               for (j = 2; s[j] != '\0'; j++)
                   map[s[0]-'A'][s[j]-'A'] = true;
          }
          isFind = false;
          ans = 1;
          DFS(0, 1);
          if (ans == 1)
              printf ("1 channel needed.\n");
          else printf ("%d channels needed.\n", ans);
    }
    return 0;
}
```
### [四色原理](https://blog.csdn.net/lyy289065406/article/details/6647986)
```cpp
/*四色定理*/
 
//Memory Time 
//184K   0MS 
 
#include<iostream>
using namespace std;
 
typedef class
{
	public:
		int next[27];  //直接后继
		int pn;   //next[]指针（后继个数）
}point;
 
int main(int i,int j,int k)
{
	int n;
	while(cin>>n)
	{
		if(!n)
			break;
 
		getchar();  //n的换行符
 
		point* node=new point[n+1];  //结点
 
		/*Structure the Map*/
 
		for(i=1;i<=n;i++)
		{
			getchar();  //结点序号
			getchar();  //冒号
 
			if(node[i].pn<0)   //初始化指针
				node[i].pn=0;
 
			char ch;
			while((ch=getchar())!='\n')
			{
				j=ch%('A'-1);   //把结点字母转换为相应的数字，如A->1  C->3
				node[i].next[ ++node[i].pn ]=j;
			}
		}
 
		int color[27]={0};  //color[i]为第i个结点当前染的颜色，0为无色（无染色）
		color[1]=1;  //结点A初始化染第1种色
		int maxcolor=1;  //当前已使用不同颜色的种数
 
		for(i=1;i<=n;i++)  //枚举每个顶点
		{
			color[i]=n+1;  //先假设结点i染最大的颜色
			bool vist[27]={false};  //标记第i种颜色是否在当前结点的相邻结点染过
			for(j=1;j<=node[i].pn;j++) //枚举顶点i的所有后继
			{
				int k=node[i].next[j];
				if(color[k])  //顶点i的第j个直接后继已染色
					vist[ color[k] ]=true;  //标记该种颜色
			}
			for(j=1;i<=n;j++)  //从最小的颜色开始，枚举每种颜色
				if(!vist[j] && color[i]>j) //注意染色的过程是一个不断调整的过程，可能会暂时出现大于4的颜色
				{                          //因此不能单纯枚举4种色，不然会WA
					color[i]=j;
					break;
				}
 
			if(maxcolor<color[i])
			{
				maxcolor=color[i];
				if(maxcolor==4)   //由四色定理知，最终完成染色后，图上最多只有四种颜色
					break;        //因此当染色过程出现结点的颜色为4时，就可以断定最少要用4种颜色染色
			}
		}
 
		if(maxcolor==1)
			cout<<1<<" channel needed."<<endl;
		else
			cout<<maxcolor<<" channels needed."<<endl;
 
		delete node;
	}
	return 0;
}
```

