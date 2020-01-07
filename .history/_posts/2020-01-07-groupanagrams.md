---
layout: post
title: 异位词分组
---
//给定一个字符串数组，将字母异位词组合在一起。字母异位词指字母相同，但排列不同的字符串。 
//
// 示例: 
//
// 输入: ["eat", "tea", "tan", "ate", "nat", "bat"],
//输出:
//[
//  ["ate","eat","tea"],
//  ["nat","tan"],
//  ["bat"]
//] 
//
// 说明： 
//
// 
// 所有输入均为小写字母。 
// 不考虑答案输出的顺序。 
// 
// Related Topics 哈希表 字符串

### 题解
1.排序解决
``` java
public List<List<String>> groupAnagrams(String[] strs) {
        List<List<String>> res = new ArrayList<>();
        if (strs == null || strs.length == 0) return res;
        Map<String,List> map = new HashMap();
        for (String str : strs) {
            char[] chars = str.toCharArray();
            Arrays.sort(chars);
            String key = String.valueOf(chars);
            if (!map.containsKey(key)) map.put(key, new ArrayList());
            map.get(key).add(str);
        }
        return new ArrayList(map.values());
}
```   
{: .box-note}
**Note:** 在集合中添加另外一个集合元素时，集合的类型由构造元素决定
可以把一些不必要的尖括号去掉.
.box

2.素数解决
``` java
public List<List<String>> groupAnagrams(String[] strs) {
        Map<Long,List> map = new HashMap();
        for (String str : strs) {
            long k = key(str);
            if (!map.containsKey(k)) map.put(k, new ArrayList());
            map.get(k).add(str);
        }
        List<List<String>> res = new ArrayList();
        for (List list : map.values()) {
            res.add(list);
        }
        return res;
}
 public static long key(String str) {
        long key = 1;
        for (char c : str.toCharArray()){
            int n = c - 'a' + 1;
            key = key * (n * n + n + 41) % Integer.MAX_VALUE;

        }
        //        prime1           *          prime2   *   %MAX_VALUE;
        //key = (s[1]*s[1]+s[1]+41)*(s[2]*s[2]+s[2]+41)*...%MAX_VALUE;
        return key;
    }
```  

{: .box-note}
**Note:** 第二中方法使用了欧拉公式
.box

