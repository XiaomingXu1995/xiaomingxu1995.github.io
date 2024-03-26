
### 非递归方式中序遍历二叉树
```c++
#include <iostream>
#include <stack>
using namespace std;

// 定义二叉树节点结构
struct TreeNode {
    int val;
    TreeNode *left;
    TreeNode *right;
    TreeNode(int x) : val(x), left(NULL), right(NULL) {}
};

// 非递归中序遍历
void inorderTraversal(TreeNode* root) {
    stack<TreeNode*> stack;
    TreeNode* current = root;

    while (current != NULL || !stack.empty()) {
        // 尽可能地向左走，沿途的节点入栈
        while (current != NULL) {
            stack.push(current);
            current = current->left;
        }

        // 当前节点为空，说明到达了最左边，开始回溯
        current = stack.top();
        stack.pop();
        cout << current->val << " ";  // 访问节点

        // 转向右子树
        current = current->right;
    }
}

int main() {
    // 构建一个简单的测试二叉树
    //       1
    //      / \
    //     2   3
    //    / \
    //   4   5
    TreeNode *root = new TreeNode(1);
    root->left = new TreeNode(2);
    root->right = new TreeNode(3);
    root->left->left = new TreeNode(4);
    root->left->right = new TreeNode(5);

    cout << "Inorder Traversal: ";
    inorderTraversal(root);

    return 0;
}

```

