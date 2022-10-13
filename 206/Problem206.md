# Problem 206 - Reverse Linked List - Easy
Given the `head` of a singly linked list, reverse the list, and return the reversed list.

 

**Example 1:**

![Example1 Image](rev1ex1.jpg) 
```
Input: head = [1,2,3,4,5]
Output: [5,4,3,2,1]
```
**Example 2:**

![Example2 Image](rev1ex2.jpg)
```
Input: head = [1,2]
Output: [2,1]
```
**Example 3:**
```
Input: head = []
Output: []
```

**Constraints:**

- The number of nodes in the list is the range [0, 5000].
- -5000 <= Node.val <= 5000
 

**Follow up:** A linked list can be reversed either iteratively or recursively. Could you implement both?

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

### 7 ms, 8.4 mb
```
ListNode* reverseList(ListNode* head) {
    ListNode* prevNode = nullptr;
    ListNode* currentNode = head;
    ListNode* nextNode = currentNode;
    
    while(currentNode){
        nextNode = nextNode->next;
        currentNode->next = prevNode;
        prevNode = currentNode;
        currentNode = nextNode;
    }
    
    head = prevNode;
    
    return head;
}
```