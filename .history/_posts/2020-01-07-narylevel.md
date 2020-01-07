---
layout: post
title: n叉树层次遍历
---
给定一个 N 叉树，返回其节点值的层序遍历。 (即从左到右，逐层遍历)。

例如，给定一个 3叉树 :

 


![tu](/imgfromleetcode/narytreeexample.png)
 

返回其层序遍历:

[
     [1],
     [3,2,4],
     [5,6]
]
 

说明:

树的深度不会超过 1000。
树的节点总数不会超过 5000。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/n-ary-tree-level-order-traversal
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

### 题解

``` java
private List<List<Integer>> res = new ArrayList();
public List<List<Integer>> levelOrder(Node root) {
    if (root == null) return res;
    helper(root, 0);
    return res;
}

private void helper(Node root, int level) {
    if (res.size() <= level) {
        res.add(new ArrayList());
    }
    res.get(level).add(root.val);
    for (Node child : root.children) {
        helper(child, level + 1);
    }
}
```  
2.迭代

``` java
public List<List<Integer>> levelOrder(Node root) {
    List<List<Integer>> res = new ArrayList();
    if (root == null) return res;
    Queue<Node> queue = new LinkedList();
    queue.offer(root);
    
    while (!queue.isEmpty()) {
        List<Integer> curList = new LinkedList();
        int len = queue.size();
        for (int i = 0; i < len; i++) {
            Node cur = queue.poll();
            curList.add(cur.val);
            for (Node c : cur.children) queue.offer(c);
        }
        res.add(curList);
    }
    return res;
}
```   
