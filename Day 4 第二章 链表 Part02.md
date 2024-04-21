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
[题目链接]()
[文章讲解]()
[视频讲解]()

## 面试题 02.07. 链表相交
[题目链接]()
[文章讲解]()
[视频讲解]()

## 142.环形链表II 
[题目链接]()
[文章讲解]()
[视频讲解]()

## 总结
[文章讲解]()

