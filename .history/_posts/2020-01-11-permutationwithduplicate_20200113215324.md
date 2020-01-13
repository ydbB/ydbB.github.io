---
layout: post
title: 全排列II
subtitle: wu
---
给定一个可包含重复数字的序列，返回所有不重复的全排列。

示例:

输入: [1,1,2]
输出:
[
  [1,1,2],
  [1,2,1],
  [2,1,1]
]

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/permutations-ii
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解

1.迭代

~~~ java
    private List<List<Integer>> res = new ArrayList<>();
    private boolean[] used;
    private void findPermuteUnique(int[] nums, int depth, Stack<Integer> stack) {
        if (depth == nums.length) {
            res.add(new ArrayList<Integer>(stack));
            return;
        }

        for (int i=0;i<nums.length;++i) {
            if (!used[i]) {
                if (i > 0 &&  nums[i] == nums[i-1] && !used[i-1]) continue;

                used[i] = true;
                stack.push(nums[i]);
                findPermuteUnique(nums, depth+1, stack);
                stack.pop();
                used[i] = false;
            }
        }
    }

    public List<List<Integer>> permuteUnique(int[] nums) {
        if (nums == null || nums.length < 0) return res;
        Arrays.sort(nums);
        used = new boolean[nums.length];
        findPermuteUnique(nums, 0, new Stack<Integer>());
        return res;
    }
~~~   

2. dfs

~~~ java
public List<List<Integer>> permuteUnique(int[] nums) {
            List<List<Integer>> res = new ArrayList<>();
        if (nums == null || nums.length < 0) return res;
        boolean[] used = new boolean[nums.length];
        Arrays.sort(nums);
        dfs(nums, used, new ArrayList<Integer>(), res);
        return res;
    }

    public void dfs(int[] nums, boolean[] used,
                    List<Integer> list,
                    List<List<Integer>> res) {
        if (list.size() == nums.length) {
            res.add( new ArrayList<Integer>(list));
            return;
        }

        for (int i=0;i<nums.length;++i) {
            if (used[i]) continue;
            if (i > 0 && nums[i] == nums[i-1] && !used[i-1]) continue;

            used[i] = true;
            list.add(nums[i]);
            dfs(nums,used,list,res);
            used[i] = false;
            list.remove(list.size()-1);
        }

    }
~~~  
