# Day 6 第二章 链表 Part02

 今日任务 
● 哈希表理论基础 
● 242.有效的字母异位词 
● 349. 两个数组的交集 
● 202. 快乐数
● 1. 两数之和   

## 哈希表理论基础
[文章讲解](https://programmercarl.com/%E5%93%88%E5%B8%8C%E8%A1%A8%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html)

### 哈希表
- 哈希表（英文名字为Hash table)
- 哈希表是根据关键码的值而直接进行访问的数据结构。
![image](https://github.com/zhangchi0605/LeetCode/assets/30234384/36449d7b-4908-4f40-9ea6-59fe2792425d)
- 哈希表解决什么问题: 一般哈希表都是用来快速判断一个元素是否出现集合里。要枚举的话时间复杂度是O(n)，但如果使用哈希表的话， 只需要O(1)就可以做到。
  
### 哈希函数
- 哈希函数如下图所示，通过hashCode把名字转化为数值，一般hashcode是通过特定编码方式，可以将其他数据格式转化为不同的数值，这样就把学生名字映射为哈希表上的索引数字了。
![image](https://github.com/zhangchi0605/LeetCode/assets/30234384/6218a974-1d12-44b6-a37c-a132ad626415)
- 如果hashCode得到的数值大于 哈希表的大小了，也就是大于tableSize了. 会在再次对数值做一个取模的操作.

### 哈希碰撞
- 如图所示，小李和小王都映射到了索引下标 1 的位置，这一现象叫做哈希碰撞。
![image](https://github.com/zhangchi0605/LeetCode/assets/30234384/3bc9ce45-d541-471d-a287-76e8b192c1b7)
- 哈希碰撞有两种解决方法， 拉链法和线性探测法
#### 拉链法
- 发生冲突的元素都被存储在链表中
![image](https://github.com/zhangchi0605/LeetCode/assets/30234384/b22ae30f-5d35-442c-ab46-58b551f690be)
- 其实拉链法就是要选择适当的哈希表的大小，这样既不会因为数组空值而浪费大量内存，也不会因为链表太长而在查找上浪费太多时间。

#### 线性探测法
- 使用线性探测法，一定要保证tableSize大于dataSize
- 例如冲突的位置，放了小李，那么就向下找一个空位放置小王的信息。所以要求tableSize一定要大于dataSize ，要不然哈希表上就没有空置的位置来存放 冲突的数据了
![image](https://github.com/zhangchi0605/LeetCode/assets/30234384/adc671ed-7ce2-408a-98a6-420c0ffad67c)

### 常见的三种哈希结构
- 数组
- set (集合）
 ![image](https://github.com/zhangchi0605/LeetCode/assets/30234384/e8850936-da49-4c2d-b0d0-9dd155691858)

- map (映射)
![image](https://github.com/zhangchi0605/LeetCode/assets/30234384/55303174-c774-4f36-90b9-25a3f560b81e)


## 242.有效的字母异位词 
[题目链接](https://leetcode.cn/problems/valid-anagram/description/)
[文章讲解](https://programmercarl.com/0242.%E6%9C%89%E6%95%88%E7%9A%84%E5%AD%97%E6%AF%8D%E5%BC%82%E4%BD%8D%E8%AF%8D.html)
[视频讲解](https://www.bilibili.com/video/BV1YG411p7BA)

### 思路（数组就是一个简单哈希表）
- 这道题目中字符串只有小写字符，那么就可以定义一个数组，来记录字符串s里字符出现的次数
- 需要把字符映射到数组也就是哈希表的索引下标上
- 因为字符a到字符z的ASCII是26个连续的数值，所以字符a映射为下标0，相应的字符z映射为下标25 （只需要将 s[i] - ‘a’ 所在的元素做+1 操作即可）
- 最后如果record数组所有元素都为零0，说明字符串s和t是字母异位词

### 注意
- C-style Array (```int record[26] = {};```): This is a plain old data type (POD) from C, adopted in C++. It is very straightforward and uses static memory allocation. It lacks any sort of member functions or methods.```
- C++-style std::array (```std::array<int, 26> a{};```): This is a container that comes from the C++ Standard Template Library (STL). It wraps around a C-style array to provide convenience functions, type safety, and compatibility with other STL algorithms and functions.

```cpp
class Solution {
public:
    bool isAnagram(string s, string t) {
        int record[26] = {0};
        for (int i = 0; i < s.size(); i++) {
            // 并不需要记住字符a的ASCII，只要求出一个相对数值就可以了
            record[s[i] - 'a']++;
        }
        for (int i = 0; i < t.size(); i++) {
            record[t[i] - 'a']--;
        }
        for (int i = 0; i < 26; i++) {
            if (record[i] != 0) {
                // record数组如果有的元素不为零0，说明字符串s和t 一定是谁多了字符或者谁少了字符。
                return false;
            }
        }
        // record数组所有元素都为零0，说明字符串s和t是字母异位词
        return true;
    }
};
```


## 349. 两个数组的交集 
[题目链接](https://leetcode.cn/problems/intersection-of-two-arrays/)
[文章讲解](https://programmercarl.com/0349.%E4%B8%A4%E4%B8%AA%E6%95%B0%E7%BB%84%E7%9A%84%E4%BA%A4%E9%9B%86.html)
[视频讲解](https://www.bilibili.com/video/BV1ba411S7wu)

### 思路
- 学会使用一种哈希数据结构：unordered_set
- 注意题目特意说明：输出结果中的每个元素一定是唯一的，也就是说输出的结果的去重的， 同时可以不考虑输出结果的顺序
- 使用数组来做哈希的题目，是因为题目都限制了数值的大小（这里不适用），而且如果哈希值比较少、特别分散、跨度非常大，使用数组就造成空间的极大浪费。
### set选择
- C++ 给提供了如下三种可用的数据结构：
    - std::set
    - std::multiset
    - std::unordered_set
 - std::set和std::multiset底层实现都是红黑树，std::unordered_set的底层实现是哈希表， 使用unordered_set 读写效率是最高的，并不需要对数据进行排序，而且还不要让数据重复，所以选择unordered_set。

- 时间复杂度: O(n + m) m 是最后要把 set转成vector
- 空间复杂度: O(n)
```cpp
class Solution {
public:
    vector<int> intersection(vector<int>& nums1, vector<int>& nums2) {
        unordered_set<int> result_set; // 存放结果，之所以用set是为了给结果集去重
        unordered_set<int> nums_set(nums1.begin(), nums1.end());
        for (int num : nums2) {
            // 发现nums2的元素 在nums_set里又出现过
            if (nums_set.find(num) != nums_set.end()) {
                result_set.insert(num);
            }
        }
        return vector<int>(result_set.begin(), result_set.end());
    }
};
```

      
## 202. 快乐数
[题目链接](https://leetcode.cn/problems/happy-number/)
[文章讲解](https://programmercarl.com/0202.%E5%BF%AB%E4%B9%90%E6%95%B0.html#%E6%80%9D%E8%B7%AF)
 
## 1. 两数之和
[题目链接](https://leetcode.cn/problems/two-sum/)
[文章讲解](https://programmercarl.com/0001.%E4%B8%A4%E6%95%B0%E4%B9%8B%E5%92%8C.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE)
[视频讲解](https://www.bilibili.com/video/BV1aT41177mK)
