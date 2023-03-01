# C++常用容器

## [vector](https://cplusplus.com/vector)

1、[emplace_bac`k()](https://cplusplus.com/reference/vector/vector/emplace_back/)：在vector 的末尾插入一个新元素

```c++
vector<int> myvector = {10,20,30};
myvector.emplace_back (100);
```

2、back()：访问vector末尾的一个元素

## [string](https://cplusplus.com/reference/string/string)

1、[substr()](https://cplusplus.com/reference/string/string/substr/)：从字符位置pos开始并跨越len个字符，而不是到索引为len的位置

```c++
std::string str="We think in generalities, but we live in details.";
std::string str2 = str.substr (3,5);     // "think"
std::size_t pos = str.find("live");      // position of "live" in str
std::string str3 = str.substr (pos);     // get from "live" to the end
```

2、[append()](https://cplusplus.com/reference/string/string/append/)：在当前字符串后追加一个字符串

```c++
//重载函数
string& append (const string& str);//追加一个字符串
string& append (const string& str, size_t subpos, size_t sublen);//追加一个子串
string& append (const char* s);//追加一个指针字符串
string& append (size_t n, char c);//追加n个字符c
```

3、strncpy()：复制字符串

```c++
char str1[]= "To be or not to be";
char str2[40];
char str3[40];
strncpy ( str2, str1, sizeof(str2) );//“To be or not to be”
strncpy ( str3, str2, 5 );//“To be”
str3[5] = '\0';   /* null character manually added */
```

3、substr(size_t pos , size_t len)：获得子字符串，[pos, pos + len]

```c++
std::string str="We think in generalities, but we live in details.";
                                           // (quoting Alfred N. Whitehead)
std::string str2 = str.substr (3,5);     // "think"
```



##  [queue](https://cplusplus.com/reference/queue/queue/?kw=queue)

1 、front()：得到队列的第一个元素

````c++
std::queue<int> myqueue;
myqueue.push(77);
myqueue.push(16);
myqueue.front() -= myqueue.back(); 
````

## [map](https://cplusplus.com/reference/map/map/)

1、at(key_type& k)：返回键为K的映射

```c++
  std::map<std::string,int> mymap = {
                { "alpha", 0 },
                { "beta", 0 },
                { "gamma", 0 } };

  mymap.at("alpha") = 10;
  mymap.at("beta") = 20;
  mymap.at("gamma") = 30;
  for (auto& x: mymap) {
    std::cout << x->first << ": " << x->second << '\n';
  }
```
### [unordered_map](https://cplusplus.com/reference/unordered_map/)

1、unordered_map的遍历

````c++
unordered_map<string, vector<int>> timemap;
for(auto &[name, list] : timemap) {
    ···
}
````

2、find(key_type& k)：在容器中搜索以*k*作为键的元素，如果找到则返回一个迭代器iterator，否则返回一个迭代器map.end()

```c++
unordered_map<string,double>::const_iterator got = mymap.find (input);

  if ( got == mymap.end() )
    std::cout << "not found";
  else
    std::cout << got->first << " is " << got->second;
    
```



## [set](https://cplusplus.com/reference/set/set/)

> Set是按照特定顺序（**有序**）存储**唯一元素**的容器

1、set的遍历，使用构造器**iterator**

```c++
for(set<int>::iterator it=numSet.begin() ;it!=numSet.end();it++)
{
    cout<<*it<<endl;
}
```

2、insert()：向set中插入数据，且保持**有序**，若已存在，则不插入

# C++常用库

## 算法库   *\#include\<algorithm\>*

### sort 
> sort(RandomAccessIterator first, RandomAccessIterator last)：对元素进行排序	//不能对map的键值对排序

```c++
bool myfunction (int i,int j) { return (i<j); }

struct myclass {
  bool operator() (int i,int j) { return (i<j);}
} myobject;

  int myints[] = {32,71,12,45,26,80,53,33};
  std::vector<int> myvector (myints, myints+8);               // 32 71 12 45 26 80 53 33

  // using default comparison (operator <):
  std::sort (myvector.begin(), myvector.begin()+4);           //(12 32 45 71)26 80 53 33

  // using function as comp
  std::sort (myvector.begin()+4, myvector.end(), myfunction); // 12 32 45 71(26 33 53 80)

  // using object as comp
  std::sort (myvector.begin(), myvector.end(), myobject);     //(12 26 32 33 45 53 71 80)
```


### reverse
> reverse (BidirectionalIterator first, BidirectionalIterator last)：反转范围元素顺序 **[first, last)**

```c++
reverse(myvector.begin(),myvector.end())
```



## 处理字符数组 *\#include\<cstring\>*

> 字符数组，即c语言中的字符串 char *c;

### strcpy

>  strcpy ( char * destination, const char * source )：*将source* 指向的 C 字符串复制到*destination*指向的数组中

```c++
char str1[]="Sample string";
char str2[40];
strcpy (str2,str1);
```

