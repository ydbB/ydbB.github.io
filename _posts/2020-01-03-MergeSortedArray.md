---
layout: post
title: 合并两个排好序的数组到第一个数组中(LeetCode 88)
image: /img/hello_world.jpeg
---
给定两个有序整数数组 nums1 和 nums2，将 nums2 合并到 nums1 中，使得 num1 成为一个有序数组。

说明:

初始化 nums1 和 nums2 的元素数量分别为 m 和 n。
你可以假设 nums1 有足够的空间（空间大小大于或等于 m + n）来保存 nums2 中的元素。
示例:

输入:
nums1 = [1,2,3,0,0,0], m = 3
nums2 = [2,5,6],       n = 3

输出: [1,2,2,3,5,6]

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/merge-sorted-array
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。  

{: .box-note}
**Note:** 简单题，不在说明时间复杂度为 O(NM) 的代码。

贴一个时间复杂度为：{O(N + M) 的代码，  
``` java
public void merge(int[] nums1, int m, int[] nums2, int n) {
        int lastIndex = nums1.length - 1;
        int i = n - 1, j = m - 1;
        while ( i >= 0 && j >= 0) {
         if (nums2[i] > nums1[j]) {
             nums1[lastIndex --] = nums2[i --];
         } else nums1[lastIndex --] = nums1[j --];
        }
        while (i >= 0) nums1[lastIndex --] = nums2[i --];
    }
```   

超级简洁版:
``` java
public void merge(int[] nums1, int m, int[] nums2, int n) {
    int i = m - 1, j = n - 1, last = m + n - 1;
    while (i >= 0 && j >= 0) nums1[last --] = nums2[i] > nums1[j] ? nums2[i --] : nums1[j --]; 

    while (j >= 0) nums1[last --] = nums2[j --];
}
```  
