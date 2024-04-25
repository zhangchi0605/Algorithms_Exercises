# Day 2 第一章  数组 Part02

## 今日任务

977.有序数组的平方 ，209.长度最小的子数组 ，59.螺旋矩阵II ，总结 

## 977.有序数组的平方
[题目链接](https://leetcode.cn/problems/squares-of-a-sorted-array/)
[文章讲解](https://programmercarl.com/0977.%E6%9C%89%E5%BA%8F%E6%95%B0%E7%BB%84%E7%9A%84%E5%B9%B3%E6%96%B9.html)
[视频讲解](https://www.bilibili.com/video/BV1QB4y1D7ep )

### 暴力排序
- 每个数平方之后，排个序
- 时间复杂度是 O(n + nlogn)
- 注意：sort命令：std::sort (myvector.begin(), myvector.end());
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
### 双指针法
- 数组其实是有序的， 只不过负数平方之后可能成为最大数了。
- 那么数组平方的最大值就在数组的两端，不是最左边就是最右边，不可能是中间。
- 时间复杂度为O(n)
  
- 注意：数组要初始化 ``` vector<int> result(nums.size(), 0); ``` 
  
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
[题目链接](https://leetcode.cn/problems/minimum-size-subarray-sum/)
[文章讲解](https://programmercarl.com/0209.%E9%95%BF%E5%BA%A6%E6%9C%80%E5%B0%8F%E7%9A%84%E5%AD%90%E6%95%B0%E7%BB%84.html)
[视频讲解](https://www.bilibili.com/video/BV1tZ4y1q7XE)

### 暴力算法
- 积累：
    -  int result = INT32_MAX;
    -  result = result < subLength ? result : subLength;
    -  return result == INT32_MAX ? 0 : result;
      
```cpp
class Solution {
public:
    int minSubArrayLen(int s, vector<int>& nums) {
        int result = INT32_MAX; // 最终的结果
        int sum = 0; // 子序列的数值之和
        int subLength = 0; // 子序列的长度
        for (int i = 0; i < nums.size(); i++) { // 设置子序列起点为i
            sum = 0;
            for (int j = i; j < nums.size(); j++) { // 设置子序列终止位置为j
                sum += nums[j];
                if (sum >= s) { // 一旦发现子序列和超过了s，更新result
                    subLength = j - i + 1; // 取子序列的长度
                    result = result < subLength ? result : subLength;
                    break; // 因为我们是找符合条件最短的子序列，所以一旦符合条件就break
                }
            }
        }
        // 如果result没有被赋值的话，就返回0，说明没有符合条件的子序列
        return result == INT32_MAX ? 0 : result;
    }
};

```

### 滑动窗口
- 所谓滑动窗口，就是不断的调节子序列的起始位置和终止位置，从而得出我们要想的结果。
- 只用一个for循环，那么这个循环的索引，一定是表示 滑动窗口的终止位置。
    - 窗口就是 满足其和 ≥ s 的长度最小的 连续 子数组。
    - 窗口的结束位置如何移动：窗口的结束位置就是遍历数组的指针，也就是for循环里的索引。
    - 窗口的起始位置如何移动：如果当前窗口的值大于等于s了，窗口就要向前移动了（也就是该缩小了）。
  
- 时间复杂度：O(n)：
    - 每个元素在滑动窗后进来操作一次，出去操作一次，每个元素都是被操作两次，所以时间复杂度是 2 × n 也就是O(n)
- 空间复杂度：O(1)
```cpp
class Solution {
public:
    int minSubArrayLen(int target, vector<int>& nums) {
        int front_index = 0; // 滑动窗口起始位置
        int sum = 0; // 滑动窗口数值之和
        int subLength = 0; // 滑动窗口的长度
        int result = INT32_MAX;

        for (int back_index = 0; back_index < nums.size(); back_index++)
        {
            sum += nums[back_index];

            while (sum >= target) // 注意这里使用while，每次更新 front_index（起始位置），并不断比较子序列是否符合条件
            {
                subLength = back_index - front_index + 1;
                result = result < subLength ? result : subLength;
                sum -= nums[front_index]; 
                front_index++; // 这里体现出滑动窗口的精髓之处，不断变更front_index（子序列的起始位置）
            }
        }
        return result == INT32_MAX ? 0 : result;
    }
};
```

## 59.螺旋矩阵II
[题目链接](https://leetcode.cn/problems/spiral-matrix-ii/)
[文章讲解](https://programmercarl.com/0059.%E8%9E%BA%E6%97%8B%E7%9F%A9%E9%98%B5II.html)
[视频讲解](https://www.bilibili.com/video/BV1SL4y1N7mV/)

### 顺时针画矩阵
- 模拟顺时针画矩阵的过程: 填充上行从左到右，填充右列从上到下，填充下行从右到左，填充左列从下到上
- 思路：初始化一个 n×n 大小的矩阵 mat，然后模拟整个向内环绕的填入过程：
    1. 定义当前左右上下边界 l,r,t,b，初始值 num = 1，迭代终止值 tar = n * n；
    2. 当 num <= tar 时，始终按照 从左到右 从上到下 从右到左 从下到上 填入顺序循环，每次填入后：
        - 执行 num += 1：得到下一个需要填入的数字；
        - 更新边界：例如从左到右填完后，上边界 t += 1，相当于上边界向内缩 1。
    3. 使用num <= tar而不是l < r || t < b作为迭代条件，是为了解决当n为奇数时，矩阵中心数字无法在迭代过程中被填充的问题。
    4. 最终返回 mat 即可。
 
- 注意：
    - 初始化矩阵 vector<vector<int>> mat(n, vector<int>(n, 0));
    - for循环边界条件 for (int i = right; i >= left; i--)
    
- 时间复杂度 O(n^2): 模拟遍历二维矩阵的时间
- 空间复杂度 O(1)
```cpp
class Solution {
public:
    vector<vector<int>> generateMatrix(int n) {
        
        vector<vector<int>> mat(n, vector<int>(n, 0));
        int top = 0;
        int bottom = n-1;
        int left = 0;
        int right = n-1;
        int num = 1;
        int target = n*n;

        while (num <= target)
        {
            for (int i = left; i <= right; i++) // left to right.
            {
                mat[top][i] = num++;
            }
            top++;
            for (int i = top; i <= bottom; i++) // top to bottom.
            {
                mat[i][right] = num++;
            }
            right--;
            for (int i = right; i >= left; i--) // right to left.
            {
                mat[bottom][i] = num++;
            }
            bottom--;
            for (int i = bottom; i >= top; i--) // bottom to top.
            {
                mat[i][left] = num++;
            }
            left++;
        }
        return mat;
    }
};
```
