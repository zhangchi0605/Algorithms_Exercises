# Day 4 第二章 链表 Part02

今日任务 
● 24. 两两交换链表中的节点 
● 19.删除链表的倒数第N个节点 
● 面试题 02.07. 链表相交 
● 142.环形链表II 
● 总结

## 24. 两两交换链表中的节点
[题目链接](https://leetcode.cn/problems/swap-nodes-in-pairs/)
[文章讲解](https://programmercarl.com/0024.%E4%B8%A4%E4%B8%A4%E4%BA%A4%E6%8D%A2%E9%93%BE%E8%A1%A8%E4%B8%AD%E7%9A%84%E8%8A%82%E7%82%B9.html)
[视频讲解](https://www.bilibili.com/video/BV1YT411g7br)

### 虚拟头结点
- 使用虚拟头节点，画图辅助模拟链表操作过程。 ![image](https://github.com/zhangchi0605/LeetCode/assets/30234384/e5488594-2feb-4d31-9bc6-f1633d2a445c)
- 注意需要记录的临时节点指针方向。注意最终结果是虚拟头节点的next。
- 时间复杂度：O(n)
- 空间复杂度：O(1）
```cpp
class Solution {
public:
    ListNode* swapPairs(ListNode* head) {
        ListNode* dummyHead = new ListNode(0); // 设置一个虚拟头结点
        dummyHead->next = head; // 将虚拟头结点指向head，这样方便后面做删除操作
        ListNode* cur = dummyHead;
        while(cur->next != nullptr && cur->next->next != nullptr) {
            ListNode* tmp = cur->next; // 记录临时节点
            ListNode* tmp1 = cur->next->next->next; // 记录临时节点

            cur->next = cur->next->next;    // 步骤一
            cur->next->next = tmp;          // 步骤二
            cur->next->next->next = tmp1;   // 步骤三

            cur = cur->next->next; // cur移动两位，准备下一轮交换
        }
        ListNode* result = dummyHead->next;
        delete dummyHead;
        return result;
    }
};
```

## 19.删除链表的倒数第N个节点
[题目链接](https://leetcode.cn/problems/remove-nth-node-from-end-of-list/)
[文章讲解](https://programmercarl.com/0019.%E5%88%A0%E9%99%A4%E9%93%BE%E8%A1%A8%E7%9A%84%E5%80%92%E6%95%B0%E7%AC%ACN%E4%B8%AA%E8%8A%82%E7%82%B9.html)
[视频讲解](https://www.bilibili.com/video/BV1vW4y1U7Gf)

### 双指针(快慢指针)
- 定义fast指针和slow指针，初始值为虚拟头结点 ![image](https://github.com/zhangchi0605/LeetCode/assets/30234384/d7c82362-bd32-4991-b7f6-920f57262516)
- fast首先走n + 1步 ，为什么是n+1呢，因为只有这样同时移动的时候slow才能指向删除节点的上一个节点（方便做删除操作）![image](https://github.com/zhangchi0605/LeetCode/assets/30234384/8db0c4c0-62e4-4839-9fd0-33f197b45646)
- fast和slow同时移动，直到fast指向末尾 ![image](https://github.com/zhangchi0605/LeetCode/assets/30234384/2f2f75ab-10b3-4da4-815c-42a95c99733a)
- 删除slow指向的下一个节点 ![image](https://github.com/zhangchi0605/LeetCode/assets/30234384/5da35938-4a15-4446-99ef-b6c94822b330)
  
- 时间复杂度: O(n)
- 空间复杂度: O(1)
```cpp
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* dummyHead = new ListNode(0, head);
        ListNode* fast = dummyHead;
        ListNode* slow = dummyHead;
        while(n-- && fast != nullptr) {
            fast = fast->next;
        }
        fast = fast->next; // fast再提前走一步，因为需要让slow指向删除节点的上一个节点
        while (fast)
        {
            fast = fast->next;
            slow = slow->next;
        }

        ListNode* tem = slow->next;
        slow->next = tem->next;
        delete tem;
        ListNode* result = dummyHead->next;
        delete dummyHead;
        return result;
    }
};
```

## 面试题 02.07. 链表相交
[题目链接](https://leetcode.cn/problems/intersection-of-two-linked-lists-lcci/)
[文章讲解](https://programmercarl.com/%E9%9D%A2%E8%AF%95%E9%A2%9802.07.%E9%93%BE%E8%A1%A8%E7%9B%B8%E4%BA%A4.html)

### 
- 求两个链表交点节点的指针
- 交点不是数值相等，而是指针相等
- 求出两个链表的长度，并求出两个链表长度的差值，然后让curA移动到，和curB 末尾对齐的位置 ![image](https://github.com/zhangchi0605/LeetCode/assets/30234384/ba3ab130-4c6b-4c3e-b351-a1cf67975330)
- 比较curA和curB是否相同，如果不相同，同时向后移动curA和curB，如果遇到curA == curB，则找到交点。

- 时间复杂度：O(n + m)
- 空间复杂度：O(1)
```cpp
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        ListNode* curA = headA;
        ListNode* curB = headB;
        int lenA = 0, lenB = 0;
        while (curA != NULL) { // 求链表A的长度
            lenA++;
            curA = curA->next;
        }
        while (curB != NULL) { // 求链表B的长度
            lenB++;
            curB = curB->next;
        }
        curA = headA;
        curB = headB;
        // 让curA为最长链表的头，lenA为其长度
        if (lenB > lenA) {
            swap (lenA, lenB);
            swap (curA, curB);
        }
        // 求长度差
        int gap = lenA - lenB;
        // 让curA和curB在同一起点上（末尾位置对齐）
        while (gap--) {
            curA = curA->next;
        }
        // 遍历curA 和 curB，遇到相同则直接返回
        while (curA != NULL) {
            if (curA == curB) {
                return curA;
            }
            curA = curA->next;
            curB = curB->next;
        }
        return NULL;
    }
};
```


## 142.环形链表II 
[题目链接](https://leetcode.cn/problems/linked-list-cycle-ii/description/)
[文章讲解](https://programmercarl.com/0142.%E7%8E%AF%E5%BD%A2%E9%93%BE%E8%A1%A8II.html)
[视频讲解](https://www.bilibili.com/video/BV1if4y1d7ob)

### 1. 判断链表是否有环 2. 找到这个环的入口
- 判断链表是否环: 可以使用快慢指针法，分别定义 fast 和 slow 指针，从头结点出发，fast指针每次移动两个节点，slow指针每次移动一个节点，如果 fast 和 slow指针在途中相遇 ，说明这个链表有环。
- 如果有环，如何找到这个环的入口:
    - 结论: 从头结点出发一个指针，从相遇节点 也出发一个指针，这两个指针每次只走一个节点， 那么当这两个指针相遇的时候就是 环形入口的节点。
    - 推导: [过程](https://programmercarl.com/0142.%E7%8E%AF%E5%BD%A2%E9%93%BE%E8%A1%A8II.html#%E6%80%9D%E8%B7%AF) 图 ![image](https://github.com/zhangchi0605/LeetCode/assets/30234384/8cb4bf6f-680a-4515-b169-65f5de9a9f0f)
```cpp
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        ListNode* fast = head;
        ListNode* slow = head;
        while(fast != NULL && fast->next != NULL) {
            slow = slow->next;
            fast = fast->next->next;
            // 快慢指针相遇，此时从head 和 相遇点，同时查找直至相遇
            if (slow == fast) {
                ListNode* index1 = fast;
                ListNode* index2 = head;
                while (index1 != index2) {
                    index1 = index1->next;
                    index2 = index2->next;
                }
                return index2; // 返回环的入口
            }
        }
        return NULL;
    }
};
```


## 总结
[文章讲解](https://programmercarl.com/%E9%93%BE%E8%A1%A8%E6%80%BB%E7%BB%93%E7%AF%87.html)

