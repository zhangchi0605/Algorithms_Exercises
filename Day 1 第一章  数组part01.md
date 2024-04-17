# Day 1 第一章  数组part01

- 数组是存放在连续内存空间上的相同类型数据的集合
    - 数组下标都是从0开始的。
    - 数组内存空间的地址是连续的
    - 二维数组在内存空间中的地址是连续的
    - 数组的元素是不能删的，只能覆盖
- 删除或者增添数组元素的时候，**需要移动**其他元素的地址
- 在C++中，vector是容器，它的底层实现是数组

## 704 Binary Search
[文章](https://programmercarl.com/0704.%E4%BA%8C%E5%88%86%E6%9F%A5%E6%89%BE.html)
[力扣题](https://leetcode.cn/problems/binary-search/)

- 二分搜索在循环搜索的过程中需要注意的内容：
    - 坚持搜索区间的定义**(左闭右闭)、(左闭右开)**
    - 根据对应的区间定义更新 left / right 的值

### 左闭右闭
  - 潜在的目标元素如果存在，一定在 [left, right] 中，且区间中都是尚未检查的元素
  - 每次与mid值比较且没有查找到目标元素时，剩余的二分区间一定不包含mid位置
      - e.g. mid > target ⇒ 因此下一个迭代的区间是 [left, mid-1]，因为mid已经确认不包含我们需要的目标元素
      - e.g. mid < target ⇒ 下一个迭代的区间是 [mid+1, right]
  - 每次循环判断时，**while 的条件判断**需要写成 **left <= right**
      - 由于我们的区间定义意味着所有区间内的元素都是未检查的元素(可能为目标元素)
      - 当区间长度为2时，剩余2个元素尚未被检查 ⇒ 同理长度为1时仍需要检查
      - 因此此时 **left <= right** 保证了最后一次循环会检查 left == right 位置的元素
  - **左闭右闭答案写法:**
    ```cpp
      class Solution {
      public:
          int search(vector<int>& nums, int target) {
              int left = 0;
              int right = nums.size() - 1; // 定义target在左闭右闭的区间里，[left, right]
              while (left <= right) { // 当left==right，区间[left, right]依然有效，所以用 <=
                  int middle = left + ((right - left) / 2);// 防止溢出 等同于(left + right)/2
                  if (nums[middle] > target) {
                      right = middle - 1; // target 在左区间，所以[left, middle - 1]
                  } else if (nums[middle] < target) {
                      left = middle + 1; // target 在右区间，所以[middle + 1, right]
                  } else { // nums[middle] == target
                      return middle; // 数组中找到目标值，直接返回下标
                  }
              }
              // 未找到目标值
              return -1;
          }
      };
    ```
            
### 左闭右开
  - 目标如果存在，一定在 [left, right) 中，且区间中都是尚未检查的元素
      - **注意此时该区间不包含 right**
  - 每次与mid值比较且没有查找到目标元素时，剩余的二分区间由区间定义意义
      - e.g. mid > target ⇒ 下一个迭代的区间是 [left, mid)
      - e.g. mid < target ⇒ 下一个迭代的区间是 [mid+1, right)
          - **此时使用 mid+1 因为我们是左闭右开区间**
  - 每次循环判断时，**while 的条件判断**需要写成 **left < right**
      - 由于我们的区间定义意味着区间的最后一个元素：right 所在的元素是被检查过且不是目标值的
      - 当区间长度为2时，只有1个元素尚未被检查 ⇒ 此时 left < right 应该是最后一次检查
  - **左闭右开答案写法:**     
  ```cpp
  class Solution {
  public:
      int search(vector<int>& nums, int target) {
          int left = 0;
          int right = nums.size(); // 定义target在左闭右开的区间里，即：[left, right)
          while (left < right) { // 因为left == right的时候，在[left, right)是无效的空间，所以使用 <
              int middle = left + ((right - left) >> 1);
              if (nums[middle] > target) {
                  right = middle; // target 在左区间，在[left, middle)中
              } else if (nums[middle] < target) {
                  left = middle + 1; // target 在右区间，在[middle + 1, right)中
              } else { // nums[middle] == target
                  return middle; // 数组中找到目标值，直接返回下标
              }
          }
          // 未找到目标值
          return -1;
      }
  };
  ```
            

## 27 Remove Element
