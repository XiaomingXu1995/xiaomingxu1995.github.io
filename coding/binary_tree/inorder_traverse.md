
### 中序遍历二叉树
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

// 递归中序遍历
void inorderTraversal(TreeNode* node) {
    if (node == NULL) {
        return; // 基本情况：如果当前节点为空，直接返回
    }
    inorderTraversal(node->left); // 遍历左子树
    cout << node->val << " ";     // 访问当前节点
    inorderTraversal(node->right); // 遍历右子树
}

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
这段代码定义了一个`TreeNode`结构来表示二叉树的节点，每个节点包含一个整数值、一个指向左子节点的指针和一个指向右子节点的指针。`inorderTraversal`函数实现了非递归的中序遍历。在这个函数中，我们使用一个栈来暂存节点，先尽量深入树的左侧，然后依次访问节点并转向右侧。

注意，这个示例只是实现了中序遍历的功能，实际应用中可能需要根据具体需求进行相应的调整。
