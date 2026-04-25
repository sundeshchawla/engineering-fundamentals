Base case is always if (!root) return — write this first, always

class TreeNode
{
    int val;
    TreeNode* left;
    TreeNode* right;

    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
}



void inorder(TreeNode& root, vector<int> result)
{
    if(!root) return;

    inorder(root->left, result);
    result.push_back(root->val);
    inorder(root->right, result);
}