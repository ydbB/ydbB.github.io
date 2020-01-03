---
layout: post
title: 二进制求和
---
给定两个二进制字符串，返回他们的和（用二进制表示）。

输入为非空字符串且只包含数字 1 和 0。

示例 1:

输入: a = "11", b = "1"
输出: "100"
示例 2:

输入: a = "1010", b = "1011"
输出: "10101"

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/add-binary
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。  
### 题解
1,自己写的比较乱的版本
``` java
public String addBinary(String a, String b) {
       int in = 0;
        StringBuilder sb = new StringBuilder();
        int i = a.length() - 1, j = b.length() - 1;
        while (i >= 0 && j >= 0) {
            int sum = (a.charAt(i) - '0' + b.charAt(j) - '0') + in;
            in = sum  / 2;
            sb.append(sum % 2);
            i --; j --;
        }
        while (i >= 0) {
            int sum = (a.charAt(i) - '0') + in;
            in = sum  / 2;
            sb.append(sum % 2);
            i --;
        }
        while (j >= 0) {
            int sum = (b.charAt(j) - '0') + in;
            in = sum  / 2;
            sb.append(sum % 2);
            j --;
        }
        if (in == 1) sb.append(in);
        return sb.reverse().toString();  
    }
```   
 {: .box-note}
 **Note:** 思路:就是小学学到竖式加法.  

 2.大佬的解法(思路相同,但是简洁)  
 ``` java
 public String addBaniry(String a, String b) {
     StringBuilder sb = new StringBuilder();
     int in = 0;
     for (int i = a.length() -1, j = b.length() -1; i >= 0 || j >= 0 || in == 1; i--, j--) {
         int sum = in;
         sum += i >= 0 ? a.charAt(i) - '0' : 0;
         sum += j >= 0 ? b.charAt(j) - '0' : 0;
         sb.append(sum % 2);
         in = sum / 2;
     }
     return sb.reverse().toString();
 }
 ```   
 3.更改版  
 ```java
 public String addBaniry(String a, String b) {
     StringBuilder sb = new StringBuilder();
     int in = 0;
     int i = a.length() - 1, j = b.length() - 1;

     while (i >= 0 || j >= 0 || in == 1) {
         int sum = in;
         sum += i >= 0 ? a.charAt(i) - '0' : 0;
         sum += j >= 0 ? b.charAt(j) - '0' : 0;
         sb.append(sum % 2);
         in = sum / 2;
     }
     return sb.reverse().toString();
 }
 ```   
 
 {: .box-Warning}
 **Warning:** 注意这里不要使用 $\mathtt{sb.append(sum - in)}$ 莫名bug,暂时不理解原因.
