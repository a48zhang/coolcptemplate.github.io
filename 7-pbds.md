# 7-pb_ds

## 解锁

```cpp
#include <bits/extc++.h>
using namespace __gnu_pbds;
```

如果爆了：

```cpp
#include<ext/pb_ds/assoc_container.hpp>
#include<ext/pb_ds/tree_policy.hpp> // tree
#include<ext/pb_ds/hash_policy.hpp> // hash
#include<ext/pb_ds/trie_policy.hpp> // trie
#include<ext/pb_ds/priority_queue.hpp> // priority_queue
using namespace __gnu_pbds;
```

使用 `priority_queue` 小心与 `std` 产生冲突。

## `hash_table`

```cpp
cc_hash_table<int,bool> h; //拉链法
gp_hash_table<int,bool> h; //探测法
```

探测法可能快一些。使用同 `map`。复杂度 $O(n)$。

远快于 `unordered_map`

## `priority_queue`

```cpp
template < typename Value_Type ,
typename Cmp_Fn = std :: less < Value_Type >,
typename Tag = pairing_heap_tag ,
typename Allocator = std :: allocator <char > >
class priority_queue
```

### Tag
* pairing_heap_tag 配对堆
* binomial_heap_tag 二项堆
* rc_binomial_heap_tag 冗余计数二项堆
* binary_heap_tag 二叉堆
* thin_heap_tag 类似斐波那契堆


**支持堆的合并**

### Tree

```cpp
__gnu_pbds::tree<T,__gnu_pbds::null_type,less<T>,__gnu_pbds::rb_tree_tag,__gnu_pbds::tree_order_statistics_node_update>st;
```

如果你用不着 `order_by_key` 等，可以这样构造：

```cpp
__gnu_pbds::tree<T,__gnu_pbds::null_type>st;
```

实现类似 `std::map` 的，只需要把上面两个中的 `__gnu_pbds::null_type` 改成你想映射成的类型即可。

使用（成员函数）
类似 std::set 但比它强大。

迭代器

begin 返回第一个迭代器，即最“小”元素的迭代器。

end 返回最后一个迭代器的后一个位置的迭代器。

类似地有 rbegin 和 rend，但是和 hash_table 一样没有 cbegin 和 cend。

容量

empty 返回是否为空。

size 返回容器大小。

max_size 返回理论最大值。

修改器

clear 清空容器，返回 void()。

insert 插入一个数，返回 pair<iterator,bool>，表示所在迭代器和插入是否成功。

erase 擦除一个数或迭代器，返回一个 bool 表示是否成功。

查找

find 找寻一个数，返回该数的迭代器，找不到则返回 end。

lower_bound 返回指向首个不小于给定键的元素的迭代器，找不到则返回 end。

upper_bound 返回指向首个不小于给定键的元素的迭代器，找不到则返回 end。

order_of_key(x) 返回 x 以比较的排名，排名定义为比 x “小”的数的数量。

find_by_order(x) 返回的排名 x 所对应元素的迭代器，排名定义为比一个数“小”的数的数量。

合并与分裂

join(x) 将 x 树并入当前树，前提是两棵树的类型一样，x 树被清空，返回 void()。前提是两棵树各自的最大值和最小值构成的区间不交，否则抛出 join_error 的逻辑错误（logic_error）并结束程序。而这前提在算竞中很难做到，故一般使用启发式合并来代替。

split(x,b)“小于等于” x 的属于当前树，其余的属于 b 树，返回 void()。

迭代器和容量部分时间复杂度为 O(1)，其余除了 clear 为 O(size) 外全为 O(log size)。