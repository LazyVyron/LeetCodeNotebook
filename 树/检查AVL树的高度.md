# 检查AVL树的高度是否符合定义

> 第一思路的想法是直接比较左子树和右子树的高度差，在这个过程中有很多重复的计算，所以可以设置一个flag，当遇到不满足的子情况时，记录下来，一遍检查即可。

````
boolean flag = true; //用来记录是否有子情况不符合要求
public boolean isBalanced(TreeNode root) {
    if(root == null)
        return true;
    getDepth(root);
    return flag;   
}
public int getDepth(TreeNode node){
    if(node == null)
        return 0;
    int left = getDepth(node.left);
    int right = getDepth(node.right);
    if(Math.abs(left - right ) > 1)
        flag = false;//此时已经检查出不合格了，等到递归栈结束就直接返回了
    return Math.max(left,right)+1;
}
````