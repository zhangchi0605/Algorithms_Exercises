# Day 7 第三章 哈希表 Part02

今日任务 

● 454.四数相加II 
● 383. 赎金信 
● 15. 三数之和 
● 18. 四数之和 
● 总结  

## 454.四数相加II
[题目链接](https://leetcode.cn/problems/4sum-ii/)
[文章讲解](https://programmercarl.com/0454.%E5%9B%9B%E6%95%B0%E7%9B%B8%E5%8A%A0II.html)
[视频讲解](https://www.bilibili.com/video/BV1Md4y1Q7Yh)

## 思路
- 本题是使用哈希法的经典题目
- 这道题目是四个独立的数组，只要找到A[i] + B[j] + C[k] + D[l] = 0就可以，不用考虑有重复的四个元素相加等于0的情况，所以相对于题目18. 四数之和，题目15.三数之和，还是简单了不少！
### 本题解题步骤：
  - 首先定义 一个unordered_map，key放a和b两数之和，value 放a和b两数之和出现的次数。
  - 遍历大A和大B数组，统计两个数组元素之和，和出现的次数，放到map中。
  - 定义int变量count，用来统计 a+b+c+d = 0 出现的次数。
  - 在遍历大C和大D数组，找到如果 0-(c+d) 在map中出现过的话，就用count把map中key对应的value也就是出现次数统计出来。
  - 最后返回统计值 count 就可以了
```cpp
class Solution {
public:
    int fourSumCount(vector<int>& A, vector<int>& B, vector<int>& C, vector<int>& D) {
        unordered_map<int, int> umap; //key:a+b的数值，value:a+b数值出现的次数
        // 遍历大A和大B数组，统计两个数组元素之和，和出现的次数，放到map中
        for (int a : A) {
            for (int b : B) {
                umap[a + b]++;
            }
        }
        int count = 0; // 统计a+b+c+d = 0 出现的次数
        // 在遍历大C和大D数组，找到如果 0-(c+d) 在map中出现过的话，就把map中key对应的value也就是出现次数统计出来。
        for (int c : C) {
            for (int d : D) {
                if (umap.find(0 - (c + d)) != umap.end()) {
                    count += umap[0 - (c + d)];
                }
            }
        }
        return count;
    }
};
```

## 383. 赎金信 
[题目链接]()
[文章讲解]()
[视频讲解]()

## 15. 三数之和 
[题目链接]()
[文章讲解]()
[视频讲解]()

## 18. 四数之和 
[题目链接]()
[文章讲解]()
[视频讲解]()

## 总结
[文章讲解]()
