# Day 8 第四章 字符串 Part01

今日任务 

● 344.反转字符串
● 

## 344.反转字符串
[题目链接](344.反转字符串)
[文章讲解](https://programmercarl.com/0344.%E5%8F%8D%E8%BD%AC%E5%AD%97%E7%AC%A6%E4%B8%B2.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE)
[视频讲解](https://www.bilibili.com/video/BV1fV4y17748)

### 双指针
- 字符串也是一种数组，所以元素在内存中是连续分布
- 对于字符串，我们定义两个指针（也可以说是索引下标），一个从字符串前面，一个从字符串后面，两个指针同时向中间移动，并交换元素。


```cpp
```


## 541. 反转字符串II
[题目链接](https://leetcode.cn/problems/reverse-string-ii/)
[文章讲解](https://programmercarl.com/0541.%E5%8F%8D%E8%BD%AC%E5%AD%97%E7%AC%A6%E4%B8%B2II.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE)
[视频讲解](https://www.bilibili.com/video/BV1dT411j7NN)

### 思路
- 遍历字符串的过程中，只要让 i += (2 * k)，i 每次移动 2 * k 就可以了，然后判断是否需要有反转的区间。
- 然后判断是否需要有反转的区间 ```if (i + k <= s.size())```
### 过程
1. 每隔 2k 个字符的前 k 个字符进行反转
2. 剩余字符小于 2k 但大于或等于 k 个，则反转前 k 个字符
3. 剩余字符少于 k 个，则将剩余字符全部反转。

```cpp
```

##
[题目链接]()
[文章讲解]()
[视频讲解]()

##
[题目链接]()
[文章讲解]()
[视频讲解]()
