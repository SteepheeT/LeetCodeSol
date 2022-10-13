# Problem 142 - Linked List Cycle II - Medium
Given the `head` of a linked list, return *the node where the cycle begins. If there is no cycle, return* `null`.

There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the `next` pointer. Internally, `pos` is used to denote the index of the node that tail's `next` pointer is connected to **(0-indexed)**. 

It is `-1` if there is no cycle. **Note that**`pos` **is not passed as a parameter.**

**Do not modify** the linked list.

 

**Example 1:**

![Example1](circularlinkedlist.png)

```
Input: head = [3,2,0,-4], pos = 1
Output: tail connects to node index 1
Explanation: There is a cycle in the linked list, where tail connects to the second node.
```
**Example 2:**

![Example2](circularlinkedlist_test2.png)

```
Input: head = [1,2], pos = 0
Output: tail connects to node index 0
Explanation: There is a cycle in the linked list, where tail connects to the first node.
```
**Example 3:**

![Example3](circularlinkedlist_test3.png)

```
Input: head = [1], pos = -1
Output: no cycle
Explanation: There is no cycle in the linked list.
```

**Constraints:**

- The number of the nodes in the list is in the range `[0, 104]`.
- `-105 <= Node.val <= 105`
- `pos` is `-1` or a **valid index** in the linked-list.
 

**Follow up:** Can you solve it using O(1) (i.e. constant) memory?

---
## Solution - C++
- Normal solution, uses unordered map and register any nodes appeared while traverse.
- If the current visited node is registered inside the map, then there's a loop and the current node is the beginning of the loop.
- Otherwise, we will reach the end of the list, and thus return `null`.
### 37 ms, 10 mb
```
ListNode *detectCycle(ListNode *head) {
    unordered_map<ListNode*, bool> mp;
    while(head){
        if(mp.count(head)){
            return head;
        }
        else{
            mp[head] = true;
            head = head->next;
        }
    }
    return nullptr;
}
```

### 27 ms, 7.6 mb
- Using two different pointers, `fp` travels 2 steps a time; `sp` travels 1 step a time.
- If both of them starts from the beginning, by the time they meet, `fp` will travel **exactly 2 times** of the `sp`'s travel distance. *i.e. if `sp` went **m** distance, then `fp` went **2m**.*
- If there's no loop, `fp` will reach the end of the list and thus we return `null`
- Otherwise, we got a loop. We not reset the `sp` to head, then ask `fp` and `sp` to both move 1 step at a time.
- They will eventually meet at the beginning of the loop
```
ListNode *detectCycle(ListNode *head) {
    if(!head || !head->next){
        return nullptr;
    }
    bool found = false;
    ListNode* fast = head;
    ListNode* slow = head;
    while(fast->next && fast->next->next){
        slow = slow->next;
        fast = fast->next->next;
        if(slow == fast){
            found = true;
            break;
        }
    }
    if(!found){
        return nullptr;
    }
    
    slow = head;
    while(slow != fast){
        slow = slow->next;
        fast = fast->next;
    }
    return slow;
}
```

### 12 ms, 7.6 mb
- Improve version of the previous code, removed bool cycle indicator, adjust second loop's position

```
ListNode *detectCycle(ListNode *head) {
    if(!head || !head->next){
        return nullptr;
    }
    
    ListNode* fast = head;
    ListNode* slow = head;
    while(fast->next && fast->next->next){
        slow = slow->next;
        fast = fast->next->next;
        if(slow == fast){
            slow = head;
            while(slow != fast){
                slow = slow->next;
                fast = fast->next;
            }
            return slow;
        }
    }
    return nullptr;
}
```