# LeetCode 热题 100
## Table of Contents
- [哈希](#哈希)
  - [1. 两数之和](#1-两数之和)

## 哈希
### [1. 两数之和](https://leetcode-cn.com/problems/two-sum/)

首先想到的实现方式是两个循环遍历数组，两两求和，时间复杂度为 $O(n^2)$ 。实现代码如下：
```C++
class Solution {
public:
    vector<int> twoSum(vector<int>& nums, int target) {
        for (size_t i = 0; i < nums.size() - 1; i++) {
            for (size_t j = i + 1; j < nums.size(); j++) {
                if (nums[i] + nums[j] == target) {
                    return {static_cast<int>(i), static_cast<int>(j)};
                }
            }
        }
        return {};
    }
};
```
通过测试，执行用时51ms，击败31.73%；消耗内存13.90MB，击败63.97%。

#### 优化思路
使用哈希表存储已遍历的元素，以空间换时间。哈希表存元素到索引的映射，这样就能通过元素值快速查找到索引。每次遍历时，判断 `target - nums[i]` 是否在哈希表中，如果在则说明先前已经遍历过该元素，直接返回元素的索引；否则将当前元素存入哈希表。时间复杂度为 $O(n)$ 。

C++通过 `std::unordered_map` 实现哈希表，和 Python 的 `dict` 类似。

`std::unordered_map` 和 `std::map` 的区别：
| 特性 | `std::unordered_map` | `std::map` |
|:---:|:---:|:---:|
| 底层实现 | 哈希表 | 红黑树 |
| 查找 | $O(1)$ | $O(\log n)$ |
| 插入 | $O(1)$ | $O(\log n)$ |
| 删除 | $O(1)$ | $O(\log n)$ |
| 有序性 | 无序 | 有序 |

`unordered_map.find(key)` 返回一个迭代器，如果找到则返回指向该元素的迭代器，否则返回 `end()`。
`end()` 是一个指向容器末尾的迭代器，它不指向任何元素，而是表示超出容器末尾的一个位置。通常用于检查元素是否存在于哈希表中。

通过测试，执行用时4ms，击败58.92%；消耗内存14.68MB，击败15.20%。