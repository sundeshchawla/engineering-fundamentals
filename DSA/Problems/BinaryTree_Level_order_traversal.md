My code

/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        if (root == NULL) return {};
        
        queue<TreeNode*> traverse1;
        queue<TreeNode*> tempqueue;

        traverse1.push(root);

        vector<vector<int>> finalres;

        while(!traverse1.empty())
        {
            vector<int> res;

            while(!traverse1.empty())
            {
                auto curr = traverse1.front();
                traverse1.pop();

                if(curr->left != NULL) tempqueue.push(curr->left);

                if(curr->right != NULL) tempqueue.push(curr->right);

                res.push_back(curr->val);
            }

            swap(traverse1, tempqueue);
            finalres.push_back(res);
        }

        return finalres;
    }
};




GPT code

class Solution {
public:
    vector<vector<int>> levelOrder(TreeNode* root) {
        if (!root) return {};

        queue<TreeNode*> q;
        q.push(root);

        vector<vector<int>> result;

        while (!q.empty()) {
            int size = q.size();
            vector<int> level;

            for (int i = 0; i < size; i++) {
                TreeNode* curr = q.front();
                q.pop();

                level.push_back(curr->val);

                if (curr->left) q.push(curr->left);
                if (curr->right) q.push(curr->right);
            }

            result.push_back(level);
        }

        return result;
    }
};