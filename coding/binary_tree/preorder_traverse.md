
### 前序遍历二叉树
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

// 递归前序遍历
void preorderTraversal(TreeNode* node) {
    if (node == NULL) return; // 基本情况：如果当前节点为空，直接返回
    
    cout << node->val << " ";     // 访问当前节点
    preorderTraversal(node->left); // 遍历左子树
    preorderTraversal(node->right); // 遍历右子树
}

// 非递归前序遍历
void preorderTraversal(TreeNode* root) {
    if (root == NULL) return; // 如果根节点为空，直接返回
    
    stack<TreeNode*> stack; // 创建一个栈用于存放节点
    stack.push(root); // 将根节点压入栈

    while (!stack.empty()) {
        TreeNode* node = stack.top(); // 访问栈顶元素
        stack.pop(); // 弹出栈顶元素
        cout << node->val << " "; // 访问节点

        // 重要：先右后左压入栈
        if (node->right != NULL) {
            stack.push(node->right); // 右子节点压入栈
        }
        if (node->left != NULL) {
            stack.push(node->left); // 左子节点压入栈
        }
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

    cout << "Preorder Traversal: ";
    preorderTraversal(root); // 进行前序遍历

    return 0;
}
```
在这个实现中，首先检查根节点是否为空。然后，使用一个栈来跟踪待访问的节点。根节点首先被推入栈。在每次迭代中，从栈中弹出一个节点进行访问，并按照“根-左-右”的顺序推入其子节点。注意，在将子节点压入栈时，先压入右子节点，再压入左子节点。这样做是因为栈是后进先出(LIFO)的数据结构，我们希望左子节点先于右子节点被处理，从而保证了前序遍历的顺序。

通过使用栈，我们能够以非递归的方式模拟递归过程，有效地实现前序遍历。
