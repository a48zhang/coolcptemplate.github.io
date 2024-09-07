# `pb_ds`

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

|                | pop                             | push                            | modify                        | join        | erase                         |
| -------------- | ------------------------------- | ------------------------------- | ----------------------------- | ----------- | ----------------------------- |
| 配对堆         | θ(1)                            | 最坏 θ(size) 均摊 θ(log size)   | 最坏 θ(size) 均摊 θ(log size) | θ(1)        | 最坏 θ(size) 均摊 θ(log size) |
| 二项堆         | 最坏 θ(log size) 均摊 θ(1)      | O(log size)                     | O(log size)                   | O(log size) | O(log size)                   |
| 冗余计数二项堆 | θ(1)                            | O(log size)                     | O(log size)                   | O(log size) | O(log size)                   |
| 二叉堆         | 最坏 θ(size) 均摊 θ(log size)？ | 最坏 θ(size) 均摊 θ(log size)？ | θ(size)                       | θ(size)     | O(size)                       |
| thin_heap_tag  | θ(1)                            | 最坏 θ(size) 均摊 θ(log size)   | 最坏 θ(size) 均摊 θ(log size) | θ(size)     | 最坏 θ(size) 均摊 θ(log size) |

**支持堆的合并**

