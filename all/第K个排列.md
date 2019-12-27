# 第K个排列
> 给出集合 [1,2,3,…,n]，其所有元素共有 n! 种排列。  
按大小顺序列出所有排列情况，并一一标记，当 n = 3 时, 所有排列如下："123""132""213""231""312""321"给定 n 和 k，返回第 k 个排列。

思路：康拓逆展开  
知识补充：康托展开是用来计算第k个组合是什么的。

有一个关键的数组，{1, 1, 2, 6, 24, 120, 720, 5040, 40320, 362880, 3628800};这分别对应的是0!,1! ......10!。因为题目给的范围是1~9，所以写的是这些。

以12345为例子，求他的第62个排序。答案是34152.已知总排列数是5！，显然第5！个排列是54321。要求的数是小于5！的。**首先62-1=61。**第62个排列用61/4!,得2余13.这意味着第一个数字前面有2个数比他小，所以是3.然后用13去除以3！，得到2余1.所以第二个数字前面有2个数字比他小，所以排列的第二位是4（因为3已经使用过）.用1去除以2！，得到0余1，所以他前面比他小的数有0个，所以排列的第三位是1.余数1/1！得1余0，所以比他小的数前面有1个，所以是5，最后剩下1，所以是34152

代码如下

````
class Solution {
    // 康托逆展开
    public String getPermutation(int n, int k) {
        // 把[1,2,3·····n]转化为字符串
        StringBuffer s = new StringBuffer();
        for (int i = 0; i < n; i++) {
            s.append(i + 1);
        }
        char[] origin = s.toString().toCharArray();
        // k-1
        k=k-1;
        //用于康托展开的取余
        int[] factorial = {1, 1, 2, 6, 24, 120, 720, 5040, 40320, 362880, 3628800};
        //存储结果
        StringBuffer result = new StringBuffer();
        boolean[] used = new boolean[n];
        for (boolean b : used) b = false;
        int index;
        for (int i = 0; i < n; i++) {
            index = getIndex(1+k/factorial[n-i-1], used);
            used[index] = true;
            result.append(origin[index]);
            k %= factorial[n-i-1];
        }
        return result.toString();
    }

    // 找到第total个没用过的数字
    public int getIndex(int n, boolean[] used) {
        for (int i = 0, count = 0; i < used.length; i++) {
            if (!used[i])
                count++;
            if (count == n)
                return i;
        }
        //正常情况下是到不了这一步的
        return used.length-1;
    }
}
````