Base case is always if (!root) return — write this first, always

class TreeNode
{
    int val;
    TreeNode* left;
    TreeNode* right;

    TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
}



void postorder(TreeNode& root, vector<int> result)
{
    if(!root) return;

    postorder(root->left, result);
    postorder(root->right, result);
    result.push_back(root->val);
}