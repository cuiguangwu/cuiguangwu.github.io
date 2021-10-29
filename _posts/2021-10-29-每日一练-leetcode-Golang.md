2. Add Two Numbers（https://leetcode.com/problems/add-two-numbers/）
Medium

14539

3202

Add to List

Share
You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order, and each of their nodes contains a single digit. Add the two numbers and return the sum as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

 

Example 1:


Input: l1 = [2,4,3], l2 = [5,6,4]
Output: [7,0,8]
Explanation: 342 + 465 = 807.
Example 2:

Input: l1 = [0], l2 = [0]
Output: [0]
Example 3:

Input: l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
Output: [8,9,9,9,0,0,0,1]
 

Constraints:

The number of nodes in each linked list is in the range [1, 100].
0 <= Node.val <= 9
It is guaranteed that the list represents a number that does not have leading zero
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
 //代码
 、、、
func addTwoNumbers(l1 *ListNode, l2 *ListNode) *ListNode {
    head := new(ListNode)
    cnt := 0
    pNode := head
    for l1!=nil && l2!=nil{
        node := new(ListNode)
        node.Val = (cnt + (l1.Val + l2.Val)) % 10
        cnt = (cnt + (l1.Val + l2.Val)) / 10
        pNode.Next = node
        pNode = node
        l1 = l1.Next
        l2 = l2.Next
    }
    for l1!=nil{
        node := new(ListNode)
        node.Val = (cnt + l1.Val) % 10
        cnt = (cnt + l1.Val) / 10
        pNode.Next = node
        pNode = node
        l1 = l1.Next
    }
    for l2!=nil{
        node := new(ListNode)
        node.Val = (cnt + l2.Val) % 10
        cnt = (cnt + l2.Val) / 10
        pNode.Next = node
        pNode = node
        l2 = l2.Next
    }
    if cnt!=0 {
        node := new(ListNode)
        node.Val = cnt
        pNode.Next = node
    }
    head = head.Next
    return head
}
、、、
