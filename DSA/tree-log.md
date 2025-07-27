```
📅 Date: 25th July  
📘 Topic: Tree Traversals (Inorder, Preorder, Postorder, Level Order)
Reference:Video lecture (https://www.youtube.com/watch?v=5NiXlPrLslg&list=PLDzeHZWIZsTo87y1ytEAqp7wYlEP3nner)
Question: Leetcode(inorder,preorder,postorder)

-----------------------------------------------------
🌳 Tree Traversal Summary:

1. 🔵 Inorder Traversal (LNR)
   Left → Node → Right
   ➤ Code:
   void inorder(TreeNode* root) {
       if(root == NULL) return;
       inorder(root->left);
       cout << root->val << " ";
       inorder(root->right);
   }

2. 🟢 Preorder Traversal (NLR)
   Node → Left → Right
   ➤ Code:
   void preorder(TreeNode* root) {
       if(root == NULL) return;
       cout << root->val << " ";
       preorder(root->left);
       preorder(root->right);
   }

3. 🔴 Postorder Traversal (LRN)
   Left → Right → Node
   ➤ Code:
   void postorder(TreeNode* root) {
       if(root == NULL) return;
       postorder(root->left);
       postorder(root->right);
       cout << root->val << " ";
   }

4. 🟡 Level Order Traversal (BFS)
   Level by Level → Left to Right
   ➤ Code:
   void levelOrder(TreeNode* root) {
       if(root == NULL) return;
       queue<TreeNode*> q;
       q.push(root);
       while(!q.empty()) {
           TreeNode* node = q.front(); q.pop();
           cout << node->val << " ";
           if(node->left) q.push(node->left);
           if(node->right) q.push(node->right);
       }
   }

-----------------------------------------------------
📝 Notes:
- Base case: if root == NULL → return;
- DFS Traversals → Recursive
- BFS Traversal → Queue used
- Jahan "N" hota hai → wahi pe print hota hai
- "L" = call to left subtree, "R" = call to right subtree
```
