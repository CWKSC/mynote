# C++

```c++
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
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode* current, *recordStart;
        current = recordStart = new ListNode();
        while(l1 || l2){
            int value = 0;
            int carry = 0;
            if(l1){
                value += l1->val;
                l1 = l1->next;
            }
            if(l2){
                value += l2->val;
                l2 = l2->next;
            }
            current->val += value;
            if(current->val >= 10){
                current->val -= 10;
                carry++;
            }
            if(carry != 1 && l1 == nullptr && l2 == nullptr) break;
            current->next = new ListNode(carry);
            current = current->next;
        }
        return recordStart;
    }
};
```

