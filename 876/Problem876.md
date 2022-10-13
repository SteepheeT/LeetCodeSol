# Problem 876 - Middle of the linked list - Easy
Given the `head` of a singly linked list, return the *middle node of the linked list*.

If there are two middle nodes, return the **second middle** node.

**Example 1:**

![Example1](lc-midlist1.jpg)
```
Input: head = [1,2,3,4,5]
Output: [3,4,5]
Explanation: The middle node of the list is node 3.
```
**Example 2:**

![Example2](lc-midlist2.jpg)
```
Input: head = [1,2,3,4,5,6]
Output: [4,5,6]
Explanation: Since the list has two middle nodes with values 3 and 4, we return the second one.
```

Constraints:

- The number of nodes in the list is in the range `[1, 100]`.
- `1 <= Node.val <= 100`

---
## Solution - C++
### Node Definition
```
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
```

### 0 ms, 7 mb
```
ListNode* middleNode(ListNode* head) {
    if(!head)
        return head;
    int length = 0;
    ListNode* current = head;
    while(current){
        length++;
        current = current->next;
    }
    if(length % 2 == 1){
        length--;
    }
    length /= 2;
    
    for(int i=0; i<length; i++){
        head = head->next;
    }
    return head;
}
```