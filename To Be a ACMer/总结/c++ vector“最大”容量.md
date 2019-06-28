
[博客链接](https://blog.csdn.net/iceboy314159/article/details/80329979)
```cpp
#include <stdio.h>
#include <vector>
int main() {
	std::vector<double> v;
	printf("size:%d capacity:%d max_size:%lld\n",v.size(),v.capacity(),v.max_size());
	int last_capacity = -1;
	for (int i = 0; i < v.max_size(); ++i) {
		v.push_back(1.0*i);
		if (last_capacity!=v.capacity()) {
			printf("size:%10d capacity:%10d c/l:%d max_size:%lld\n",
				v.size(),v.capacity(),v.capacity()/last_capacity,v.max_size());
		}
		last_capacity = v.capacity();
	}
	return 0;
}

```
![](https://github.com/BinGYiZhanG/aoapc-book/blob/master/To%20Be%20a%20ACMer/Images/17270628.png)

结论:<br>
 1,vector的最大容量max_size是4798784676560895，这个值不变，这个“最大”只是逻辑上的，也就是这个类型逻辑上支持vector的最大长度<br>
**注:** 程序继续运行下去，在重新向操作系统申请内存时会报错<br>
 2,vector的capacity,是指当前状态下（未重新向操作系统申请内存前）的最大容量。这个值如果不指定，则开始是0，加入第一个值时，由于capacity不够，向操作系统申请了长度为1的内存。在这之后每次capacity不足时，都会重新向操作系统申请长度为原来两倍的内存。<br>
**注:** 由此也可以得出结论，最佳方法是vector创建时，就指定一个capacity，无法预知大小没关系，先设一个值，总比0好。这样避免频繁的realloc操作，提高程序效率
