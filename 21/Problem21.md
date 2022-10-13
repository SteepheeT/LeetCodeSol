# Problem 21 - Merge Two Sorted List - Easy
You are given the heads of two sorted linked `lists` list1 and `list2`.

Merge the two lists in a **one sorted** list. The list should be made by splicing together the nodes of the first two lists.

Return the head of the merged linked list.

**Example 1:**

![Example 1 Image](../img/21e1.jpg)
```
Input: list1 = [1,2,4], list2 = [1,3,4]
Output: [1,1,2,3,4,4]
```
**Example 2:**
```
Input: list1 = [], list2 = []
Output: []
```
**Example 3:**
```
Input: list1 = [], list2 = [0]
Output: [0]
```

**Constraints:**

* The number of nodes in both lists is in the range [0, 50].

* -100 <= Node.val <= 100
* Both list1 and list2 are sorted in **non-decreasing** order.

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
### 16 ms, 14.8 mb
```
ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
    if(list1 == nullptr) return list2;
    else if(list2 == nullptr) return list1;
    
    ListNode* ans = nullptr, pos = nullptr;

    if(list1->val <= list2->val){
        ans = list1;
        pos = list1;
        if(list1->next != nullptr){
            list1 = list1->next;
        }
        else{
            ans->next = list2;
            return ans;
        }
    }
    else{
        ans = list2;
        pos = list2;
        if(list2->next != nullptr){
            list2 = list2->next;    
        }
        else{
            ans->next = list1;
            return ans;
        }
    }
    
    for(int i = 0; i < 100; i++){
        if(list1->val <= list2->val){
            pos->next = list1;
            list1 = list1->next;
            pos = pos->next;
        }
        else if(list1->val > list2->val){
            pos->next = list2;
            list2 = list2->next;
            pos = pos->next;
        }
        if(list1 == nullptr){
            pos->next = list2;
            break;
        }
        else if(list2 == nullptr){
            pos->next = list1;
            break;
        }
    }

    return ans;   
}
```

### 11 ms, 14.8 mb
```
ListNode* mergeTwoLists(ListNode* list1, ListNode* list2) {
    if(list1 == nullptr) return list2;
    else if(list2 == nullptr) return list1;
    
    ListNode* ans = list1;
    if(list1->val <= list2->val){
        list1 = list1->next;
    }
    else{
        ans = list2;
        list2 = list2->next;
    }
    
    ListNode* pos = ans;
    
    while(list1 && list2){
        if(list1->val <= list2->val){
            pos->next = list1;
            list1 = list1->next;
        }
        else{
            pos->next = list2;
            list2 = list2->next;
        }
        pos = pos->next;
    }
    
    if(list1){
        pos->next = list1;
    }
    else{
        pos->next = list2;
    }
    return ans;
    
}
```