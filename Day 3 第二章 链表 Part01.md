# Day 3 第二章 链表 Part01

## 链表理论基础
[文章讲解](https://programmercarl.com/%E9%93%BE%E8%A1%A8%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html)

### 链表

#### 单链表
- 链表是一种通过指针串联在一起的线性结构，每一个节点由两部分组成，一个是数据域一个是指针域（存放指向下一个节点的指针），最后一个节点的指针域指向null（空指针的意思）。
- 链表的入口节点称为链表的头结点也就是head
- 单链表中的指针域只能指向节点的下一个节点。
![image](https://github.com/zhangchi0605/LeetCode/assets/30234384/4c0ab276-3da3-4101-b038-5b431b98353f)

#### 双链表
- 每一个节点有两个指针域，一个指向下一个节点，一个指向上一个节点。
- 既可以向前查询也可以向后查询。
![image](https://github.com/zhangchi0605/LeetCode/assets/30234384/7fec7b42-285d-4004-8c00-eb701c4857ce)

#### 循环链表
- 链表首尾相连
- 循环链表可以用来解决约瑟夫环问题（约瑟夫问题是个著名的问题：N个人围成一圈，第一个人从1开始报数，报M的将被杀掉，下一个人接着从1开始报。如此反复，最后剩下一个，求最后的胜利者。）
![image](https://github.com/zhangchi0605/LeetCode/assets/30234384/f79905e9-0455-4aa6-a94f-896a246516a2)


### 链表的存储方式
- 链表中的节点在内存散乱分布在内存中的某地址上，分配机制取决于操作系统的内存管理。
- 链表是通过指针域的指针链接在内存中各个节点
![image](https://github.com/zhangchi0605/LeetCode/assets/30234384/73e28c0b-ffb1-4f72-b401-a5c1ba4ccdce)

### 链表的定义
- 如果不定义构造函数使用默认构造函数的话，在初始化的时候就不能直接给变量赋值！
- 单链表:
```cpp
struct ListNode {
    int val;  // 节点上存储的元素
    ListNode *next;  // 指向下一个节点的指针
    ListNode(int x) : val(x), next(NULL) {}  // 节点的构造函数
};
```

### 链表的操作

#### 删除节点
- 只要将C节点的next指针 指向E节点就可以了
- 在C++里最好是再手动释放这个D节点，释放这块内存
![image](https://github.com/zhangchi0605/LeetCode/assets/30234384/497caa49-e0a3-4085-a1b5-68865940f1c9)

#### 添加节点
- 链表的增添和删除都是O(1)操作，也不会影响到其他节点。
- 要是删除第五个节点，需要从头节点查找到第四个节点通过next指针进行删除操作，查找的时间复杂度是O(n)
![image](https://github.com/zhangchi0605/LeetCode/assets/30234384/9784a2e4-3410-44c7-a8ad-1ca31559cfd0)

### 性能分析
- 数组在定义的时候，长度就是固定的，如果想改动数组的长度，就需要重新定义一个新的数组。
- 链表的长度可以是不固定的，并且可以动态增删， 适合数据量不固定，频繁增删，较少查询的场景。
![image](https://github.com/zhangchi0605/LeetCode/assets/30234384/63a6d539-5fc8-4b3c-bd49-c0e824195fe0)


## 203.移除链表元素
[题目链接](https://leetcode.cn/problems/remove-linked-list-elements/)
[文章讲解](https://programmercarl.com/0203.%E7%A7%BB%E9%99%A4%E9%93%BE%E8%A1%A8%E5%85%83%E7%B4%A0.html)
[视频讲解](https://www.bilibili.com/video/BV18B4y1s7R9)

### 虚拟头结点法
- 设置一个虚拟头结点,并指向head: ```ListNode* dummy_node = new ListNode(0, head); ```
![image](https://github.com/zhangchi0605/LeetCode/assets/30234384/f2367895-5086-4b87-9fe7-3d8f04c4d44a)

- 代码：
- 时间复杂度: O(n)
- 空间复杂度: O(1)
```cpp
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
        ListNode* dummy_node = new ListNode(0, head);
        ListNode* current_node = dummy_node;  // Start with the dummy node
        while (current_node->next != nullptr) {
            if (current_node->next->val == val) { // 注意是下一个node的值等于val
                ListNode* temp = current_node->next;
                current_node->next = current_node->next->next;
                delete temp;
            } else {
                current_node = current_node->next;
            }
        }
        head = dummy_node->next;
        delete dummy_node;
        return head;
    }
};
```

## 707.设计链表 
[题目链接]()
[文章讲解]()
[视频讲解]()
### 虚拟头结点法
- 获取链表中下标为 index 的节点的值的意思是: 第 index 个节点
- 实现功能:
    - get(index)：获取链表中第 index 个节点的值。如果索引无效，则返回-1。
    - addAtHead(val)：在链表的第一个元素之前添加一个值为 val 的节点。插入后，新节点将成为链表的第一个节点。
    - addAtTail(val)：将值为 val 的节点追加到链表的最后一个元素。
    - addAtIndex(index,val)：在链表中的第 index 个节点之前添加值为 val  的节点。如果 index 等于链表的长度，则该节点将附加到链表的末尾。如果 index 大于链表长度，则不会插入节点。如果index小于0，则在头部插入节点。
    - deleteAtIndex(index)：如果索引 index 有效，则删除链表中的第 index 个节点

- LeetCode [官方题解不错](https://leetcode.cn/problems/design-linked-list/solutions/1840997/she-ji-lian-biao-by-leetcode-solution-abix/)
- 复杂度<img width="365" alt="image" src="https://github.com/zhangchi0605/LeetCode/assets/30234384/51550d8f-2b74-4d63-8b1c-99a6fffd95c7">

```cpp
class MyLinkedList {
public:
    // 定义链表节点结构体
    struct ListNode {
        int val;
        ListNode* next;
        ListNode(int val):val(val), next(nullptr){}
    };

    MyLinkedList() {
        this->size = 0;
        this->head = new ListNode(0);
    }
    
    int get(int index) {
        if (index < 0 || index >= size) {
            return -1;
        }
        ListNode *cur = head;
        for (int i = 0; i <= index; i++) {
            cur = cur->next;
        }
        return cur->val;
    }
    
    void addAtHead(int val) {
        addAtIndex(0, val);
    }
    
    void addAtTail(int val) {
        addAtIndex(size, val);
    }
    
    void addAtIndex(int index, int val) {
        if (index > size) {
            return;
        }
        index = max(0, index);
        size++;
        ListNode *pred = head;
        for (int i = 0; i < index; i++) {
            pred = pred->next;
        }
        ListNode *toAdd = new ListNode(val);
        toAdd->next = pred->next;
        pred->next = toAdd;
    }
    
    void deleteAtIndex(int index) {
        if (index < 0 || index >= size) {
            return;
        }
        size--;
        ListNode *pred = head;
        for (int i = 0; i < index; i++) {
            pred = pred->next;
        }
        ListNode *p = pred->next;
        pred->next = pred->next->next;
        delete p;
    }
private:
    int size;
    ListNode *head;
};
```
## 206.反转链表 
[题目链接]()
[文章讲解]()
[视频讲解]()
