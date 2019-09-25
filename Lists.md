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
    int ListSize(ListNode* head) {
		int size = 0;
		while (head) {
			head = head->next;
			size++;
		}
		return size;
	}
    ListNode* removeNthFromEnd(ListNode* head, int n) {
        if (!head)
			return NULL;
		ListNode* fic = new ListNode(0);
        ListNode* buf = NULL;
		fic->next = head;
		ListNode* q = fic;
        for (int i = ListSize(head) - n; i > 0; i--)
            q = q->next;
        buf = q->next;
        q->next = q->next->next;
        delete buf;
        buf = fic->next;
        delete fic;
        return buf;
        
    }
};
```
## Merge Two Sorted Lists
https://leetcode.com/problems/merge-two-sorted-lists/
```C++
class Solution {
public:
	ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
		ListNode* f = l1, * s = l2;
		if (!f)
			return s;
		if (!s)
			return f;
		ListNode* g = new ListNode(42), * buf = g;
		while (s && f) {
			if (f->val > s->val) {
				buf->next = s;
				s = s->next;
			}
			else {
				buf->next = f;
				f = f->next;
			}
			buf = buf->next;
		}
		(f) ? (buf->next = f) : (buf->next = s);
		return g->next;

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
        ListNode *slow = head, *fast = head->next;
        while (!(slow == fast)){
            if (!fast || !fast->next)
                return false;
            slow = slow->next;
            fast = fast->next->next;
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
        ListNode *slow = head, *fast = head->next;
        while (!(slow == fast)){
            if (!fast || !fast->next)
                return NULL;
            slow = slow->next;
            fast = fast->next->next;
        }
        slow = head;
        fast = fast->next;
        while (!(slow == fast)) {
            fast = fast->next;
            slow = slow->next;
        }
        return fast;
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
        if (!head || !head->next || !head->next->next)
            return;
        ListNode* q = middleNode(head);
        q = reverseList(q);
        ListNode* buf1 = NULL, *buf2 = NULL;
        while (head->next && q->next) {
            buf1 = head->next;
            buf2 = q->next;
            head->next = q;
            q->next = buf1;
            head = buf1;
            q = buf2;
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
		ListNode* f = l1, * s = l2;
		if (!f)
			return s;
		if (!s)
			return f;
		ListNode* g = new ListNode(42), * buf = g;
		while (s && f) {
			if (f->val > s->val) {
				buf->next = s;
				s = s->next;
			}
			else {
				buf->next = f;
				f = f->next;
			}
			buf = buf->next;
		}
		(f) ? (buf->next = f) : (buf->next = s);
		return g->next;

	}
    ListNode* middleNode(ListNode* head) {
        ListNode* fast = head->next;
        while (fast) {
            fast = fast->next;
            if (fast) {
                fast = fast->next;
                head = head->next;
            }
        }
        fast = head->next;
        head->next = NULL;
        return fast;
    }
    ListNode* sortList(ListNode* head) {
        if (!head || !head->next)
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
		ListNode* fic = new ListNode(0);
		fic->next = head;
		ListNode* q = fic;
		ListNode* buf = NULL;
		while (q->next) {
			if (q->next->val == val) {
				buf = q->next;
				q->next = q->next->next;
				delete buf;
			}
            else
                q = q->next;
		}
		buf = fic->next;
        delete fic;
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
    int ListSize(ListNode* head) {
		int size = 0;
		while (head) {
			head = head->next;
			size++;
		}
		return size;
	}
    bool isPalindrome(ListNode* head) {
        if (!head || !head->next)
            return true;
        ListNode* q = middleNode(head);
        if (ListSize(head) % 2) {
            q->next = reverseList(q->next);
            q = q->next;
        }
        else 
            q = reverseList(q);
        while (q){
                if (q->val != head->val)
                    return false;
                head = head->next;
                q = q->next;
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
        ListNode* buf(0);
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
        while (!(pA == pB)){
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
