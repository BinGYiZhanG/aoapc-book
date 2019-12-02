* [题解](https://blog.csdn.net/x603560617/article/details/87966145)

```
/*
// Definition for a Node.
class Node {
public:
    int val;
    Node* left;
    Node* right;
    Node* next;

    Node() : val(0), left(NULL), right(NULL), next(NULL) {}

    Node(int _val) : val(_val), left(NULL), right(NULL), next(NULL) {}

    Node(int _val, Node* _left, Node* _right, Node* _next)
        : val(_val), left(_left), right(_right), next(_next) {}
};
*/
class Solution {
public:
    Node* connect(Node* root) {
        if (!root) return NULL;//
        Node *p = root->next;
        while(p){
            if (p->left){//若左子树存在，
                p = p->left;
                break;
            }
            if(p->right){
                p = p->right;
                break;
            }
            p = p->next;
        }
        /*
        //右子树的next指针指向
            root的next指针的左孩子，或者右孩子,
            或者root的next的next指针的左右孩子
        */
        if (root->right) 
            root->right->next = p;
        /*
        //如果root的左孩子存在，则让其指向
            root的右孩子，
            或者next指针的左右孩子,
        
        */
        
        if (root->left) root->left->next = root->right?root->right:p;
        connect(root->right);
        connect(root->left);
        return root;

    }
};

```
