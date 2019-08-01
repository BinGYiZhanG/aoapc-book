### udebug使用:

控制台输出的内容输出到txt文件
```cpp
#include <iostream>
#include <fstream>
#include <string>
using namespace std;

int main()
{
	//string ifile = "text.txt";
	//ifstream in(ifile);
	//ofstream out;
	ofstream out("text.txt");
	if (!out)	return 0;
	out << "OK" << endl;
	out.close();
    cout << "Hello World!\n";
}
```
会再创建一个与```.cpp```同名的文件夹，在该文件夹下，会有```txt```文件
