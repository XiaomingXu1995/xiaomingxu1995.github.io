
### 后序遍历二叉树
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

// 递归后序遍历
void postorderTraversal(TreeNode* node) {
    if (node == NULL) return; // 基本情况：如果当前节点为空，直接返回
    
    postorderTraversal(node->left); // 遍历左子树
    postorderTraversal(node->right); // 遍历右子树
    cout << node->val << " ";     // 访问当前节点
}

// 非递归后序遍历
void postorderTraversal(TreeNode* root) {
    stack<TreeNode*> stack;
    TreeNode *current = root;
    TreeNode *lastVisited = NULL;

    while (current != NULL || !stack.empty()) {
        // 尽可能地向左走，并将沿途的节点入栈
        while (current != NULL) {
            stack.push(current);
            current = current->left;
        }

        // 查看栈顶元素
        current = stack.top();

        // 如果当前节点的右子树为空或已被访问，则可以访问当前节点
        if (current->right == NULL || current->right == lastVisited) {
            cout << current->val << " "; // 访问节点
            stack.pop(); // 将节点出栈
            lastVisited = current; // 更新最后访问的节点
            current = NULL; // 重置当前节点
        } else {
            // 否则，转向访问右子树
            current = current->right;
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

    cout << "Postorder Traversal: ";
    postorderTraversal(root); // 进行后序遍历

    return 0;
}
```

这个方法的关键是维护一个`lastVisited`节点变量来追踪最近访问过的节点。这个变量帮助我们判断一个节点的右子节点是否已经被访问过。如果当前节点的右子树为空或者右子树已经被访问，那么就可以安全地访问当前节点。在访问完当前节点后，我们需要将`lastVisited`更新为当前节点，并将`current`设置为`NULL`，这样在下一次循环中，我们会从栈顶节点继续执行。

通过这种方式，我们能够在不使用递归的情况下实现二叉树的后序遍历。
