[toc]

# STL六大部件

容器，分配器，算法，迭代器，适配器，仿函数

![image.png](https://note.youdao.com/yws/res/22354/WEBRESOURCE47afefbe77de41f2951e4e8ad2fe0ed6)

# STL结构

## 前闭后开区间

![image.png](https://note.youdao.com/yws/res/22358/WEBRESOURCE63cc9a7b89b5c416df3590672d3101bd)

1. `begin()`指向第一个元素，`end()`指向最后一个元素的下一个元素
2. 迭代器类型`Container<T>::iterator`

![image.png](https://note.youdao.com/yws/res/22369/WEBRESOURCE7109ebc4059111ac2f2c4840645f7494)

3. `map`中有`key`和`value`，`set`中`key`就是`value`，`value`也就是`key`
4. `map`中元素的`key`不能重复，`set`中放的元素不能重复
5. `multimap`中元素的`key`能重复，`multiset`中放的元素能重复

# 容器简介（顺序容器 and 关联式容器）

## `array`

### 特性

1. 无开销的随机访问
2. 快速遍历；适合于线性搜索
3. 大小必须是一个常数表达式（=在编译时已知）
4. 不支持改变大小的操作（调整大小，插入，擦除，...）
5. 如果元素类型有很高的复制/分配成本，可能会很慢（重新排序的元素需要复制/移动它们）

### 结构

![image.png](https://note.youdao.com/yws/res/23304/WEBRESOURCE61d0fbfa37f32bf0996da70787623a84)

## `vector`

![image.png](https://note.youdao.com/yws/res/23804/WEBRESOURCEe2decfa59e764d8d99237e45cd218aa6)

### 特性

1. 无开销的随机访问
2. 快速遍历；适合于线性搜索
3. 以恒定时间在末端插入
4. 如果在前面和/或随机位置的插入/擦除操作占主导地位，可能会很慢
5. 如果元素类型有很高的复制/分配成本，可能会很慢（重新排序的元素需要复制/移动它们）
6. 所有可以改变容量的操作（插入、推回......）都可能使任何`vector`元素的引用/指针失效

> 什么意思？

>> 改变容量，会在另外一个地方开辟这个空间，然后将元素挪过去

7. 对于非常多的值来说，可能会有很长的分配时间

### 结构

![image.png](https://note.youdao.com/yws/res/23801/WEBRESOURCEcb0422136304cbb329caef7efbb578e2)
![image.png](https://note.youdao.com/yws/res/23322/WEBRESOURCE966de34e8c5ba60f862eee8190a178c8)

> `resize()`改变大小指元素，而不是容量

### 迭代器范围

![image.png](https://note.youdao.com/yws/res/23332/WEBRESOURCE0d7dc80c8875ab1260aab2082e412bfa)

> 范围末尾的迭代器指向的是最后一个元素的下一个元素（后面）

### 插入元素

![image.png](https://note.youdao.com/yws/res/23338/WEBRESOURCE10e28e4fd1b4fbd039234cbdbda20e70)

### 就地插入和构建元素

![image.png](https://note.youdao.com/yws/res/23344/WEBRESOURCE3862a79f5d04467f733b0e223f98e37d)

> `emplace_back`是通过创建临时对象，然后到容器的末尾吗？

>>`v.emplace_back(9, 7)`使用了`emplace_back`函数，该函数在容器的末尾直接构造元素，而不是先创建临时对象然后再移动或复制它,通过调用`explicit p2d(int x_, int y_)`构造函数来直接在容器中构造一个新的`p2d`对象是合法的,而不是进行隐式转换，再插入到末尾 

### 擦除元素

![image.png](https://note.youdao.com/yws/res/23366/WEBRESOURCE3ba0b8a7bb47edd65ca2168d7dbd8b57)

> 擦除不影响容量，也就是说，没有一个`vector`的内存被释放

### 注意`insert`/`erase`后的迭代器

> 如果一个`vector`的容量被改变，那么迭代器会失效（因为换地方存储了）

![image.png](https://note.youdao.com/yws/res/23382/WEBRESOURCE1d0ca3e2167f51d88789b02a4967e63a)

![image.png](https://note.youdao.com/yws/res/23377/WEBRESOURCE3605067e4c1b089770b52d95501a33f3)

## `list`

![](https://hackingcpp.com/cpp/std/list.png)

### 特性

1. 重组操作不需要移动/复制元素（适合于存储具有高复制/分配成本的大型对象）
2. 恒定时间拼接（完整列表的）
3. 仅在线性时间内进行随机访问
4. 由于内存位置不好，所以遍历速度慢


### 结构

![image.png](https://note.youdao.com/yws/res/23390/WEBRESOURCEd620f31d8112b37bacd84ca4f2430426)

### 构造

![image.png](https://note.youdao.com/yws/res/23395/WEBRESOURCE85260b37a6ebcebfaf55b842c620dcd5)

### `assign`分配：新内容分配给现有列表

![image.png](https://note.youdao.com/yws/res/23398/WEBRESOURCE13145fc80df1b00eeeead5c2a6a7525f)

![image.png](https://note.youdao.com/yws/res/23404/WEBRESOURCE20a927eec547eb1f46c862616a82ec80)

> 注意不是在原地方直接代替

### 获取元素的值

![image.png](https://note.youdao.com/yws/res/23409/WEBRESOURCE6748bc35e16b289b380ff306ee547216)

### 改变大小

![image.png](https://note.youdao.com/yws/res/23414/WEBRESOURCE798a0350cc4bfcfe7ea9d87f37a2603e)

### 添加/插入元素

![image.png](https://note.youdao.com/yws/res/23420/WEBRESOURCEaad4ef270aa84c1c5940f559e7514e13)

> 插入构造元素，不需要复制/移动

![image.png](https://note.youdao.com/yws/res/23429/WEBRESOURCEae9810c1075e524e7a26e0a8e502ae31)

### |连接|/|合并已经排序好的列表|

![image.png](https://note.youdao.com/yws/res/23434/WEBRESOURCE76ccda2cf1453f3ee51311dda22b1dd7)

> `1.splice 2`，将元素挂在1上，2去除连接的部分

### 迭代器

![image.png](https://note.youdao.com/yws/res/23445/WEBRESOURCE4a9901d797686efe25c7137bcc4319f5)

> 注意此时迭代器不能和`vector`一样直接用`c.begin()+1`，而需要用`next()`，因为不是连续分布的

> 代码使用`rbegin()`函数获取逆向迭代器，它指向列表中的最后一个元素。通过调用`base()`函数，将逆向迭代器转换为正向迭代器

> `next`参数默认为1

![image.png](https://note.youdao.com/yws/res/23466/WEBRESOURCEcc9262e4ccf8aafe5f070e502845c570)

### 排序

![image.png](https://note.youdao.com/yws/res/23457/WEBRESOURCEe64988e4d3fc8a620160046b7f0df691)

### 清除

![image.png](https://note.youdao.com/yws/res/23461/WEBRESOURCE390a7b15cb9860a4bac9bcb3deae98f6)

## `forward_list`

![image.png](https://note.youdao.com/yws/res/23806/WEBRESOURCE40fd403276749e83348e165e99b9e5b3)

### 特性

1. 使用的内存比`list`少
2. 重组操作不需要移动/复制元素（适合于存储具有高复制/分配成本的大型对象）
3. 恒定时间拼接（完整列表的）
4. 仅在线性时间内随机访问
5. 由于内存位置不好，所以遍历速度慢
6. 只可能进行前向遍历
7. 由于只有前向链接，界面有些繁琐

```
no:size(),back(),push_back(),pop_back(),insert()
```

![image.png](https://note.youdao.com/yws/res/23739/WEBRESOURCEac50ae2e17e501704130af0b8ec0fe81)
![image.png](https://note.youdao.com/yws/res/23741/WEBRESOURCE4f2b5595296bae4156ef5d494b4dfe39)

> 注意`after`和`front`

### 构造

![image.png](https://note.youdao.com/yws/res/23745/WEBRESOURCE547929b11d28a82fc274f31b4e916c16)

### `assign`

![image.png](https://note.youdao.com/yws/res/23752/WEBRESOURCE951d51fdc607a0a5b91c8d850cfba5a9)

### `access`

![image.png](https://note.youdao.com/yws/res/23755/WEBRESOURCEc318b74cdcc1ecb5594077103e7303d8)

![image.png](https://note.youdao.com/yws/res/23759/WEBRESOURCE6dd849a57d6b55a38f74b5ce4e0d5c7f)

### `insert`

![image.png](https://note.youdao.com/yws/res/23763/WEBRESOURCE0cef99b2cc045ffe0aaa8f596067d546)

### `splice`

![image.png](https://note.youdao.com/yws/res/23768/WEBRESOURCE585268323d51b1ab6248958859373147)

### `Iterators`

![image.png](https://note.youdao.com/yws/res/23778/WEBRESOURCEa82ef4514d816ec94dc57b0b7615baa0)

### `operate elements`

![image.png](https://note.youdao.com/yws/res/23783/WEBRESOURCE8100d13b2754e791b322eaa40776ba63)

### `erase`

![image.png](https://note.youdao.com/yws/res/23785/WEBRESOURCE1c04f6fcab0d30f4447196ac48889e0b)

![image.png](https://note.youdao.com/yws/res/23787/WEBRESOURCEdef398a1381e9593cb19e937536c74d2)

## `deque`

![image.png](https://note.youdao.com/yws/res/23808/WEBRESOURCEfdd61e095fd5559bbe8217321836aa6f)

### `特性`

1. 恒定时间随机访问（开销极小）
2. 快速遍历；适合于线性搜索
3. 在两端都有良好的插入和删除性能
4. 插入时不会使元素的引用/指针失效(存储分段连续，实现让用户看起来整体连续)
5. 如果元素类型有很高的复制/分配成本，可能会很慢
6. 对于大量的值来说，可能会有很长的分配时间

![image.png](https://note.youdao.com/yws/res/23810/WEBRESOURCE590cf14f8cc003aa506e225928f7039a)
![image.png](https://note.youdao.com/yws/res/23812/WEBRESOURCE2fce0ac8a28961e7e7d116d9e1d32fc9)

### 内存分布

![image.png](https://note.youdao.com/yws/res/23828/WEBRESOURCE2e10c49030b91ea6a25598236a98d905)

> 动态分配，连续的小块

### 构造

![image.png](https://note.youdao.com/yws/res/23815/WEBRESOURCEefa723dd4ea16a1857fcf1739a2f5e18)

### `Assign`

![image.png](https://note.youdao.com/yws/res/23820/WEBRESOURCE4c8f393bca84c6e6a7ac218e1af6b693)

### `operate values`

![image.png](https://note.youdao.com/yws/res/23824/WEBRESOURCEfab0203ef5f434241e576f6b7a4fef8c)

![image.png](https://note.youdao.com/yws/res/23833/WEBRESOURCE72920f7c91a168ac2bbc401d07bf689f)

### `size`

![image.png](https://note.youdao.com/yws/res/23836/WEBRESOURCEb2e929de3edc7781f8e8ad3571fe695e)

### `insert`

![image.png](https://note.youdao.com/yws/res/23839/WEBRESOURCE8e91564aac20f3a865fe20c3757810db)

### `iterators`

![image.png](https://note.youdao.com/yws/res/23844/WEBRESOURCEf8a7f937e616c378c6c306b80194d574)

### `erase`

![image.png](https://note.youdao.com/yws/res/23848/WEBRESOURCEd0f85308e0d8b365aa2b98707fd54cde)

## `set`/`map`

标准库中的关联容器是以节点为基础的，这些节点由指针连接。

![image.png](https://note.youdao.com/yws/res/24030/WEBRESOURCEb672359b175c77ce64feb4b88533b1e3)

> 键或键值对被存储在由指针连接的节点中

### `set`/`unordered_set`

#### 结构

![image.png](https://note.youdao.com/yws/res/23998/WEBRESOURCEb0e3a13e6f85d2ecb1c06985b067a038)

> `set`的`key`和`value`相同

> `set`红黑树结构，`unordered_set`哈希表结构

> `set`有序，`unordered_set`无序

![image.png](https://note.youdao.com/yws/res/24006/WEBRESOURCE60b0db66f0eb9dd719c857e6cf1eeb77)

> `set`元素不重复，当插入重复元素时，`reject`;`multiset`元素可重复

### `map`/`unordered_map`

#### 结构

![image.png](https://note.youdao.com/yws/res/24016/WEBRESOURCEd608903701e49a10f0a93d8e3a05bbbc)

![image.png](https://note.youdao.com/yws/res/24018/WEBRESOURCE90713ac129a6e59be8266907de6c6340)

![image.png](https://note.youdao.com/yws/res/24020/WEBRESOURCE19902c36c776330a593db7610b84bbe9)

> `map`的`key`和`value`不同，判断元素是否相同看`key`

> `map`红黑树结构，`unordered_map`哈希表结构

> `map`有序，`unordered_map`无序

> `map`元素不重复，当插入重复元素时，`reject`;`multimap`元素可重复


### 创建

![image.png](https://note.youdao.com/yws/res/24036/WEBRESOURCEaeccdb73f4e1c99abc4fe83514b2b85a)

> 比如` std::map<int, value> map{ {1,"abc"},{2,"sss"},{3,"xx"} };`，则会调用`value`的构造函数，再调用拷贝函数生成副本，赋给map


### `insert`

#### `for set`

![image.png](https://note.youdao.com/yws/res/24039/WEBRESOURCE84f6214f7f2d1e3185ef47ae3aff0daa)

![image.png](https://note.youdao.com/yws/res/24041/WEBRESOURCE3be2e16df03df1158ff1d6fdc4abb824)

#### `for map`

![image.png](https://note.youdao.com/yws/res/24047/WEBRESOURCE3ffcf901eaed3d3ae2632e4e5b9d6553)

![image.png](https://note.youdao.com/yws/res/24055/WEBRESOURCEea89c10fac4d1bdd8db6d06272facd77)

![image.png](https://note.youdao.com/yws/res/24057/WEBRESOURCEba3f296d9c40369783fb1fc12e8946fa)

> 复制/移动键值对到`map`中。如果你的`key`和/或`value`类型的复制很昂贵，请使用`emplace`（原地构造，不需要复制移动）

### `find/access/count  keys`

![image.png](https://note.youdao.com/yws/res/24067/WEBRESOURCEf8ce2764a961d5f6c49a1928ddd50e5e)

![image.png](https://note.youdao.com/yws/res/24069/WEBRESOURCE48cce3c1bf2d27ea1d4e612dff514f61)

### `iterate elements`

> 不可能通过迭代器或基于范围的for循环来修改键，因为这可能破坏容器的不变性（键的排序或在哈希表中的位置）

![image.png](https://note.youdao.com/yws/res/24078/WEBRESOURCE283d2ebd86dcd315626f35256dba5c5b)


> 图片有误!!

`for(auto key : s1)`复制开销大，而`for(auto const& key : s2)`复制开销小。
推荐使用`for(auto&& [key, value] : map){}`!

```c
#include <cstdio>
#include <map>
#include <string>

struct value
{
    std::string data;

    value()
    {
        printf("call default constructor\n");
    }
    value(const char* s)
        :data(s)
    {
        printf("call constructor from const char*\n");
    }
    value(const value& v)
        :data(v.data)
    {
        printf("call copy constructor\n");
    }
    value(value&& v)noexcept
        :data(std::move(v.data))
    {
        printf("call move constructor\n");
    }
    value& operator = (const value& v)
    {
        printf("call copy assignment operator\n");

        if (&v == this)return *this;
        data = v.data;
        return *this;
    }
    value& operator = (value&& v)noexcept
    {
        printf("call move assignment operator\n");

        data = std::move(v.data);
        return *this;
    }
};

int main()
{
    std::map<int, value> map{ {1,"abc"},{2,"sss"},{3,"xx"} };

    printf("\nUsing auto const& [key, value]:\n");
    for (auto const& [key, value] : map) {
        printf("%d:%s\n", key, value.data.c_str());
    }

    printf("\nUsing auto [key, value]:\n");
    for (auto [key, value] : map) {
        printf("%d:%s\n", key, value.data.c_str());
    }

    printf("\nUsing auto&& [key, value]:\n");
    for (auto&& [key, value] : map) {
        printf("%d:%s\n", key, value.data.c_str());
    }
}
```

- 结果

![image.png](https://note.youdao.com/yws/res/24240/WEBRESOURCE94e7b817d91649f20bc63e11f72d0407)

> 分析

`std::map<int, value> map{ {1,"abc"},{2,"sss"},{3,"xx"} };`，会调用`value`的构造函数，再调用拷贝函数生成副本，赋给map

关于`auto &&[key,value]`，这种情况实际就是引用

遍历数组不会触发移动构造函数

![image.png](https://note.youdao.com/yws/res/24098/WEBRESOURCEa9e5796883e557623b58f685d33a9022)

![image.png](https://note.youdao.com/yws/res/24100/WEBRESOURCEf391e64f44435b6f88ed0e5f3fdd8733)

### `get range of equivalent keys`

![image.png](https://note.youdao.com/yws/res/24111/WEBRESOURCE4d49265a40792e1bee268b51c38883fa)

### `get Upper/Lower Key Bound Positions`

![image.png](https://note.youdao.com/yws/res/24122/WEBRESOURCE979d0acb28997c17fd9228b3ce89cc59)

![image.png](https://note.youdao.com/yws/res/24124/WEBRESOURCE771d207e2b9bdf63ad3994e3b0e06874)

### `get size/empty`

![image.png](https://note.youdao.com/yws/res/24132/WEBRESOURCEc70fcf2fe2f222f2eefda2a242a7054b)

### `erase`

![image.png](https://note.youdao.com/yws/res/24137/WEBRESOURCE469a26ec701bc8487a8bcf5428c13a69)

### `extract && (Re-)insert Nodes`

![image.png](https://note.youdao.com/yws/res/24147/WEBRESOURCE59dad8aa310934fec6c860f90cf03551)

### `copy and assign`

![image.png](https://note.youdao.com/yws/res/24152/WEBRESOURCEcdc0a8096977ed1977484cb2042a7e7e)

### `compare Entire Sets/maps`

![image.png](https://note.youdao.com/yws/res/24163/WEBRESOURCE06ed9e3fcd45829ac9c6995ca9550362)

> 根据字典序比较的规则，比较两个集合时会逐个比较元素，直到找到第一个不相等的元素为止。如果在这个位置上，左边的元素小于右边的元素，则认为左边的集合小于右边的集合；如果左边的元素大于右边的元素，则认为左边的集合大于右边的集合

### `merge`

![image.png](https://note.youdao.com/yws/res/24168/WEBRESOURCE926a26cc4bd6fcec3837d12f91185194)

### `inspect/control Hash Table`

![image.png](https://note.youdao.com/yws/res/24179/WEBRESOURCE50708cc94eb094286eb8c4c1dad2db98)

![image.png](https://note.youdao.com/yws/res/24181/WEBRESOURCE9a7dd21e2683e2d52adfbb64d2d96097)

### `get types`

![image.png](https://note.youdao.com/yws/res/24186/WEBRESOURCEfab2411bcbf6f7db29d1d76c77542388)

### 总结

![](https://hackingcpp.com/cpp/std/set.png)

![](https://hackingcpp.com/cpp/std/map.png)

![](https://hackingcpp.com/cpp/std/unordered_set.png)

![](https://hackingcpp.com/cpp/std/unordered_map.png)

1. `map`和`set`都是非重复元素，如果放进去为重复的，则会放入失败，`reject`
2. `multimap`和`multiset`可以是重复元素
3. `set`的`key`和`value`一样，`map`的`key`和`value`不同，比较放入的是否相同是比较`key`
4. `map`和`unordered_map`可以用`c[i] = "xx"`的方式，而`multimap`和`multiset`不能，`multimap`需要用`c.insert(pair<long, string>(i, buf));`方式，`multiset`需要用`c.insert(buf)`方式
5. `map`/`set`/`multimap`/`multiset`结构是红黑树，`unordered_map`/`unordered_set`结构是哈希表
6. `map`不能用`std::find()`，只能用容器内置的`c.find()`，`set`都可以使用


## `push`和`emplace`的区别

`push_back()`函数接受一个已存在的对象作为参数，并将其副本添加到容器的末尾。如果你希望将一个已经存在的对象添加到容器中，可以使用`push_back()`。它会创建一个对象的副本，并将副本添加到容器中。

``emplace_back()`函数接受参数列表，并在容器的末尾就地构造一个新对象。这意味着你可以直接传递构造对象所需的参数，而不必先创建一个临时对象。`emplace_back()`通过在容器内部就地构造对象，避免了复制或移动对象的开销，因此在性能上可能更高效。

# 容器测试（顺序容器 and 关联式容器）

## `array`

```c
#include <array>
#include <iostream>
#include <ctime> 
#include <cstdlib> //qsort, bsearch, NULL

using namespace std;

const long ASIZE = 50000L;
//-----------------
long get_a_target_long()
{
	long target = 0;

	cout << "target (0~" << RAND_MAX << "): ";
	cin >> target;
	return target;
}

int compareLongs(const void* a, const void* b)
{
	return (*(long*)a - *(long*)b);
}
//---------------------------------------------------

void test_array()
{
	cout << "\ntest_array().......... \n";

	array<long, ASIZE> c;

	clock_t timeStart = clock();
	for (long i = 0; i < ASIZE; ++i) {
		c[i] = rand();
	}
	cout << "milli-seconds : " << (clock() - timeStart) << endl;	//
	cout << "array.size()= " << c.size() << endl;
	cout << "array.front()= " << c.front() << endl;
	cout << "array.back()= " << c.back() << endl;
	cout << "array.data()= " << c.data() << endl;

	long target = get_a_target_long();

	timeStart = clock();
	::qsort(c.data(), ASIZE, sizeof(long), compareLongs);
	long* pItem = (long*)::bsearch(&target, (c.data()), ASIZE, sizeof(long), compareLongs);
	cout << "qsort()+bsearch(), milli-seconds : " << (clock() - timeStart) << endl;	//    
	if (pItem != NULL)
		cout << "found, " << *pItem <<"addr = "<< pItem << endl;
	else
		cout << "not found! " << endl;
}


int main() {
	test_array();
}
```

- 结果

![image.png](https://note.youdao.com/yws/res/22389/WEBRESOURCEfa043b0f4fd435a1e6cbb24ffb49ff0a)


## `vector`

1. `::find()`表示是全局的，想表明所有的算法都是全局的模板函数
2. `vector`可以扩展，扩展方式是2倍扩展，但是是在另外一个地方找2倍空间，然后搬过去

```c
#include <vector>
#include <stdexcept>
#include <string>
#include <cstdlib> //abort()
#include <cstdio>  //snprintf()
#include <iostream>
#include <ctime> 
#include <algorithm> 	//sort()
#include <typeinfo>

using namespace std;

class MyString {
public:
	static size_t DCtor;  	//累計 default-ctor 的呼叫次數 
	static size_t Ctor;  	//累計 ctor      的呼叫次數 
	static size_t CCtor;  	//累計 copy-ctor 的呼叫次數 
	static size_t CAsgn;  	//累計 copy-asgn 的呼叫次數 
	static size_t MCtor;  	//累計 move-ctor 的呼叫次數 
	static size_t MAsgn;  	//累計 move-asgn 的呼叫次數 		    
	static size_t Dtor;	//累計 dtor 的呼叫次數 
private:
	char* _data;
	size_t _len;
	void _init_data(const char* s) {
		_data = new char[_len + 1];
		memcpy(_data, s, _len);
		_data[_len] = '\0';
	}
public:
	//default ctor
	MyString() : _data(NULL), _len(0) { ++DCtor; }

	//ctor
	MyString(const char* p) : _len(strlen(p)) {
		++Ctor;
		_init_data(p);
	}

	// copy ctor
	MyString(const MyString& str) : _len(str._len) {
		++CCtor;
		_init_data(str._data); 	//COPY
	}

	//move ctor, with "noexcept"
	MyString(MyString&& str) noexcept : _data(str._data), _len(str._len) {
		++MCtor;
		str._len = 0;
		str._data = NULL;  	//避免 delete (in dtor) 
	}

	//copy assignment
	MyString& operator=(const MyString& str) {
		++CAsgn;
		if (this != &str) {
			if (_data) delete _data;
			_len = str._len;
			_init_data(str._data); 	//COPY! 
		}
		else {
			// Self Assignment, Nothing to do.   
		}
		return *this;
	}

	//move assignment
	MyString& operator=(MyString&& str) noexcept {
		++MAsgn;
		if (this != &str) {
			if (_data) delete _data;
			_len = str._len;
			_data = str._data;	//MOVE!
			str._len = 0;
			str._data = NULL; 	//避免 deleted in dtor 
		}
		return *this;
	}

	//dtor
	virtual ~MyString() {
		++Dtor;
		if (_data) {
			delete _data;
		}
	}

	bool
		operator<(const MyString& rhs) const	//為了讓 set 比較大小  
	{
		return std::string(this->_data) < std::string(rhs._data); 	//借用事實：string 已能比較大小. 
	}
	bool
		operator==(const MyString& rhs) const	//為了讓 set 判斷相等. 
	{
		return std::string(this->_data) == std::string(rhs._data); 	//借用事實：string 已能判斷相等. 
	}

	char* get() const { return _data; }
};

size_t MyString::DCtor = 0;
size_t MyString::Ctor = 0;
size_t MyString::CCtor = 0;
size_t MyString::CAsgn = 0;
size_t MyString::MCtor = 0;
size_t MyString::MAsgn = 0;
size_t MyString::Dtor = 0;

class MyStrNoMove {
public:
	static size_t DCtor;  	//累計 default-ctor 的呼叫次數 
	static size_t Ctor;  	//累計 ctor      的呼叫次數 
	static size_t CCtor;  	//累計 copy-ctor 的呼叫次數 
	static size_t CAsgn;  	//累計 copy-asgn 的呼叫次數 
	static size_t MCtor;  	//累計 move-ctor 的呼叫次數 
	static size_t MAsgn;  	//累計 move-asgn 的呼叫次數 		    
	static size_t Dtor;	    //累計 dtor 的呼叫次數 
private:
	char* _data;
	size_t _len;
	void _init_data(const char* s) {
		_data = new char[_len + 1];
		memcpy(_data, s, _len);
		_data[_len] = '\0';
	}
public:
	//default ctor
	MyStrNoMove() : _data(NULL), _len(0) { ++DCtor; _init_data("jjhou"); }

	//ctor
	MyStrNoMove(const char* p) : _len(strlen(p)) {
		++Ctor;  _init_data(p);
	}

	// copy ctor
	MyStrNoMove(const MyStrNoMove& str) : _len(str._len) {
		++CCtor;
		_init_data(str._data); 	//COPY
	}

	//copy assignment
	MyStrNoMove& operator=(const MyStrNoMove& str) {
		++CAsgn;

		if (this != &str) {
			if (_data) delete _data;
			_len = str._len;
			_init_data(str._data); 	//COPY! 
		}
		else {
			// Self Assignment, Nothing to do.   
		}
		return *this;
	}

	//dtor
	virtual ~MyStrNoMove() {
		++Dtor;
		if (_data) {
			delete _data;
		}
	}

	bool
		operator<(const MyStrNoMove& rhs) const		//為了讓 set 比較大小 
	{
		return string(this->_data) < string(rhs._data);  //借用事實：string 已能比較大小. 
	}

	bool
		operator==(const MyStrNoMove& rhs) const	//為了讓 set 判斷相等. 
	{
		return string(this->_data) == string(rhs._data);  //借用事實：string 已能判斷相等. 
	}

	char* get() const { return _data; }
};

size_t MyStrNoMove::DCtor = 0;
size_t MyStrNoMove::Ctor = 0;
size_t MyStrNoMove::CCtor = 0;
size_t MyStrNoMove::CAsgn = 0;
size_t MyStrNoMove::MCtor = 0;
size_t MyStrNoMove::MAsgn = 0;
size_t MyStrNoMove::Dtor = 0;

template<typename T>
void output_static_data(const T& myStr)
{
	cout << typeid(myStr).name() << " -- " << endl;
	cout << " CCtor=" << T::CCtor
		<< " MCtor=" << T::MCtor
		<< " CAsgn=" << T::CAsgn
		<< " MAsgn=" << T::MAsgn
		<< " Dtor=" << T::Dtor
		<< " Ctor=" << T::Ctor
		<< " DCtor=" << T::DCtor
		<< endl;
}


template<typename M, typename NM>
void test_moveable(M c1, NM c2, long& value)
{
	char buf[10];

	//測試 move 
	cout << "\n\ntest, with moveable elements" << endl;
	typedef typename iterator_traits<typename M::iterator>::value_type  V1type;
	clock_t timeStart = clock();
	for (long i = 0; i < value; ++i)
	{
		snprintf(buf, 10, "%d", rand());
		auto ite = c1.end();
		c1.insert(ite, V1type(buf));
	}
	cout << "construction, milli-seconds : " << (clock() - timeStart) << endl;
	cout << "size()= " << c1.size() << endl;
	output_static_data(*(c1.begin()));

	timeStart = clock();
	M c11(c1);
	cout << "copy, milli-seconds : " << (clock() - timeStart) << endl;

	timeStart = clock();
	M c12(std::move(c1));
	cout << "move copy, milli-seconds : " << (clock() - timeStart) << endl;

	timeStart = clock();
	c11.swap(c12);
	cout << "swap, milli-seconds : " << (clock() - timeStart) << endl;



	//測試 non-moveable 	
	cout << "\n\ntest, with non-moveable elements" << endl;
	typedef typename iterator_traits<typename NM::iterator>::value_type  V2type;
	timeStart = clock();
	for (long i = 0; i < value; ++i)
	{
		snprintf(buf, 10, "%d", rand());
		auto ite = c2.end();
		c2.insert(ite, V2type(buf));
	}

	cout << "construction, milli-seconds : " << (clock() - timeStart) << endl;
	cout << "size()= " << c2.size() << endl;
	output_static_data(*(c2.begin()));

	timeStart = clock();
	NM c21(c2);
	cout << "copy, milli-seconds : " << (clock() - timeStart) << endl;

	timeStart = clock();
	NM c22(std::move(c2));
	cout << "move copy, milli-seconds : " << (clock() - timeStart) << endl;

	timeStart = clock();
	c21.swap(c22);
	cout << "swap, milli-seconds : " << (clock() - timeStart) << endl;
}

string get_a_target_string()
{
	long target = 0;
	char buf[10];

	cout << "target (0~" << RAND_MAX << "): ";
	cin >> target;
	snprintf(buf, 10, "%d", target);
	return string(buf);
}

int compareStrings(const void* a, const void* b)
{
	if (*(string*)a > *(string*)b)
		return 1;
	else if (*(string*)a < *(string*)b)
		return -1;
	else
		return 0;
}

namespace jj02
{
	void test_vector(long& value)
	{
		cout << "\ntest_vector().......... \n";

		vector<string> c;
		char buf[10];

		clock_t timeStart = clock();
		for (long i = 0; i < value; ++i)
		{
			try {
				snprintf(buf, 10, "%d", rand());
				c.push_back(string(buf));
			}
			catch (exception& p) {
				cout << "i=" << i << " " << p.what() << endl;
				//曾經最高 i=58389486 then std::bad_alloc
				abort();
			}
		}
		cout << "milli-seconds : " << (clock() - timeStart) << endl;
		cout << "vector.max_size()= " << c.max_size() << endl;	//1073747823
		cout << "vector.size()= " << c.size() << endl;
		cout << "vector.front()= " << c.front() << endl;
		cout << "vector.back()= " << c.back() << endl;
		cout << "vector.data()= " << c.data() << endl;
		cout << "vector.capacity()= " << c.capacity() << endl << endl;


		string target = get_a_target_string();
		{
			timeStart = clock();
			auto pItem = find(c.begin(), c.end(), target);
			cout << "std::find(), milli-seconds : " << (clock() - timeStart) << endl;

			if (pItem != c.end())
				cout << "found, " << *pItem << endl << endl;
			else
				cout << "not found! " << endl << endl;
		}

		{
			timeStart = clock();
			sort(c.begin(), c.end());
			cout << "sort(), milli-seconds : " << (clock() - timeStart) << endl;

			timeStart = clock();
			string* pItem = (string*)::bsearch(&target, (c.data()),
				c.size(), sizeof(string), compareStrings);
			cout << "bsearch(), milli-seconds : " << (clock() - timeStart) << endl;

			if (pItem != NULL)
				cout << "found, " << *pItem << endl << endl;
			else
				cout << "not found! " << endl << endl;
		}

		c.clear();
		test_moveable(vector<MyString>(), vector<MyStrNoMove>(), value);
	}
}

int main() {
	cout << "put value!" << endl;
	long value;
	cin >> value;
	jj02::test_vector(value);
}
```

- 结果

![image.png](https://note.youdao.com/yws/res/22408/WEBRESOURCEf7d162c6916207c109f44afdbc4a9514)
![image.png](https://note.youdao.com/yws/res/22406/WEBRESOURCE724ee734ecab114b9e1557b010e71e24)

## `list`

1. 每放一个元素，就在空间中找到一个节点的大小
2. 一个结点一个结点扩充

```c
#include <list>
#include <stdexcept>
#include <string>
#include <cstdlib> //abort()
#include <cstdio>  //snprintf()
#include <algorithm> //find()
#include <iostream>
#include <ctime> 

using namespace std;

//以下 MyString 是為了測試 containers with moveable elements 效果.  
class MyString {
public:
	static size_t DCtor;  	//累計 default-ctor 的呼叫次數 
	static size_t Ctor;  	//累計 ctor      的呼叫次數 
	static size_t CCtor;  	//累計 copy-ctor 的呼叫次數 
	static size_t CAsgn;  	//累計 copy-asgn 的呼叫次數 
	static size_t MCtor;  	//累計 move-ctor 的呼叫次數 
	static size_t MAsgn;  	//累計 move-asgn 的呼叫次數 		    
	static size_t Dtor;	//累計 dtor 的呼叫次數 
private:
	char* _data;
	size_t _len;
	void _init_data(const char* s) {
		_data = new char[_len + 1];
		memcpy(_data, s, _len);
		_data[_len] = '\0';
	}
public:
	//default ctor
	MyString() : _data(NULL), _len(0) { ++DCtor; }

	//ctor
	MyString(const char* p) : _len(strlen(p)) {
		++Ctor;
		_init_data(p);
	}

	// copy ctor
	MyString(const MyString& str) : _len(str._len) {
		++CCtor;
		_init_data(str._data); 	//COPY
	}

	//move ctor, with "noexcept"
	MyString(MyString&& str) noexcept : _data(str._data), _len(str._len) {
		++MCtor;
		str._len = 0;
		str._data = NULL;  	//避免 delete (in dtor) 
	}

	//copy assignment
	MyString& operator=(const MyString& str) {
		++CAsgn;
		if (this != &str) {
			if (_data) delete _data;
			_len = str._len;
			_init_data(str._data); 	//COPY! 
		}
		else {
			// Self Assignment, Nothing to do.   
		}
		return *this;
	}

	//move assignment
	MyString& operator=(MyString&& str) noexcept {
		++MAsgn;
		if (this != &str) {
			if (_data) delete _data;
			_len = str._len;
			_data = str._data;	//MOVE!
			str._len = 0;
			str._data = NULL; 	//避免 deleted in dtor 
		}
		return *this;
	}

	//dtor
	virtual ~MyString() {
		++Dtor;
		if (_data) {
			delete _data;
		}
	}

	bool
		operator<(const MyString& rhs) const	//為了讓 set 比較大小  
	{
		return std::string(this->_data) < std::string(rhs._data); 	//借用事實：string 已能比較大小. 
	}
	bool
		operator==(const MyString& rhs) const	//為了讓 set 判斷相等. 
	{
		return std::string(this->_data) == std::string(rhs._data); 	//借用事實：string 已能判斷相等. 
	}

	char* get() const { return _data; }
};
size_t MyString::DCtor = 0;
size_t MyString::Ctor = 0;
size_t MyString::CCtor = 0;
size_t MyString::CAsgn = 0;
size_t MyString::MCtor = 0;
size_t MyString::MAsgn = 0;
size_t MyString::Dtor = 0;

class MyStrNoMove {
public:
	static size_t DCtor;  	//累計 default-ctor 的呼叫次數 
	static size_t Ctor;  	//累計 ctor      的呼叫次數 
	static size_t CCtor;  	//累計 copy-ctor 的呼叫次數 
	static size_t CAsgn;  	//累計 copy-asgn 的呼叫次數 
	static size_t MCtor;  	//累計 move-ctor 的呼叫次數 
	static size_t MAsgn;  	//累計 move-asgn 的呼叫次數 		    
	static size_t Dtor;	    //累計 dtor 的呼叫次數 
private:
	char* _data;
	size_t _len;
	void _init_data(const char* s) {
		_data = new char[_len + 1];
		memcpy(_data, s, _len);
		_data[_len] = '\0';
	}
public:
	//default ctor
	MyStrNoMove() : _data(NULL), _len(0) { ++DCtor; _init_data("jjhou"); }

	//ctor
	MyStrNoMove(const char* p) : _len(strlen(p)) {
		++Ctor;  _init_data(p);
	}

	// copy ctor
	MyStrNoMove(const MyStrNoMove& str) : _len(str._len) {
		++CCtor;
		_init_data(str._data); 	//COPY
	}

	//copy assignment
	MyStrNoMove& operator=(const MyStrNoMove& str) {
		++CAsgn;

		if (this != &str) {
			if (_data) delete _data;
			_len = str._len;
			_init_data(str._data); 	//COPY! 
		}
		else {
			// Self Assignment, Nothing to do.   
		}
		return *this;
	}

	//dtor
	virtual ~MyStrNoMove() {
		++Dtor;
		if (_data) {
			delete _data;
		}
	}

	bool
		operator<(const MyStrNoMove& rhs) const		//為了讓 set 比較大小 
	{
		return string(this->_data) < string(rhs._data);  //借用事實：string 已能比較大小. 
	}

	bool
		operator==(const MyStrNoMove& rhs) const	//為了讓 set 判斷相等. 
	{
		return string(this->_data) == string(rhs._data);  //借用事實：string 已能判斷相等. 
	}

	char* get() const { return _data; }
};
size_t MyStrNoMove::DCtor = 0;
size_t MyStrNoMove::Ctor = 0;
size_t MyStrNoMove::CCtor = 0;
size_t MyStrNoMove::CAsgn = 0;
size_t MyStrNoMove::MCtor = 0;
size_t MyStrNoMove::MAsgn = 0;
size_t MyStrNoMove::Dtor = 0;

string get_a_target_string()
{
	long target = 0;
	char buf[10];

	cout << "target (0~" << RAND_MAX << "): ";
	cin >> target;
	snprintf(buf, 10, "%d", target);
	return string(buf);
}

template<typename T>
void output_static_data(const T& myStr)
{
	cout << typeid(myStr).name() << " -- " << endl;
	cout << " CCtor=" << T::CCtor
		<< " MCtor=" << T::MCtor
		<< " CAsgn=" << T::CAsgn
		<< " MAsgn=" << T::MAsgn
		<< " Dtor=" << T::Dtor
		<< " Ctor=" << T::Ctor
		<< " DCtor=" << T::DCtor
		<< endl;
}


template<typename M, typename NM>
void test_moveable(M c1, NM c2, long& value)
{
	char buf[10];

	//測試 move 
	cout << "\n\ntest, with moveable elements" << endl;
	typedef typename iterator_traits<typename M::iterator>::value_type  V1type;
	clock_t timeStart = clock();
	for (long i = 0; i < value; ++i)
	{
		snprintf(buf, 10, "%d", rand());
		auto ite = c1.end();
		c1.insert(ite, V1type(buf));
	}
	cout << "construction, milli-seconds : " << (clock() - timeStart) << endl;
	cout << "size()= " << c1.size() << endl;
	output_static_data(*(c1.begin()));

	timeStart = clock();
	M c11(c1);
	cout << "copy, milli-seconds : " << (clock() - timeStart) << endl;

	timeStart = clock();
	M c12(std::move(c1));
	cout << "move copy, milli-seconds : " << (clock() - timeStart) << endl;

	timeStart = clock();
	c11.swap(c12);
	cout << "swap, milli-seconds : " << (clock() - timeStart) << endl;



	//測試 non-moveable 	
	cout << "\n\ntest, with non-moveable elements" << endl;
	typedef typename iterator_traits<typename NM::iterator>::value_type  V2type;
	timeStart = clock();
	for (long i = 0; i < value; ++i)
	{
		snprintf(buf, 10, "%d", rand());
		auto ite = c2.end();
		c2.insert(ite, V2type(buf));
	}

	cout << "construction, milli-seconds : " << (clock() - timeStart) << endl;
	cout << "size()= " << c2.size() << endl;
	output_static_data(*(c2.begin()));

	timeStart = clock();
	NM c21(c2);
	cout << "copy, milli-seconds : " << (clock() - timeStart) << endl;

	timeStart = clock();
	NM c22(std::move(c2));
	cout << "move copy, milli-seconds : " << (clock() - timeStart) << endl;

	timeStart = clock();
	c21.swap(c22);
	cout << "swap, milli-seconds : " << (clock() - timeStart) << endl;
}

void test_list(long& value)
{
	cout << "\ntest_list().......... \n";

	list<string> c;
	char buf[10];

	clock_t timeStart = clock();
	for (long i = 0; i < value; ++i)
	{
		try {
			snprintf(buf, 10, "%d", rand());
			c.push_back(string(buf));
		}
		catch (exception& p) {
			cout << "i=" << i << " " << p.what() << endl;
			abort();
		}
	}
	cout << "milli-seconds : " << (clock() - timeStart) << endl;
	cout << "list.size()= " << c.size() << endl;
	cout << "list.max_size()= " << c.max_size() << endl;    //357913941
	cout << "list.front()= " << c.front() << endl;
	cout << "list.back()= " << c.back() << endl;

	string target = get_a_target_string();
	timeStart = clock();
	auto pItem = find(c.begin(), c.end(), target);
	cout << "std::find(), milli-seconds : " << (clock() - timeStart) << endl;

	if (pItem != c.end())
		cout << "found, " << *pItem << endl;
	else
		cout << "not found! " << endl;

	timeStart = clock();
	c.sort();
	cout << "c.sort(), milli-seconds : " << (clock() - timeStart) << endl;

	c.clear();
	test_moveable(list<MyString>(), list<MyStrNoMove>(), value);
}

int main() {
	long value;
	cout << "Please enter value:" << endl;
	cin >> value;
	test_list(value);
}
```


- 结果

![image.png](https://note.youdao.com/yws/res/23286/WEBRESOURCEb5fd9a3ec7288694e75146f57fa3118a)

![image.png](https://note.youdao.com/yws/res/23284/WEBRESOURCE3a408451440f45cbdb6a1e88d58ffe97)

## `forward_list`

```c
#include <stdexcept>
#include <string>
#include <cstdlib> //abort()
#include <cstdio>  //snprintf()
#include <algorithm> //find()
#include <iostream>
#include <ctime> 
#include <forward_list>

void test_forward_list(long& value)
{
	cout << "\ntest_forward_list().......... \n";

	forward_list<string> c;
	char buf[10];

	clock_t timeStart = clock();
	for (long i = 0; i < value; ++i)
	{
		try {
			snprintf(buf, 10, "%d", rand());
			c.push_front(string(buf));
		}
		catch (exception& p) {
			cout << "i=" << i << " " << p.what() << endl;
			abort();
		}
	}
	cout << "milli-seconds : " << (clock() - timeStart) << endl;
	cout << "forward_list.max_size()= " << c.max_size() << endl;  //536870911
	cout << "forward_list.front()= " << c.front() << endl;


	string target = get_a_target_string();
	timeStart = clock();
	auto pItem = find(c.begin(), c.end(), target);
	cout << "std::find(), milli-seconds : " << (clock() - timeStart) << endl;

	if (pItem != c.end())
		cout << "found, " << *pItem << endl;
	else
		cout << "not found! " << endl;

	timeStart = clock();
	c.sort();
	cout << "c.sort(), milli-seconds : " << (clock() - timeStart) << endl;

	c.clear();
	//test_moveable(forward_list<MyString>(), forward_list<MyStrNoMove>(), value);//无该操作，因为`forward_list`没有函数内的`insert`,`size`操作
}

int main() {
	long value;
	cout << "Please enter value:" << endl;
	cin >> value;
	test_forward_list(value);
}
```

![image.png](https://note.youdao.com/yws/res/23683/WEBRESOURCE23f42772550dffd32c0d63a143ac720e)


## `deque`

1. 可以扩充，而且两边都能扩充，结构分段连续，但是让使用者感觉是整个连续的

![image.png](https://note.youdao.com/yws/res/23694/WEBRESOURCEcee06410b71441e36810d5e3275de205)

```c
#include <deque>
#include <stdexcept>
#include <string>
#include <cstdlib> //abort()
#include <cstdio>  //snprintf()
#include <iostream>
#include <ctime> 
#include <algorithm>

using namespace std;

//以下 MyString 是為了測試 containers with moveable elements 效果.  
class MyString {
public:
	static size_t DCtor;  	//累計 default-ctor 的呼叫次數 
	static size_t Ctor;  	//累計 ctor      的呼叫次數 
	static size_t CCtor;  	//累計 copy-ctor 的呼叫次數 
	static size_t CAsgn;  	//累計 copy-asgn 的呼叫次數 
	static size_t MCtor;  	//累計 move-ctor 的呼叫次數 
	static size_t MAsgn;  	//累計 move-asgn 的呼叫次數 		    
	static size_t Dtor;	//累計 dtor 的呼叫次數 
private:
	char* _data;
	size_t _len;
	void _init_data(const char* s) {
		_data = new char[_len + 1];
		memcpy(_data, s, _len);
		_data[_len] = '\0';
	}
public:
	//default ctor
	MyString() : _data(NULL), _len(0) { ++DCtor; }

	//ctor
	MyString(const char* p) : _len(strlen(p)) {
		++Ctor;
		_init_data(p);
	}

	// copy ctor
	MyString(const MyString& str) : _len(str._len) {
		++CCtor;
		_init_data(str._data); 	//COPY
	}

	//move ctor, with "noexcept"
	MyString(MyString&& str) noexcept : _data(str._data), _len(str._len) {
		++MCtor;
		str._len = 0;
		str._data = NULL;  	//避免 delete (in dtor) 
	}

	//copy assignment
	MyString& operator=(const MyString& str) {
		++CAsgn;
		if (this != &str) {
			if (_data) delete _data;
			_len = str._len;
			_init_data(str._data); 	//COPY! 
		}
		else {
			// Self Assignment, Nothing to do.   
		}
		return *this;
	}

	//move assignment
	MyString& operator=(MyString&& str) noexcept {
		++MAsgn;
		if (this != &str) {
			if (_data) delete _data;
			_len = str._len;
			_data = str._data;	//MOVE!
			str._len = 0;
			str._data = NULL; 	//避免 deleted in dtor 
		}
		return *this;
	}

	//dtor
	virtual ~MyString() {
		++Dtor;
		if (_data) {
			delete _data;
		}
	}

	bool
		operator<(const MyString& rhs) const	//為了讓 set 比較大小  
	{
		return std::string(this->_data) < std::string(rhs._data); 	//借用事實：string 已能比較大小. 
	}
	bool
		operator==(const MyString& rhs) const	//為了讓 set 判斷相等. 
	{
		return std::string(this->_data) == std::string(rhs._data); 	//借用事實：string 已能判斷相等. 
	}

	char* get() const { return _data; }
};
size_t MyString::DCtor = 0;
size_t MyString::Ctor = 0;
size_t MyString::CCtor = 0;
size_t MyString::CAsgn = 0;
size_t MyString::MCtor = 0;
size_t MyString::MAsgn = 0;
size_t MyString::Dtor = 0;

class MyStrNoMove {
public:
	static size_t DCtor;  	//累計 default-ctor 的呼叫次數 
	static size_t Ctor;  	//累計 ctor      的呼叫次數 
	static size_t CCtor;  	//累計 copy-ctor 的呼叫次數 
	static size_t CAsgn;  	//累計 copy-asgn 的呼叫次數 
	static size_t MCtor;  	//累計 move-ctor 的呼叫次數 
	static size_t MAsgn;  	//累計 move-asgn 的呼叫次數 		    
	static size_t Dtor;	    //累計 dtor 的呼叫次數 
private:
	char* _data;
	size_t _len;
	void _init_data(const char* s) {
		_data = new char[_len + 1];
		memcpy(_data, s, _len);
		_data[_len] = '\0';
	}
public:
	//default ctor
	MyStrNoMove() : _data(NULL), _len(0) { ++DCtor; _init_data("jjhou"); }

	//ctor
	MyStrNoMove(const char* p) : _len(strlen(p)) {
		++Ctor;  _init_data(p);
	}

	// copy ctor
	MyStrNoMove(const MyStrNoMove& str) : _len(str._len) {
		++CCtor;
		_init_data(str._data); 	//COPY
	}

	//copy assignment
	MyStrNoMove& operator=(const MyStrNoMove& str) {
		++CAsgn;

		if (this != &str) {
			if (_data) delete _data;
			_len = str._len;
			_init_data(str._data); 	//COPY! 
		}
		else {
			// Self Assignment, Nothing to do.   
		}
		return *this;
	}

	//dtor
	virtual ~MyStrNoMove() {
		++Dtor;
		if (_data) {
			delete _data;
		}
	}

	bool
		operator<(const MyStrNoMove& rhs) const		//為了讓 set 比較大小 
	{
		return string(this->_data) < string(rhs._data);  //借用事實：string 已能比較大小. 
	}

	bool
		operator==(const MyStrNoMove& rhs) const	//為了讓 set 判斷相等. 
	{
		return string(this->_data) == string(rhs._data);  //借用事實：string 已能判斷相等. 
	}

	char* get() const { return _data; }
};
size_t MyStrNoMove::DCtor = 0;
size_t MyStrNoMove::Ctor = 0;
size_t MyStrNoMove::CCtor = 0;
size_t MyStrNoMove::CAsgn = 0;
size_t MyStrNoMove::MCtor = 0;
size_t MyStrNoMove::MAsgn = 0;
size_t MyStrNoMove::Dtor = 0;

string get_a_target_string()
{
	long target = 0;
	char buf[10];

	cout << "target (0~" << RAND_MAX << "): ";
	cin >> target;
	snprintf(buf, 10, "%d", target);
	return string(buf);
}

template<typename T>
void output_static_data(const T& myStr)
{
	cout << typeid(myStr).name() << " -- " << endl;
	cout << " CCtor=" << T::CCtor
		<< " MCtor=" << T::MCtor
		<< " CAsgn=" << T::CAsgn
		<< " MAsgn=" << T::MAsgn
		<< " Dtor=" << T::Dtor
		<< " Ctor=" << T::Ctor
		<< " DCtor=" << T::DCtor
		<< endl;
}


template<typename M, typename NM>
void test_moveable(M c1, NM c2, long& value)
{
	char buf[10];

	//測試 move 
	cout << "\n\ntest, with moveable elements" << endl;
	typedef typename iterator_traits<typename M::iterator>::value_type  V1type;
	clock_t timeStart = clock();
	for (long i = 0; i < value; ++i)
	{
		snprintf(buf, 10, "%d", rand());
		auto ite = c1.end();
		c1.insert(ite, V1type(buf));
	}
	cout << "construction, milli-seconds : " << (clock() - timeStart) << endl;
	cout << "size()= " << c1.size() << endl;
	output_static_data(*(c1.begin()));

	timeStart = clock();
	M c11(c1);
	cout << "copy, milli-seconds : " << (clock() - timeStart) << endl;

	timeStart = clock();
	M c12(std::move(c1));
	cout << "move copy, milli-seconds : " << (clock() - timeStart) << endl;

	timeStart = clock();
	c11.swap(c12);
	cout << "swap, milli-seconds : " << (clock() - timeStart) << endl;



	//測試 non-moveable 	
	cout << "\n\ntest, with non-moveable elements" << endl;
	typedef typename iterator_traits<typename NM::iterator>::value_type  V2type;
	timeStart = clock();
	for (long i = 0; i < value; ++i)
	{
		snprintf(buf, 10, "%d", rand());
		auto ite = c2.end();
		c2.insert(ite, V2type(buf));
	}

	cout << "construction, milli-seconds : " << (clock() - timeStart) << endl;
	cout << "size()= " << c2.size() << endl;
	output_static_data(*(c2.begin()));

	timeStart = clock();
	NM c21(c2);
	cout << "copy, milli-seconds : " << (clock() - timeStart) << endl;

	timeStart = clock();
	NM c22(std::move(c2));
	cout << "move copy, milli-seconds : " << (clock() - timeStart) << endl;

	timeStart = clock();
	c21.swap(c22);
	cout << "swap, milli-seconds : " << (clock() - timeStart) << endl;
}

void test_deque(long& value)
{
	cout << "\ntest_deque().......... \n";

	deque<string> c;
	char buf[10];

	clock_t timeStart = clock();
	for (long i = 0; i < value; ++i)
	{
		try {
			snprintf(buf, 10, "%d", rand());
			c.push_back(string(buf));
		}
		catch (exception& p) {
			cout << "i=" << i << " " << p.what() << endl;
			abort();
		}
	}
	cout << "milli-seconds : " << (clock() - timeStart) << endl;
	cout << "deque.size()= " << c.size() << endl;
	cout << "deque.front()= " << c.front() << endl;
	cout << "deque.back()= " << c.back() << endl;
	cout << "deque.max_size()= " << c.max_size() << endl;	//1073741821	

	string target = get_a_target_string();
	timeStart = clock();
	auto pItem = find(c.begin(), c.end(), target);
	cout << "std::find(), milli-seconds : " << (clock() - timeStart) << endl;

	if (pItem != c.end())
		cout << "found, " << *pItem << endl;
	else
		cout << "not found! " << endl;

	timeStart = clock();
	::sort(c.begin(), c.end());
	cout << "sort(), milli-seconds : " << (clock() - timeStart) << endl;

	c.clear();
	test_moveable(deque<MyString>(), deque<MyStrNoMove>(), value);
}

int main() {
	long value;
	cout << "Please enter value:" << endl;
	cin >> value;
	test_deque(value);
}
```

![image.png](https://note.youdao.com/yws/res/23701/WEBRESOURCE5ebed6c6300e9ecd8982789684a9b0b4)

![image.png](https://note.youdao.com/yws/res/23703/WEBRESOURCE5907b26a34dfc60fbafb70e6a2d1fe37)

## `stack`

> 不提供`iterator`,不然会破坏原有的性质

![image.png](https://note.youdao.com/yws/res/23720/WEBRESOURCEece2379f7b3f68d2a19e1b35aa5c8f62)

## `queue`

> 不提供`iterator`,不然会破坏原有的性质

![image.png](https://note.youdao.com/yws/res/23723/WEBRESOURCEee03c843ee8f2fe227ed390e2ef251da)


## `multiset`

1. 关联式容器，红黑树结构，`key`和`value`是同一个，可以放相同元素

```c
#include <set>
#include <stdexcept>
#include <string>
#include <cstdlib> //abort()
#include <cstdio>  //snprintf()
#include <iostream>
#include <ctime>


using namespace std;

//以下 MyString 是為了測試 containers with moveable elements 效果.  
class MyString {
public:
	static size_t DCtor;  	//累計 default-ctor 的呼叫次數 
	static size_t Ctor;  	//累計 ctor      的呼叫次數 
	static size_t CCtor;  	//累計 copy-ctor 的呼叫次數 
	static size_t CAsgn;  	//累計 copy-asgn 的呼叫次數 
	static size_t MCtor;  	//累計 move-ctor 的呼叫次數 
	static size_t MAsgn;  	//累計 move-asgn 的呼叫次數 		    
	static size_t Dtor;	//累計 dtor 的呼叫次數 
private:
	char* _data;
	size_t _len;
	void _init_data(const char* s) {
		_data = new char[_len + 1];
		memcpy(_data, s, _len);
		_data[_len] = '\0';
	}
public:
	//default ctor
	MyString() : _data(NULL), _len(0) { ++DCtor; }

	//ctor
	MyString(const char* p) : _len(strlen(p)) {
		++Ctor;
		_init_data(p);
	}

	// copy ctor
	MyString(const MyString& str) : _len(str._len) {
		++CCtor;
		_init_data(str._data); 	//COPY
	}

	//move ctor, with "noexcept"
	MyString(MyString&& str) noexcept : _data(str._data), _len(str._len) {
		++MCtor;
		str._len = 0;
		str._data = NULL;  	//避免 delete (in dtor) 
	}

	//copy assignment
	MyString& operator=(const MyString& str) {
		++CAsgn;
		if (this != &str) {
			if (_data) delete _data;
			_len = str._len;
			_init_data(str._data); 	//COPY! 
		}
		else {
			// Self Assignment, Nothing to do.   
		}
		return *this;
	}

	//move assignment
	MyString& operator=(MyString&& str) noexcept {
		++MAsgn;
		if (this != &str) {
			if (_data) delete _data;
			_len = str._len;
			_data = str._data;	//MOVE!
			str._len = 0;
			str._data = NULL; 	//避免 deleted in dtor 
		}
		return *this;
	}

	//dtor
	virtual ~MyString() {
		++Dtor;
		if (_data) {
			delete _data;
		}
	}

	bool
		operator<(const MyString& rhs) const	//為了讓 set 比較大小  
	{
		return std::string(this->_data) < std::string(rhs._data); 	//借用事實：string 已能比較大小. 
	}
	bool
		operator==(const MyString& rhs) const	//為了讓 set 判斷相等. 
	{
		return std::string(this->_data) == std::string(rhs._data); 	//借用事實：string 已能判斷相等. 
	}

	char* get() const { return _data; }
};
size_t MyString::DCtor = 0;
size_t MyString::Ctor = 0;
size_t MyString::CCtor = 0;
size_t MyString::CAsgn = 0;
size_t MyString::MCtor = 0;
size_t MyString::MAsgn = 0;
size_t MyString::Dtor = 0;

class MyStrNoMove {
public:
	static size_t DCtor;  	//累計 default-ctor 的呼叫次數 
	static size_t Ctor;  	//累計 ctor      的呼叫次數 
	static size_t CCtor;  	//累計 copy-ctor 的呼叫次數 
	static size_t CAsgn;  	//累計 copy-asgn 的呼叫次數 
	static size_t MCtor;  	//累計 move-ctor 的呼叫次數 
	static size_t MAsgn;  	//累計 move-asgn 的呼叫次數 		    
	static size_t Dtor;	    //累計 dtor 的呼叫次數 
private:
	char* _data;
	size_t _len;
	void _init_data(const char* s) {
		_data = new char[_len + 1];
		memcpy(_data, s, _len);
		_data[_len] = '\0';
	}
public:
	//default ctor
	MyStrNoMove() : _data(NULL), _len(0) { ++DCtor; _init_data("jjhou"); }

	//ctor
	MyStrNoMove(const char* p) : _len(strlen(p)) {
		++Ctor;  _init_data(p);
	}

	// copy ctor
	MyStrNoMove(const MyStrNoMove& str) : _len(str._len) {
		++CCtor;
		_init_data(str._data); 	//COPY
	}

	//copy assignment
	MyStrNoMove& operator=(const MyStrNoMove& str) {
		++CAsgn;

		if (this != &str) {
			if (_data) delete _data;
			_len = str._len;
			_init_data(str._data); 	//COPY! 
		}
		else {
			// Self Assignment, Nothing to do.   
		}
		return *this;
	}

	//dtor
	virtual ~MyStrNoMove() {
		++Dtor;
		if (_data) {
			delete _data;
		}
	}

	bool
		operator<(const MyStrNoMove& rhs) const		//為了讓 set 比較大小 
	{
		return string(this->_data) < string(rhs._data);  //借用事實：string 已能比較大小. 
	}

	bool
		operator==(const MyStrNoMove& rhs) const	//為了讓 set 判斷相等. 
	{
		return string(this->_data) == string(rhs._data);  //借用事實：string 已能判斷相等. 
	}

	char* get() const { return _data; }
};
size_t MyStrNoMove::DCtor = 0;
size_t MyStrNoMove::Ctor = 0;
size_t MyStrNoMove::CCtor = 0;
size_t MyStrNoMove::CAsgn = 0;
size_t MyStrNoMove::MCtor = 0;
size_t MyStrNoMove::MAsgn = 0;
size_t MyStrNoMove::Dtor = 0;


template<typename T>
void output_static_data(const T& myStr)
{
	cout << typeid(myStr).name() << " -- " << endl;
	cout << " CCtor=" << T::CCtor
		<< " MCtor=" << T::MCtor
		<< " CAsgn=" << T::CAsgn
		<< " MAsgn=" << T::MAsgn
		<< " Dtor=" << T::Dtor
		<< " Ctor=" << T::Ctor
		<< " DCtor=" << T::DCtor
		<< endl;
}


template<typename M, typename NM>
void test_moveable(M c1, NM c2, long& value)
{
	char buf[10];

	//測試 move 
	cout << "\n\ntest, with moveable elements" << endl;
	typedef typename iterator_traits<typename M::iterator>::value_type  V1type;
	clock_t timeStart = clock();
	for (long i = 0; i < value; ++i)
	{
		snprintf(buf, 10, "%d", rand());
		auto ite = c1.end();
		c1.insert(ite, V1type(buf));
	}
	cout << "construction, milli-seconds : " << (clock() - timeStart) << endl;
	cout << "size()= " << c1.size() << endl;
	output_static_data(*(c1.begin()));

	timeStart = clock();
	M c11(c1);
	cout << "copy, milli-seconds : " << (clock() - timeStart) << endl;

	timeStart = clock();
	M c12(std::move(c1));
	cout << "move copy, milli-seconds : " << (clock() - timeStart) << endl;

	timeStart = clock();
	c11.swap(c12);
	cout << "swap, milli-seconds : " << (clock() - timeStart) << endl;



	//測試 non-moveable 	
	cout << "\n\ntest, with non-moveable elements" << endl;
	typedef typename iterator_traits<typename NM::iterator>::value_type  V2type;
	timeStart = clock();
	for (long i = 0; i < value; ++i)
	{
		snprintf(buf, 10, "%d", rand());
		auto ite = c2.end();
		c2.insert(ite, V2type(buf));
	}

	cout << "construction, milli-seconds : " << (clock() - timeStart) << endl;
	cout << "size()= " << c2.size() << endl;
	output_static_data(*(c2.begin()));

	timeStart = clock();
	NM c21(c2);
	cout << "copy, milli-seconds : " << (clock() - timeStart) << endl;

	timeStart = clock();
	NM c22(std::move(c2));
	cout << "move copy, milli-seconds : " << (clock() - timeStart) << endl;

	timeStart = clock();
	c21.swap(c22);
	cout << "swap, milli-seconds : " << (clock() - timeStart) << endl;
}

string get_a_target_string()
{
	long target = 0;
	char buf[10];

	cout << "target (0~" << RAND_MAX << "): ";
	cin >> target;
	snprintf(buf, 10, "%d", target);
	return string(buf);
}

void test_multiset(long& value)
{
	cout << "\ntest_multiset().......... \n";

	multiset<string> c;
	char buf[10];
	clock_t timeStart = clock();
	for (long i = 0; i < value; ++i)
	{
		try {
			snprintf(buf, 10, "%d", rand());
			c.insert(string(buf));
		}
		catch (exception& p) {
			cout << "i=" << i << " " << p.what() << endl;
			abort();
		}
	}
	cout << "milli-seconds : " << (clock() - timeStart) << endl;
	cout << "multiset.size()= " << c.size() << endl;
	cout << "multiset.max_size()= " << c.max_size() << endl;	//214748364

	string target = get_a_target_string();
	{
		timeStart = clock();
		auto pItem = find(c.begin(), c.end(), target);	//比 c.find(...) 慢很多	
		cout << "std::find(), milli-seconds : " << (clock() - timeStart) << endl;
		if (pItem != c.end())
			cout << "found, " << *pItem << endl;
		else
			cout << "not found! " << endl;
	}

	{
		timeStart = clock();
		auto pItem = c.find(target);		//比 std::find(...) 快很多							
		cout << "c.find(), milli-seconds : " << (clock() - timeStart) << endl;
		if (pItem != c.end())
			cout << "found, " << *pItem << endl;
		else
			cout << "not found! " << endl;
	}

	c.clear();
	test_moveable(multiset<MyString>(), multiset<MyStrNoMove>(), value);
}


int main() {
	long value;
	cout << "Please enter value:" << endl;
	cin >> value;
	test_multiset(value);
}
```

- 结果

![image.png](https://note.youdao.com/yws/res/23873/WEBRESOURCE9018664197cacf3ef326330d64e9c729)

![image.png](https://note.youdao.com/yws/res/23875/WEBRESOURCE1bd6088ec808e225824f8a7efdd9098e)

> 查找元素快，构造元素慢

## `multimap`

1. 关联式容器，红黑树结构，分`key`和`value`，使用`key`来查找，可以放相同元素

```c
#include <map>
#include <stdexcept>
#include <string>
#include <cstdlib> //abort()
#include <cstdio>  //snprintf()
#include <iostream>
#include <ctime> 

using namespace std;

long get_a_target_long()
{
	long target = 0;

	cout << "target (0~" << RAND_MAX << "): ";
	cin >> target;
	return target;
}

void test_multimap(long& value)
{
	cout << "\ntest_multimap().......... \n";

	multimap<long, string> c;
	char buf[10];

	clock_t timeStart = clock();
	for (long i = 0; i < value; ++i)
	{
		try {
			snprintf(buf, 10, "%d", rand());
			//multimap 不可使用 [] 做 insertion 
			c.insert(pair<long, string>(i, buf));
		}
		catch (exception& p) {
			cout << "i=" << i << " " << p.what() << endl;
			abort();
		}
	}
	cout << "milli-seconds : " << (clock() - timeStart) << endl;
	cout << "multimap.size()= " << c.size() << endl;
	cout << "multimap.max_size()= " << c.max_size() << endl;	//178956970	

	long target = get_a_target_long();
	timeStart = clock();
	auto pItem = c.find(target);
	cout << "c.find(), milli-seconds : " << (clock() - timeStart) << endl;
	if (pItem != c.end())
		cout << "found, value=" << (*pItem).second << endl;
	else
		cout << "not found! " << endl;

	c.clear();
}


int main() {
	long value;
	cout << "Please enter value:" << endl;
	cin >> value;
	test_multimap(value);
}
```

- 结果

![image.png](https://note.youdao.com/yws/res/23881/WEBRESOURCEbc02ae98f25a67baea014a4abd5ae696)

> 查找元素快，构造元素慢

## `unordered_multiset`

1. 关联式容器，`hash_table`结构
2. 当元素的数量大于`bucket`（篮子）的数量，`bucket`数量变为2倍大小，元素打散重新挂在篮子上

```c
#include <unordered_set>
#include <stdexcept>
#include <string>
#include <cstdlib> //abort()
#include <cstdio>  //snprintf()
#include <iostream>
#include <ctime> 

using namespace std;

string get_a_target_string()
{
	long target = 0;
	char buf[10];

	cout << "target (0~" << RAND_MAX << "): ";
	cin >> target;
	snprintf(buf, 10, "%d", target);
	return string(buf);
}

void test_unordered_multiset(long& value)
{
	cout << "\ntest_unordered_multiset().......... \n";

	unordered_multiset<string> c;
	char buf[10];

	clock_t timeStart = clock();
	for (long i = 0; i < value; ++i)
	{
		try {
			snprintf(buf, 10, "%d", rand());
			c.insert(string(buf));
		}
		catch (exception& p) {
			cout << "i=" << i << " " << p.what() << endl;
			abort();
		}
	}
	cout << "milli-seconds : " << (clock() - timeStart) << endl;
	cout << "unordered_multiset.size()= " << c.size() << endl;
	cout << "unordered_multiset.max_size()= " << c.max_size() << endl;	//357913941
	cout << "unordered_multiset.bucket_count()= " << c.bucket_count() << endl;
	cout << "unordered_multiset.load_factor()= " << c.load_factor() << endl;
	cout << "unordered_multiset.max_load_factor()= " << c.max_load_factor() << endl;
	cout << "unordered_multiset.max_bucket_count()= " << c.max_bucket_count() << endl;
	for (unsigned i = 0; i < 20; ++i) {
		cout << "bucket #" << i << " has " << c.bucket_size(i) << " elements.\n";
	}

	string target = get_a_target_string();
	{
		timeStart = clock();
		auto pItem = find(c.begin(), c.end(), target);	//比 c.find(...) 慢很多	
		cout << "std::find(), milli-seconds : " << (clock() - timeStart) << endl;
		if (pItem != c.end())
			cout << "found, " << *pItem << endl;
		else
			cout << "not found! " << endl;
	}

	{
		timeStart = clock();
		auto pItem = c.find(target);		//比 std::find(...) 快很多							
		cout << "c.find(), milli-seconds : " << (clock() - timeStart) << endl;
		if (pItem != c.end())
			cout << "found, " << *pItem << endl;
		else
			cout << "not found! " << endl;
	}

	c.clear();
	//test_moveable(unordered_multiset<MyString>(), unordered_multiset<MyStrNoMove>(), value);
	//该函数不能调用，因为如果放入的不是常规类型，需要定义比较函数
}


int main() {
	long value;
	cout << "Please enter value:" << endl;
	cin >> value;
	test_unordered_multiset(value);
}
```

- 结果

![image.png](https://note.youdao.com/yws/res/23914/WEBRESOURCE616071c4df4e3f38d56941ac59348f3d)

![image.png](https://note.youdao.com/yws/res/23916/WEBRESOURCEee6b6b4299939075a396d7a2dc08275f)

## `unordered_multimap`

1. 关联式容器，`hash_table`结构
2. 当元素的数量大于`bucket`（篮子）的数量，`bucket`数量变为2倍大小，元素打散重新挂在篮子上

```c
#include <unordered_map>
#include <stdexcept>
#include <string>
#include <cstdlib> //abort()
#include <cstdio>  //snprintf()
#include <iostream>
#include <ctime> 

long get_a_target_long()
{
	long target = 0;

	cout << "target (0~" << RAND_MAX << "): ";
	cin >> target;
	return target;
}


void test_unordered_multimap(long& value)
{
	cout << "\ntest_unordered_multimap().......... \n";

	unordered_multimap<long, string> c;
	char buf[10];

	clock_t timeStart = clock();
	for (long i = 0; i < value; ++i)
	{
		try {
			snprintf(buf, 10, "%d", rand());
			//multimap 不可使用 [] 進行 insertion 
			c.insert(pair<long, string>(i, buf));
		}
		catch (exception& p) {
			cout << "i=" << i << " " << p.what() << endl;
			abort();
		}
	}
	cout << "milli-seconds : " << (clock() - timeStart) << endl;
	cout << "unordered_multimap.size()= " << c.size() << endl;
	cout << "unordered_multimap.max_size()= " << c.max_size() << endl;	//357913941	

	long target = get_a_target_long();
	timeStart = clock();
	auto pItem = c.find(target);
	cout << "c.find(), milli-seconds : " << (clock() - timeStart) << endl;
	if (pItem != c.end())
		cout << "found, value=" << (*pItem).second << endl;
	else
		cout << "not found! " << endl;
}


int main() {
	long value;
	cout << "Please enter value:" << endl;
	cin >> value;
	test_unordered_multimap(value);
}
```

- 结果

![image.png](https://note.youdao.com/yws/res/23907/WEBRESOURCEe27d9e84b672b904f1fcce661618327e)


## `set`

1. 关联式容器，红黑树，`value`和`key`相同，`key`不能重复
2. 如果放进去为重复的，则会放入失败，`reject`


```c
#include <set>
#include <stdexcept>
#include <string>
#include <cstdlib> //abort()
#include <cstdio>  //snprintf()
#include <iostream>
#include <ctime> 

string get_a_target_string()
{
	long target = 0;
	char buf[10];

	cout << "target (0~" << RAND_MAX << "): ";
	cin >> target;
	snprintf(buf, 10, "%d", target);
	return string(buf);
}

void test_set(long& value)
{
	cout << "\ntest_set().......... \n";

	set<string> c;
	char buf[10];

	clock_t timeStart = clock();
	for (long i = 0; i < value; ++i)
	{
		try {
			snprintf(buf, 10, "%d", rand());
			c.insert(string(buf));
		}
		catch (exception& p) {
			cout << "i=" << i << " " << p.what() << endl;
			abort();
		}
	}
	cout << "milli-seconds : " << (clock() - timeStart) << endl;
	cout << "set.size()= " << c.size() << endl;
	cout << "set.max_size()= " << c.max_size() << endl;	   //214748364

	string target = get_a_target_string();
	{
		timeStart = clock();
		auto pItem = find(c.begin(), c.end(), target);	//比 c.find(...) 慢很多	
		cout << "std::find(), milli-seconds : " << (clock() - timeStart) << endl;
		if (pItem != c.end())
			cout << "found, " << *pItem << endl;
		else
			cout << "not found! " << endl;
	}

	{
		timeStart = clock();
		auto pItem = c.find(target);		//比 std::find(...) 快很多							
		cout << "c.find(), milli-seconds : " << (clock() - timeStart) << endl;
		if (pItem != c.end())
			cout << "found, " << *pItem << endl;
		else
			cout << "not found! " << endl;
	}
}

int main() {
	long value;
	cout << "Please enter value:" << endl;
	cin >> value;
	test_set(value);
}
```

- 结果

![image.png](https://note.youdao.com/yws/res/23939/WEBRESOURCE3b5743ee3ec8c8875ab5ff91cbfea33a)

## `map`

1. `map`和`unordered_map`可以使用`c[i] = "xx"`方式，其中`i`为`key`，`"xx"`为`value`，容器会把`key`和`value`合成一个`pair`放到红黑树中

```c
#include <map>
#include <stdexcept>
#include <string>
#include <cstdlib> //abort()
#include <cstdio>  //snprintf()
#include <iostream>
#include <ctime> 

long get_a_target_long()
{
	long target = 0;

	cout << "target (0~" << RAND_MAX << "): ";
	cin >> target;
	return target;
}

void test_map(long& value)
{
	cout << "\ntest_map().......... \n";

	map<long, string> c;
	char buf[10];

	clock_t timeStart = clock();
	for (long i = 0; i < value; ++i)
	{
		try {
			snprintf(buf, 10, "%d", rand());
			c[i] = string(buf);
		}
		catch (exception& p) {
			cout << "i=" << i << " " << p.what() << endl;
			abort();
		}
	}
	cout << "milli-seconds : " << (clock() - timeStart) << endl;
	cout << "map.size()= " << c.size() << endl;
	cout << "map.max_size()= " << c.max_size() << endl;		//178956970

	long target = get_a_target_long();
	timeStart = clock();
	auto pItem = c.find(target);
	cout << "c.find(), milli-seconds : " << (clock() - timeStart) << endl;
	if (pItem != c.end())
		cout << "found, value=" << (*pItem).second << endl;
	else
		cout << "not found! " << endl;

	c.clear();
}

int main() {
	long value;
	cout << "Please enter value:" << endl;
	cin >> value;
	test_map(value);
}
```

- 结果

![image.png](https://note.youdao.com/yws/res/23943/WEBRESOURCE52221ddc3a6867cd34bb7e83821cdf17)

## `unordered_set`

1. 关联式容器，哈希表，`value`和`key`相同，`key`不能重复
2. 如果放进去为重复的，则会放入失败，`reject`

```c
#include <unordered_set>
#include <stdexcept>
#include <string>
#include <cstdlib> //abort()
#include <cstdio>  //snprintf()
#include <iostream>
#include <ctime> 

string get_a_target_string()
{
	long target = 0;
	char buf[10];

	cout << "target (0~" << RAND_MAX << "): ";
	cin >> target;
	snprintf(buf, 10, "%d", target);
	return string(buf);
}

void test_unordered_set(long& value)
{
	cout << "\ntest_unordered_set().......... \n";

	unordered_set<string> c;
	char buf[10];

	clock_t timeStart = clock();
	for (long i = 0; i < value; ++i)
	{
		try {
			snprintf(buf, 10, "%d", rand());
			c.insert(string(buf));
		}
		catch (exception& p) {
			cout << "i=" << i << " " << p.what() << endl;
			abort();
		}
	}
	cout << "milli-seconds : " << (clock() - timeStart) << endl;
	cout << "unordered_set.size()= " << c.size() << endl;
	cout << "unordered_set.max_size()= " << c.max_size() << endl;  //357913941
	cout << "unordered_set.bucket_count()= " << c.bucket_count() << endl;
	cout << "unordered_set.load_factor()= " << c.load_factor() << endl;
	cout << "unordered_set.max_load_factor()= " << c.max_load_factor() << endl;
	cout << "unordered_set.max_bucket_count()= " << c.max_bucket_count() << endl;
	for (unsigned i = 0; i < 20; ++i) {
		cout << "bucket #" << i << " has " << c.bucket_size(i) << " elements.\n";
	}

	string target = get_a_target_string();
	{
		timeStart = clock();
		auto pItem = find(c.begin(), c.end(), target);	//比 c.find(...) 慢很多	
		cout << "std::find(), milli-seconds : " << (clock() - timeStart) << endl;
		if (pItem != c.end())
			cout << "found, " << *pItem << endl;
		else
			cout << "not found! " << endl;
	}

	{
		timeStart = clock();
		auto pItem = c.find(target);		//比 std::find(...) 快很多							
		cout << "c.find(), milli-seconds : " << (clock() - timeStart) << endl;
		if (pItem != c.end())
			cout << "found, " << *pItem << endl;
		else
			cout << "not found! " << endl;
	}
}

int main() {
	long value;
	cout << "Please enter value:" << endl;
	cin >> value;
	test_unordered_set(value);
}
```

- 结果

![image.png](https://note.youdao.com/yws/res/23978/WEBRESOURCE90f652e4dddc96dcaf431d96dff15905)
![image.png](https://note.youdao.com/yws/res/23980/WEBRESOURCEa08490e9cdda181a8ad5d325475b209c)

## `unordered_map`

1. `map`和`unordered_map`可以使用`c[i] = "xx"`方式，其中`i`为`key`，`"xx"`为`value`，容器会把`key`和`value`合成一个`pair`放到红黑树中

```c
#include <unordered_map>
#include <stdexcept>
#include <string>
#include <cstdlib> //abort()
#include <cstdio>  //snprintf()
#include <iostream>
#include <ctime> 

long get_a_target_long()
{
	long target = 0;

	cout << "target (0~" << RAND_MAX << "): ";
	cin >> target;
	return target;
}

void test_unordered_map(long& value)
{
	cout << "\ntest_unordered_map().......... \n";

	unordered_map<long, string> c;
	char buf[10];

	clock_t timeStart = clock();
	for (long i = 0; i < value; ++i)
	{
		try {
			snprintf(buf, 10, "%d", rand());
			c[i] = string(buf);
		}
		catch (exception& p) {
			cout << "i=" << i << " " << p.what() << endl;
			abort();
		}
	}
	cout << "milli-seconds : " << (clock() - timeStart) << endl;
	cout << "unordered_map.size()= " << c.size() << endl;	//357913941
	cout << "unordered_map.max_size()= " << c.max_size() << endl;

	long target = get_a_target_long();
	timeStart = clock();
	//! auto pItem = find(c.begin(), c.end(), target);	//map 不適用 std::find() 			
	auto pItem = c.find(target);

	cout << "c.find(), milli-seconds : " << (clock() - timeStart) << endl;
	if (pItem != c.end())
		cout << "found, value=" << (*pItem).second << endl;
	else
		cout << "not found! " << endl;
}

int main() {
	long value;
	cout << "Please enter value:" << endl;
	cin >> value;
	test_unordered_map(value);
}
```

- 结果

![image.png](https://note.youdao.com/yws/res/23982/WEBRESOURCE36bf2a5ba1a1a1d6fa8fa47c85776a35)

## 总结

1. `map`和`set`都是非重复元素，如果放进去为重复的，则会放入失败，`reject`
2. `multimap`和`multiset`可以是重复元素
3. `set`的`key`和`value`一样，`map`的`key`和`value`不同，比较放入的是否相同是比较`key`
4. `map`和`unordered_map`可以用`c[i] = "xx"`的方式，而`multimap`和`multiset`不能，`multimap`需要用`c.insert(pair<long, string>(i, buf));`方式，`multiset`需要用`c.insert(buf)`方式
5. `map`/`set`/`multimap`/`multiset`结构是红黑树，`unordered_map`/`unordered_set`结构是哈希表
6. `map`不能用`std::find()`，只能用容器内置的`c.find()`，`set`都可以使用

# 分配器

<img src = "https://note.youdao.com/yws/res/24262/WEBRESOURCE0489941e32022f43c9e0aa8a168eeeaf" height = "300" />

- STL

1. `malloc`分配内存时，要附加额外的信息，所以实际内存要比`size`要大
2. `allocate` 调用- `Allocate` 调用- `operator new` 调用- `malloc`
3. `deallocate` 调用- `operator delete` 调用- `free`


- VC
<img src = "https://note.youdao.com/yws/res/24292/WEBRESOURCE12ae5d01881af869b766bc9b5c7dd6e2" height = "400" />

![image.png](https://note.youdao.com/yws/res/24287/WEBRESOURCE726e99ccb38255bef2282aaffa431bd4)

- GCC

![image.png](https://note.youdao.com/yws/res/24298/WEBRESOURCE9ef7a131fe244863722ac6a42ed10750)


# 常见容器操作总结

- `array`

结构：数组形式，固定大小

1. `front`:访问第一个元素
2. `back`:访问最后一个元素
3. `operator []`

- `vector`

结构：数组形式，从后面插入元素

1. `front`:访问第一个元素
2. `back`:访问最后一个元素
3. `operator []`
4. `push_back`:将元素添加到容器末尾
5. `pop_back`:移除末元素
6. `insert`:插入元素

- `list`

结构：链表连接，双向

1. `front`:访问第一个元素
2. `back`:访问最后一个元素
3. 没有`operator []`!
4. `push_back`:将元素添加到容器末尾
5. `pop_back`:移除末元素
6. `insert`:插入元素
7. `push_front`:插入元素到容器起始
8. `pop_front`:移除首元素

- `forward list`

结构：链表连接，单向，**从前面插入元素**

1. `front`:访问第一个元素
2. 没有`back`!
3. 没有`operator []`!
4. 没有`push_back`!
5. 没有`pop_back`!
6. `insert_after`:在某个元素后插入新元素
7. `push_front`:插入元素到容器起始
8. `pop_front`:移除首元素

- `deque`

结构：双端队列，允许在它的首尾两端快速插入及删除

1. `front`:访问第一个元素
2. `back`:访问最后一个元素
3. `operator []`
4. `push_back`:将元素添加到容器末尾
5. `pop_back`:移除末元素
6. `insert`:插入元素
7. `push_front`:插入元素到容器起始
8. `pop_front`:移除首元素

- `stack`

结构：栈，先进后出，栈顶操作

1. `top`:访问栈顶元素
2. `push`:向栈顶插入元素
3. `pop`:删除栈顶元素

- `queue`

结构：队列，先进先出

1. `front`:访问第一个元素
2. `back`:访问最后一个元素
2. `push`:向队列尾部插入元素
3. `pop`:删除首个元素

- `set`

结构：关联式容器，`key`==`value`，红黑树存储

1. `count`:返回匹配特定键的元素数量，有为`1`,没有为`0`

> 如果是`multiset`，则返回具体数量，因为`set`元素个数only one

2. `contains`:检查容器是否含有带特定键的元素
  

- `map`

结果：关联式容器，`key`和`value`区别，红黑树存储

1. `count`:返回匹配特定键的元素数量，有为`1`,没有为`0`
2. `operator[]`:访问或插入指定的元素
3. `contains`:检查容器是否含有带特定键的元素

> 如果是`multimap`，则返回具体数量，因为`map`元素个数only one














