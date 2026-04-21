Base case is always if (!root) return — write this first, always

class TreeNode
{
    int val;
    TreeNode* left;
    TreeNode* right;

    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
}



void preorder(TreeNode& root, vector<int> result)
{
    if(!root) return;

    result.push_back(root->val);
    preorder(root->left, result);
    preorder(root->right, result);
}