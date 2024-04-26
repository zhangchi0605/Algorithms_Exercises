# Day 10 第五章 栈与队列 Part01

## 今日任务：
● 理论基础
● 232.用栈实现队列
● 225. 用队列实现栈

## 理论基础
[文章讲解](https://programmercarl.com/%E6%A0%88%E4%B8%8E%E9%98%9F%E5%88%97%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html)

### 栈与队列理论基础
- 队列是先进先出
- 栈是先进后出
![image](https://github.com/zhangchi0605/LeetCode/assets/30234384/8e52511e-5197-4323-bd85-4a77a171d6d6)

- 栈和队列是STL（C++标准库）里面的两个数据结构。

### C++标准库是有多个版本的，要知道我们使用的STL是哪个版本，才能知道对应的栈和队列的实现原理
- HP STL: HP STL是C++ STL的第一个实现版本，而且开放源代码
- P.J.Plauger STL: 参照HP STL实现出来的，被Visual C++编译器所采用，不是开源的
- SGI STL: 由Silicon Graphics Computer Systems公司参照HP STL实现，被Linux的C++编译器GCC所采用，SGI STL是开源软件，源码可读性甚高 (接下来介绍的栈和队列也是SGI STL里面的数据结构)

### 栈
- 栈提供push 和 pop 等等接口，所有元素必须符合先进后出规则，所以栈不提供走访功能，也不提供迭代器(iterator)。 不像是set 或者map 提供迭代器iterator来遍历所有元素。
- 栈是以底层容器完成其所有的工作，对外提供统一的接口，底层容器是可插拔的（也就是说我们可以控制使用哪种容器来实现栈的功能）。
- TL中栈往往不被归类为容器，而被归类为container adapter（容器适配器）。

### 栈的实现
- 栈的内部结构，栈的底层实现可以是vector，deque，list 都是可以的， 主要就是数组和链表的底层实现。
- 常用的SGI STL，如果没有指定底层实现的话，默认是以deque为缺省情况下栈的底层结构.
- deque是一个双向队列，只要封住一段，只开通另一端就可以实现栈的逻辑了。
- 我们也可以指定vector为栈的底层实现，初始化语句如下： ```std::stack<int, std::vector<int> > third;  // 使用vector为底层容器的栈```
  
![image](https://github.com/zhangchi0605/LeetCode/assets/30234384/cd21eb81-0a38-4578-90d0-7ac6494bf548)

### 队列
- 队列中先进先出的数据结构，同样不允许有遍历行为，不提供迭代器
- SGI STL中队列一样是以deque为缺省情况下的底部结构。```std::queue<int, std::list<int>> third; // 定义以list为底层容器的队列```
- STL 队列也不被归类为容器，而被归类为container adapter（ 容器适配器）。
  
### 队列的实现
- SGI STL中 队列底层实现缺省情况下一样使用deque实现的。
- 也可以指定list 为起底层实现，初始化queue的语句如下：

## 232.用栈实现队列
[题目链接](https://leetcode.cn/problems/implement-queue-using-stacks/)
[文章讲解](https://programmercarl.com/0232.%E7%94%A8%E6%A0%88%E5%AE%9E%E7%8E%B0%E9%98%9F%E5%88%97.html#%E7%AE%97%E6%B3%95%E5%85%AC%E5%BC%80%E8%AF%BE)
[视频讲解](https://www.bilibili.com/video/BV1nY4y1w7VC)

### 思路
- 使用栈来模式队列的行为，如果仅仅用一个栈，是一定不行的，所以需要两个栈一个输入栈，一个输出栈，这里要注意输入栈和输出栈的关系。
- 在push数据的时候，只要数据放进输入栈就好
- 但在pop的时候，操作就复杂一些，输出栈如果为空，就把进栈数据全部导入进来（注意是全部导入）再从出栈弹出数据。 如果输出栈不为空，则直接从出栈弹出数据就可以了。
- 如果进栈和出栈都为空的话，说明模拟的队列为空了。

- 时间复杂度: push和empty为O(1), pop和peek为O(n)
- 空间复杂度: O(n)
```cpp
class MyQueue {
public:
    stack<int> stIn;
    stack<int> stOut;
    /** Initialize your data structure here. */
    MyQueue() {

    }
    /** Push element x to the back of queue. */
    void push(int x) {
        stIn.push(x);
    }

    /** Removes the element from in front of queue and returns that element. */
    int pop() {
        // 只有当stOut为空的时候，再从stIn里导入数据（导入stIn全部数据）
        if (stOut.empty()) {
            // 从stIn导入数据直到stIn为空
            while(!stIn.empty()) {
                stOut.push(stIn.top());
                stIn.pop();
            }
        }
        int result = stOut.top();
        stOut.pop();
        return result;
    }

    /** Get the front element. */
    int peek() {
        int res = this->pop(); // 直接使用已有的pop函数
        stOut.push(res); // 因为pop函数弹出了元素res，所以再添加回去
        return res;
    }

    /** Returns whether the queue is empty. */
    bool empty() {
        return stIn.empty() && stOut.empty();
    }
};
```

## 225.用队列实现栈
[题目链接]()
[文章讲解]()
[视频讲解]()

