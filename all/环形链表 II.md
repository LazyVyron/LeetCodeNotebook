# 环形链表 II
> 找到环的入口

思路：推导暂未整理，先直接套结论，在两个节点初次相遇后，让其中一个回到起点，然后两个以1的速度开始运动，再次相遇的时候是环入口。
**如果链表直接是一整个环，进行head与相遇点判断，相等直接返回该点**
````
        public ListNode detectCycle(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            if (slow == fast){
                fast = head;
                while (slow!=fast){ //这样写while解决了头结点就是环入口的问题
                    slow=slow.next;
                    fast=fast.next;
                    if(slow==fast)
                        return slow;
                }
            }
        }
        return null;
    }
````