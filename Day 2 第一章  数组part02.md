# Day 2 第一章  数组part02

## 977.有序数组的平方
[题目链接](https://leetcode.cn/problems/squares-of-a-sorted-array/)
[文章讲解](https://programmercarl.com/0977.%E6%9C%89%E5%BA%8F%E6%95%B0%E7%BB%84%E7%9A%84%E5%B9%B3%E6%96%B9.html)
[视频讲解](https://www.bilibili.com/video/BV1QB4y1D7ep )

# 暴力排序
- 每个数平方之后，排个序
- 时间复杂度是 O(n + nlogn)
```cpp
class Solution {
public:
    vector<int> sortedSquares(vector<int>& nums) {
        for (int i = 0; i < nums.size(); i++)
        {
            nums[i] *= nums[i];
        }
        sort(nums.begin(), nums.end());
        
        return nums;
    }
};
```




```cpp
class Solution {
public:
    vector<int> sortedSquares(vector<int>& nums) {
        int left_index = 0;
        int right_index = nums.size()-1;
        int result_index = nums.size()-1;
        
        vector<int> result(nums.size(), 0);

        while (right_index >= left_index)
        {
            if (nums[left_index]*nums[left_index] < nums[right_index]*nums[right_index])
            {
                result[result_index--] = nums[right_index]* nums[right_index];
                right_index--;
            }
            else
            {
                result[result_index--] = nums[left_index] * nums[left_index];
                left_index++;
            }
        }
        return result;
    }
};
```

## 209.长度最小的子数组
[题目链接]([https://leetcode.cn/problems/squares-of-a-sorted-array/](https://leetcode.cn/problems/minimum-size-subarray-sum/))
[文章讲解](https://programmercarl.com/0209.%E9%95%BF%E5%BA%A6%E6%9C%80%E5%B0%8F%E7%9A%84%E5%AD%90%E6%95%B0%E7%BB%84.html)
[视频讲解](https://www.bilibili.com/video/BV1tZ4y1q7XE)

## 59.螺旋矩阵II
[题目链接](https://leetcode.cn/problems/spiral-matrix-ii/)
[文章讲解](https://programmercarl.com/0059.%E8%9E%BA%E6%97%8B%E7%9F%A9%E9%98%B5II.html)
[视频讲解](https://www.bilibili.com/video/BV1SL4y1N7mV/)
