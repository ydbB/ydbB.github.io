---
layout: post
title: 柱状图中的最大面积
---
给定 n 个非负整数，用来表示柱状图中各个柱子的高度。每个柱子彼此相邻，且宽度为 1 。

求在该柱状图中，能够勾勒出来的矩形的最大面积。

 

 
![img](../imgfromleetcode/84.png)

以上是柱状图的示例，其中每个柱子的宽度为 1，给定的高度为 [2,1,5,6,2,3]。

 
![img](../imgfromleetcode/83_area.png)


图中阴影部分为所能勾勒出的最大矩形面积，其面积为 10 个单位。


示例:

输入: [2,1,5,6,2,3]
输出: 10

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/largest-rectangle-in-histogram
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。  
### 题解

1.枚举边界 i, j,在找其中的最小值.
```java
 public static int largestRectangleArea(int[] height) {
     int max = 0;
     for (int i = 0; i < height.length - 1; i++) {
         for (int j = i + 1; j < height.length; j++) {
             int min = Integer.MAX.VALUE;
            for (int k = i; k <= j; k++) {
                min = Math.min(min,height[k]);
            }
            max = Math.max(max,min * (j - i + 1));
         }
     }
     return max;
 }
 ```   

 {: .box-note}
 **Note:** 这里的时间复杂度为 O(n ^ 3) 会超时. 


 2.优化版枚举边界  
 ``` java
public static int largestRectangleArea(int[] height) {
    int max = 0;
    for (int i = 0; i < height.length - 1; i++) {
        int min = Integer.MAX_VALUE;
        for (int j = i; j < height.length; j++) {
            min = Math.min(min,height[j]);
            max = Math.max(max, (j - i + 1) * min);
        }
    }
    return max;
}
```  

{: .box-note}
**Note:** 时间复杂度为 O(n ^ 2) 

3.枚举最小值点
```java
public static int largestRectangleArea(int[] height) {
    int max = 0;
    for (int i = 0; i < height; ++ i) {
        int left = i - 1, right = i + 1;
        while (left >=0 && height[left] >= height[i]) left --;
        while (right < height && height[right] >= height[i]) right ++;
        max = Math.max(max, (right - left - 1) * height[i]); 
    }

    return max;
}
```  

{: .box-note}
**Note:** 时间复杂度为 $\mathbf{O(n ^ 2)}$  

4.栈的方式
```java
 public static int largestRectangleArea(int[] height) {
   Stack<Integer> stack = new Stack<>();
    stack.push(-1);
    int max = 0;
    //area = height[stack.pop] * (i - stack.peek() - 1)
    for (int i = 0; i < height.length; ++ i) {
        //弹出比height[i] 大的部分
        while (stack.peek() != -1 && height[stack.peek()] >= height[i]) {
            max = Math.max(max, height[stack.pop()] * (i - stack.peek() - 1));
        }
        stack.push(i);
    }

    //清空栈,并计算其中的值
    while (stack.peek() != -1) {
        max = Math.max(max, height[stack.pop()] * (height.length - stack.peek() - 1));
    }
    return max;
}
```   

{: .box-note}
**Note:** 时间复杂度为 O(n)


5.用数组替换栈
```java
public static int largestRectangleArea(int[] height) {
    if (height == null || height.length == 0) return 0;
    int len = height.length;
    int[] leeFromLeft = new int[len];//记录比height[i]的第一个数
    int[] leeFromRight = new int[len];//记录比height[i]大的最后一个数
    lessFromRight[len - 1] = len;
    lessFormLeft[0] = -1;

    for (int i = 1; i < len; i++) {
        int p = i - 1;
        while (p >= 0 && leeFromLeft[p] >= height[i]) p = leeFromLeft[p];
        lessFormLeft[i] = p;
    }

    for (int i = len - 2; i >= 0; i--) {
        int p = i + 1;
        while (p < len && leeFromLeft[p] >= height[i]) p = leeFromLeft[p];
        lessFormLeft[i] = p;
    }

    int max = 0;
    for (int i = 0; i < len; i++) {
        max = Math.max(max,(lessFromRight[i] - lessFormLeft[i] - 1) * height[i]) ;
    }
    return max;
}
```  

{: .box-note}
**Note:** 时间复杂度为 O(n) 


{: .box-warning}
**Warning:** 这个题还需要多看,多理解.  

参考
[官方题解](https://leetcode-cn.com/problems/largest-rectangle-in-histogram/solution/zhu-zhuang-tu-zhong-zui-da-de-ju-xing-by-leetcode/)
