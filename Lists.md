# Linked Lists

+ [Remove Nth Node From End of List](#remove-nth-node-from-end-of-list)
+ [Merge Two Sorted Lists](#merge-two-sorted-lists)
+ [Linked List Cycle](#linked-list-cycle)
+ [Linked List Cycle II](#linked-list-cycle-ii)
+ [Reorder List](#reorder-list)
+ [Sort List](#sort-list)
+ [Remove Linked List Elements](#remove-linked-list-elements)
+ [Reverse Linked List](#reverse-linked-list)
+ [Palindrome Linked List](#palindrome-linked-list)
+ [Delete Node in a Linked List](#delete-node-in-a-linked-list)
+ [Middle of the Linked List](#middle-of-the-linked-list)
+ [Intersection of Two Linked Lists](#intersection-of-two-linked-lists)

## Remove Nth Node From End of List

https://leetcode.com/problems/remove-nth-node-from-end-of-list/

```C++
class Solution {
public:
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        ListNode* tmp = new ListNode(42), * current = tmp;
        ListNode* endOfList = head;
        ListNode* buf;
        current->next = head;
        while (n--)
          endOfList = endOfList->next;
        while (endOfList) {
          endOfList = endOfList->next;
          current = current->next;
        }
        buf = current->next->next;
        delete current->next;
        current->next = buf;
        return tmp->next;
    }
};
```
## Merge Two Sorted Lists
https://leetcode.com/problems/merge-two-sorted-lists/
```C++
class Solution {
public:
	ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
       if (!l1)
           return l2;
       if (!l2)
           return l1;
       ListNode* buf = new ListNode(0), * current = buf;
       while (l2 && l1) {
           if (l1->val > l2->val) {
               current->next = l2;
               l2 = l2->next;
           }
           else {
               current->next = l1;
               l1 = l1->next;
           }
           current = current->next;
       }
       (l1) ? (current->next = l1) : (current->next = l2);
       return buf->next;
   }
};
```
## Linked List Cycle
https://leetcode.com/problems/linked-list-cycle/
```C++
class Solution {
public:
    bool hasCycle(ListNode *head) {
        if (!head)
            return false;
        ListNode *pSlow = head, *pFast = head->next;
        while (pSlow != pFast){
            if (!pFast || !pFast->next)
                return false;
            pSlow = pSlow->next;
            pFast = pFast->next->next;
        }
        return true;
    }
};
```
## Linked List Cycle II
https://leetcode.com/problems/linked-list-cycle-ii/
```C++
class Solution {
public:
    ListNode *detectCycle(ListNode *head) {
        if (!head)
            return NULL;
        ListNode *pSlow = head, *pFast = head->next;
        while (pSlow != pFast){
            if (!pFast || !pFast->next)
                return NULL;
            pSlow = pSlow->next;
            pFast = pFast->next->next;
        }
        pSlow = head;
        pFast = pFast->next;
        while (!(pSlow == pFast)) {
            pFast = pFast->next;
            pSlow = pSlow->next;
        }
        return pFast;
    }
};
```
## Reorder List
https://leetcode.com/problems/reorder-list/
```C++
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode *prev = NULL, *buf = NULL;
            while (head){
                buf = head->next;
                head->next = prev;
                prev = head;
                head = buf;
            }
            return prev;
        }
    ListNode* middleNode(ListNode* head) {
        ListNode* fast = head, * slow = head;
        while (fast) {
            fast = fast->next;
            if (fast) {
                fast = fast->next;
                slow = slow->next;
            }
        }
        return slow;
    }
    void reorderList(ListNode* head) {
        if (!(head && head->next && head->next->next))
            return;
        ListNode* current = middleNode(head);
        current = reverseList(current);
        ListNode* buf1 = NULL, *buf2 = NULL;
        while (head->next && current->next) {
            buf1 = head->next;
            buf2 = current->next;
            head->next = current;
            current->next = buf1;
            head = buf1;
            current = buf2;
        }
    }
};
```
## Sort List
https://leetcode.com/problems/sort-list/
```C++
class Solution {
public:
   ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
       if (!l1)
           return l2;
       if (!l2)
           return l1;
       ListNode* buf = new ListNode(0), * current = buf;
       while (l2 && l1) {
           if (l1->val > l2->val) {
               current->next = l2;
               l2 = l2->next;
           }
           else {
               current->next = l1;
               l1 = l1->next;
           }
           current = current->next;
       }
       (l1) ? (current->next = l1) : (current->next = l2);
       return buf->next;
   }
    ListNode* middleNode(ListNode* head) {
        ListNode* pFast = head;
        while (pFast) {
            pFast = pFast->next;
            if (pFast && pFast->next) {
                pFast = pFast->next;
                head = head->next;
            }
        }
        pFast = head->next;
        head->next = NULL;
        return pFast;
    }
    ListNode* sortList(ListNode* head) {
        if (!(head && head->next))
            return head;
        return mergeTwoLists(sortList(head), sortList(middleNode(head)));
    }
};
```
## Remove Linked List Elements
https://leetcode.com/problems/remove-linked-list-elements/
```C++
class Solution {
public:
	ListNode* removeElements(ListNode* head, int val) {
	    if (!head)
	        return NULL;
	    ListNode* temp = new ListNode(0);
	    temp->next = head;
	    ListNode* current = temp;
	    ListNode* buf = NULL;
	    while (current->next) {
		   if (current->next->val == val) {
		   	buf = current->next;
		   	current->next = current->next->next;
		   	delete buf;
		   }
            	   else
		   	current = current->next;
	    }
	    buf = temp->next;
            delete temp;
            return buf;
	}
};
```
## Reverse Linked List
https://leetcode.com/problems/reverse-linked-list/
```C++
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode *prev = NULL, *buf = NULL;
        while (head){
            buf = head->next;
            head->next = prev;
            prev = head;
            head = buf;
        }
        return prev;
    }
};
```
## Palindrome Linked List
https://leetcode.com/problems/palindrome-linked-list/
```C++
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        ListNode *prev = NULL, *buf = NULL;
        while (head){
            buf = head->next;
            head->next = prev;
            prev = head;
            head = buf;
        }
        return prev;
    }
    ListNode* middleNode(ListNode* head) {
        ListNode* pFast = head, * pSlow = head;
        while (pFast) {
            pFast = pFast->next;
            if (pFast && pFast->next) {
                pFast = pFast->next;
                pSlow = pSlow->next;
            }
        }
        return pSlow;
    }
    bool isPalindrome(ListNode* head) {
        if (!(head && head->next))
            return true;
        ListNode* current = middleNode(head);
        current = reverseList(current);
        while (current && head){
            if (current->val != head->val)
                return false;
            head = head->next;
            current = current->next;
        }
        return true;
    }
};
```
## Delete Node in a Linked List
https://leetcode.com/problems/delete-node-in-a-linked-list/
```C++
class Solution {
public:
    void deleteNode(ListNode* node) {
        ListNode* buf;
        node->val = node->next->val;
        buf = node->next;
        node->next = node->next->next;
        delete buf;
    }
};
```
## Middle of the Linked List
https://leetcode.com/problems/middle-of-the-linked-list/
```C++
class Solution {
public:
    ListNode* middleNode(ListNode* head) {
        ListNode* pFast = head, * pSlow = head;
	while (pFast) {
	    pFast = pFast->next;
	    if (pFast) {
	        pFast = pFast->next;
	        pSlow = pSlow->next;
	    }
	}
	return pSlow;
    }
};
```
## Intersection of Two Linked Lists
https://leetcode.com/problems/intersection-of-two-linked-lists/
```C++
class Solution {
public:
    ListNode *getIntersectionNode(ListNode *headA, ListNode *headB) {
        if (!headA || !headB)
            return NULL;
        ListNode* pA = headA, *pB = headB;
        while (pA != pB){
            pA = pA->next;
            pB = pB->next;
            if (!pA && !pB)
                return NULL;
            if (!pA)
                pA = headB;
            if (!pB)
                pB = headA;
        }
        return pA;
    }
};
```
