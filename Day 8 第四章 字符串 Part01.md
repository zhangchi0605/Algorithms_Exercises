# Day 8 第四章 字符串 Part01

今日任务 

● 344.反转字符串
● 541. 反转字符串II
● 卡码网：54.替换数字
● 151.翻转字符串里的单词
● 卡码网：55.右旋转字符串

## 344.反转字符串
[题目链接](344.反转字符串)
[文章讲解](https://programmercarl.com/0344.%E5%8F%8D%E8%BD%AC%E5%AD%97%E7%AC%A6%E4%B8%B2.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE)
[视频讲解](https://www.bilibili.com/video/BV1fV4y17748)

### 双指针
- 字符串也是一种数组，所以元素在内存中是连续分布
- 对于字符串，我们定义两个指针（也可以说是索引下标），一个从字符串前面，一个从字符串后面，两个指针同时向中间移动，并交换元素。
- 时间复杂度: O(n)
- 空间复杂度: O(1)
```cpp
class Solution {
public:
    void reverseString(vector<char>& s) {
        for (int i = 0, j = s.size() - 1; i < s.size()/2; i++, j--) {
            swap(s[i],s[j]);
        }
    }
};
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
- 时间复杂度: O(n)
- 空间复杂度: O(1)
```cpp
class Solution {
public:
    void reverse(string& s, int start, int end) {
        for (int i = start, j = end; i < j; i++, j--) {
            swap(s[i], s[j]);
        }
    }
    string reverseStr(string s, int k) {
        for (int i = 0; i < s.size(); i += (2 * k)) {
            // 1. 每隔 2k 个字符的前 k 个字符进行反转
            // 2. 剩余字符小于 2k 但大于或等于 k 个，则反转前 k 个字符
            if (i + k <= s.size()) {
                reverse(s, i, i + k - 1);
                continue;
            }
            // 3. 剩余字符少于 k 个，则将剩余字符全部反转。
            reverse(s, i, s.size() - 1);
        }
        return s;
    }
};
```

## 卡码网：54.替换数字
[题目链接](https://kamacoder.com/problempage.php?pid=1064)
[文章讲解](https://programmercarl.com/kama54.%E6%9B%BF%E6%8D%A2%E6%95%B0%E5%AD%97.html#%E6%80%9D%E8%B7%AF)

### 双指针
- 很多数组填充类的问题，其做法都是先预先给数组扩容带填充后的大小，然后在从后向前进行操作
- 这么做有两个好处：
    - 不用申请新数组。
    - 从后向前填充元素，避免了从前向后填充元素时，每次添加元素都要将添加元素之后的所有元素向后移动的问题。
### 过程
- 首先扩充数组到每个数字字符替换成 "number" 之后的大小。
- 然后从后向前替换数字字符，也就是双指针法，过程如下：i指向新长度的末尾，j指向旧长度的末尾。
  - 时间复杂度：O(n)
  - 空间复杂度：O(1)
### 注意
__单字符'', 双字符""__

```cpp
#include <iostream>
using namespace std;

int main()
{
    string s;
    while (cin >> s)
    {
        int  oldIndex = s.size() - 1;
        
        int counter = 0;
        for (int i = 0; i < s.size(); i++)
        {
            if (s[i] >= '0' && s[i] <= '9')
            {
                counter++;
            }
        }
        
        int newSize = s.size() + counter*5;
        s.resize(newSize);
        
        int  newIndex = s.size() - 1;
        
        while(oldIndex>=0)
        {
            if (s[oldIndex] >= '0' && s[oldIndex] <= '9')
            {
                s[newIndex--] = 'r';
                s[newIndex--] = 'e';
                s[newIndex--] = 'b';
                s[newIndex--] = 'm';
                s[newIndex--] = 'u';
                s[newIndex--] = 'n';
            }
            else
            {
                s[newIndex--] = s[oldIndex];
            }
            oldIndex--;
        }
        
        cout << s << endl;
    }
    return 0;
}
```

## 151.翻转字符串里的单词
[题目链接](https://leetcode.cn/problems/reverse-words-in-a-string/)
[文章讲解](https://programmercarl.com/0151.%E7%BF%BB%E8%BD%AC%E5%AD%97%E7%AC%A6%E4%B8%B2%E9%87%8C%E7%9A%84%E5%8D%95%E8%AF%8D.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE)
[视频讲解](https://www.bilibili.com/video/BV1uT41177fX)

- 我们将整个字符串都反转过来，那么单词的顺序指定是倒序了，只不过单词本身也倒序了，那么再把单词反转一下，单词不就正过来了。
  
### 过程
- 移除多余空格 (参考移除元素)
- 将整个字符串反转
- 将每个单词反转

- 举个例子，源字符串为："the sky is blue "
   - 移除多余空格 : "the sky is blue"
   - 字符串反转："eulb si yks eht"
   - 单词反转："blue is sky the"
### 注意
__去除多余空格后要resize: s.resize(slow); //slow的大小即为去除多余空格后的大小。__
     
- 时间复杂度：O(n)
- 空间复杂度: O(1) 或 O(n)，取决于语言中字符串是否可变
```cpp
class Solution {
public:
    void reverse(string& s, int start, int end){ //翻转，区间写法：左闭右闭 []
        for (int i = start, j = end; i < j; i++, j--) {
            swap(s[i], s[j]);
        }
    }

    void removeExtraSpaces(string& s) {//去除所有空格并在相邻单词之间添加空格, 快慢指针。
        int slow = 0;   //整体思想参考https://programmercarl.com/0027.移除元素.html
        for (int i = 0; i < s.size(); ++i) { //
            if (s[i] != ' ') { //遇到非空格就处理，即删除所有空格。
                if (slow != 0) s[slow++] = ' '; //手动控制空格，给单词之间添加空格。slow != 0说明不是第一个单词，需要在单词前添加空格。
                while (i < s.size() && s[i] != ' ') { //补上该单词，遇到空格说明单词结束。
                    s[slow++] = s[i++];
                }
            }
        }
        s.resize(slow); //slow的大小即为去除多余空格后的大小。
    }

    string reverseWords(string s) {
        removeExtraSpaces(s); //去除多余空格，保证单词之间之只有一个空格，且字符串首尾没空格。
        reverse(s, 0, s.size() - 1);
        int start = 0; //removeExtraSpaces后保证第一个单词的开始下标一定是0。
        for (int i = 0; i <= s.size(); ++i) {
            if (i == s.size() || s[i] == ' ') { //到达空格或者串尾，说明一个单词结束。进行翻转。
                reverse(s, start, i - 1); //翻转，注意是左闭右闭 []的翻转。
                start = i + 1; //更新下一个单词的开始下标start
            }
        }
        return s;
    }
};

```

## 卡码网：55.右旋转字符串
[题目链接](https://kamacoder.com/problempage.php?pid=1065)
[文章讲解](https://programmercarl.com/kama55.%E5%8F%B3%E6%97%8B%E5%AD%97%E7%AC%A6%E4%B8%B2.html)

### 过程
- 整体反转
- 分段 翻转前n部分
- 分段 翻转剩余部分
  
```cpp
// 版本一
#include<iostream>
#include<algorithm>
using namespace std;
int main() {
    int n;
    string s;
    cin >> n;
    cin >> s;
    int len = s.size(); //获取长度

    reverse(s.begin(), s.end()); // 整体反转
    reverse(s.begin(), s.begin() + n); // 先反转前一段，长度n
    reverse(s.begin() + n, s.end()); // 再反转后一段

    cout << s << endl;
} 
```
