# Reverse Linked List II
## https://leetcode.com/problems/reverse-linked-list-ii

Given the head of a singly linked list and two integers left and right where left <= right, reverse the nodes of the list from position left to position right, and return the reversed list.
```java
Example 1:
Input: head = [1,2,3,4,5], left = 2, right = 4
Output: [1,4,3,2,5]

Example 2:
Input: head = [5], left = 1, right = 1
Output: [5]
``` 

### Constraints:

1. The number of nodes in the list is n.
2. 1 <= n <= 500
3. -500 <= Node.val <= 500
4. 1 <= left <= right <= n

## Implementation :
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode reverseBetween(ListNode head, int left, int right) {
        if(left == right)
          return head;
        int index = 1;
        ListNode curr = head;
        ListNode prev = null;
        while(curr != null && index <= left - 1) {
            prev = curr;
            curr = curr.next;
            index++;
        }
        // curr should point to first node from where we have to reverse, and prev.next == curr
        ListNode leftPtr = prev, startPtr = curr, prevPtr = curr, ptr = curr.next;
        int nodesToReverse = right - left;
        while(nodesToReverse > 0) {
            ListNode tmp = ptr.next;
            ptr.next = prevPtr;
            prevPtr = ptr;
            ptr = tmp;
            nodesToReverse--;
        }
        ListNode rightPtr = ptr;
        // System.out.println("Left PTR : " + leftPtr.val);
        // System.out.println("Start PTR : " + startPtr.val);
        // System.out.println("PTR : "+ prevPtr.val);
        // System.out.println("Right PTR : " + rightPtr.val);
        if(leftPtr != null)
           leftPtr.next = prevPtr;
        startPtr.next = rightPtr;
        return leftPtr != null ? head : prevPtr;
    }
}
```
