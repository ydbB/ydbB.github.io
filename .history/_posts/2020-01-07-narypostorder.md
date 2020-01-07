---
layout: post
title: n叉树后序遍历
---







### 题解
1. 迭代
``` java
public List<Integer> postorder(Node root) {
    List<Integer> res = new ArrayList();
    Stack<Node> stack = new Stack();

    if (root == null) return res;
    stack.push(root);

    while (!stack.isEmpty()) {
        Node node = stack.pop();
        res.add(node.val);
        for (Node child : node.children) {
            stack.push(child);
        }
     }
     Collections.reverse(res);
     retrun res;
}
```  
2.递归
```  java
public List<Integer> postorder(Node root) {
    List<Integer> res = new ArrayList();
    //termination
    if (root == null) return res;
    for (Node node : root.children) res.addAll(postorder(node));
    res.add(root.val);
    return res;
}
```  