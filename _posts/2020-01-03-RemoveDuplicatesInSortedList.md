--- 
lyout: post
title: 从排序链表中删除重复节点
--- 
给定一个排序链表，删除所有重复的元素，使得每个元素只出现一次。

示例 1:

输入: 1->1->2
输出: 1->2
示例 2:

输入: 1->1->2->3->3
输出: 1->2->3

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。  
### 题解
```java
 public ListNode deleteDuplicates(ListNode head) {
         if (head == null || head.next == null) return head;
        ListNode node = head;
        while (node != null && node.next != null) {
            if (node.val == node.next.val) node.next = node.next.next;
            else slow = node.next;
        }
        return head;
    }
```    
看来大佬的代码改进的代码(去重了多余的指针):  
```java
public ListNode deleteDuplicates(ListNode head) {
    if (head == null || head.next == null) return head;

    ListNode node = head;

    while (node.next != null) {
        if (node.val == node.next.val) node.next = node.next.next;
        else node = node.next;
    }
    return head;
}
```  
