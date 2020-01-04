---
layout: post
title: 快乐数
---

编写一个算法来判断一个数是不是“快乐数”。

一个“快乐数”定义为：对于一个正整数，每一次将该数替换为它每个位置上的数字的平方和，然后重复这个过程直到这个数变为 1，也可能是无限循环但始终变不到 1。如果可以变为 1，那么这个数就是快乐数。

示例: 

输入: 19
输出: true
解释: 
12 + 92 = 82
82 + 22 = 68
62 + 82 = 100
12 + 02 + 02 = 1

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/happy-number
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

快乐数:
### 题解
1.[大佬的解法](https://leetcode-cn.com/problems/happy-number/solution/shi-yong-kuai-man-zhi-zhen-si-xiang-zhao-chu-xun-h/)
``` java
int bitSquareSum(int n) {
    int sum = 0;
    while (n > 0) {
        int bit = n % 10;
        sum += bit * bit;
        n /= 10;
    }
    return sum;
}

public boolean isHappy(int n) {
    int slow = n, fast = n;
    do {
        slow = bitSquareSum(slow);
        fast = bitSquareSum(fast);
        fast = bitSquareSum(fast);
    } while (slow != fast);
    return slow == 1;
}
```  
这里使用的快慢指针,因为无法得到1的数最后都会形成一个环,而对于最后可以得到1的数,1在进行计算还是1,因此,也能保证最后快慢指针能到达同一个位置.
