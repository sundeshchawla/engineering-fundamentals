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
    ListNode* reverseList(ListNode* head) {
        ListNode* leader = head;
        ListNode* follower = NULL;

        while(leader != NULL)
        {
            ListNode* temp = leader->next;

            leader->next = follower;
            follower = leader;
            leader = temp;
        }

        return follower;
    }
};