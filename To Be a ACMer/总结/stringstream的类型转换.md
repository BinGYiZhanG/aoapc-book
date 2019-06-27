* char类型转换为String 类型:

```cpp
char c;
string str;
stringstream stream;
stream << c;
str = stream.str();
```

* string到int的转换
```cpp
string result = "10000";  
int n = 0;  
stream << result;  
stream >> n;  //n等于10000 
```
