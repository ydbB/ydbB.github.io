---
layout: post
title: n叉树的前序遍历
---
给定一个 N 叉树，返回其节点值的前序遍历。

例如，给定一个 3叉树 :

 

![](../imgfromleetcode/../../imgfromleetcode/narytreeexample.png)

 

返回其前序遍历: [1,3,5,6,2,4]。

### 题解
1.递归

``` java
public List<Integer> preorder(Node root) {
        List<Integer> res = new ArrayList();
        helper(root, res);
        return res;
    }
    void helper(Node root, List res) {
        //termination
        if (root == null) return;
        //process
        res.add(root.val);
        for (Node node : root.children) {
            helper(node, res);
        }
    }
```  

2.迭代

``` java
public List<Integer> preorder(Node root) {
    List<Integer> res = new ArrayList();
    if (root == null) return res;
    Stack<Node> stack = new Stack();
    stack.push(root);
    while (!stack.isEmpty()) {
        Node visited = stack.pop();
        res.add(visited.val);
        for (int i = visited.children.size() - 1; i >= 0; i--) {
            stack.push(visited.children.get(i));
        }
    }
    return res;
} 
```   
3.另一种递归
```  java
public List<Integer> preorder(Node root) {
    List<Integer> res = new ArrayList();
    //termination
    if (root == null) return res;
    res.add(root.val);
    for (Node child : root.children) {
        res.addAll(preorder(child));
    }
    retrun res;
}
```  

