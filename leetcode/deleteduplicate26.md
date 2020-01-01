# delete duplicate 26
给定一个排序数组，你需要在原地删除重复出现的元素，使得每个元素只出现一次，返回移除后数组的新长度。

不要使用额外的数组空间，你必须在原地修改输入数组并在使用 O(1) 额外空间的条件下完成。

示例 1:

给定数组 nums = [1,1,2], 

函数应该返回新的长度 2, 并且原数组 nums 的前两个元素被修改为 1, 2。 

你不需要考虑数组中超出新长度后面的元素。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。
1.双指针
```java
 public int removeDuplicates(int[] nums) {
        //记录第一个重复的位置firstDuplicateindex
        //另一个指针不断向后移动，找到以nums[fdi]不同的值，returnfdi
        int fdi = 0;
        for (int i = 1; i < nums.length; ++ i) {
            if(nums[i] != nums[fdi]){
                nums[++ fdi] = nums[i];
            } 
        }
        return fdi + 1;
    }
```  
