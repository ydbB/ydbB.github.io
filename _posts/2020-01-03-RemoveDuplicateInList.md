---
layout: post
title: 删除链表中出现重复值的节点 82
---  
给定一个排序链表，删除所有含有重复数字的节点，只保留原始链表中 没有重复出现 的数字。

示例 1:

输入: 1->2->3->3->4->4->5
输出: 1->2->5
示例 2:

输入: 1->1->1->2->3
输出: 2->3

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list-ii
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。  
### 题解
1.简洁版
```java
public ListNode deleteDuplicates(ListNode head) {
       if (head == null || head.next == null) return head;
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode slow = dummy, fast = head;
        while (fast != null) {
            if((fast.next != null && fast.val !=fast.next.val) || fast.next == null) {
                if (slow.next == fast) slow = fast;
                else slow.next = fast.next;
            }
            fast = fast.next;
        }
        return dummy.next;
    }
```  

2.比较好理解的版本  
``` java
 public ListNode deleteDuplicates(ListNode head) {
        if (head == null) return head;
        ListNode dummy = new ListNode(-1000);
        dummy.next = head;
        ListNode slow = dummy;
        ListNode fast = dummy.next;
        while (fast != null) {
            //把重复的完全删掉
            while (fast.next != null && fast.val == fast.next.val) fast = fast.next;
            //slow 和 fast 相邻(这一遍没有重复)
            if (slow.next == fast) slow = slow.next;
            else slow.next = fast.next;
            fast = fast.next;
        }
        return dummy.next; 
    }
```    

3.递归版本
```java
public ListNode deleteDuplicates(ListNode head) {
    if (head == null) return head;

    if (head.next != null && head.val == head.next.val) {

    while (head.next != null && head.val == head.next.val) head = head.next;

    return deleteDuplicates(head.next);
    } else {
        head.next = deleteDuplicates(head.next);
    }
        return head;

}
```   
