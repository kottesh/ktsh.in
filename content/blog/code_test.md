+++
title = "Test code syntax highlight"
date = 2020-10-13
draft = true

[taxonomies]
tags=["test", "code"]
+++

```rust
fn factorial(n: u64) -> u64 {
    match n {
        0 => 1,
        _ => n * factorial(n-1)
    }
}
```

```typescript
const sum = (n: number) =>  n * (n + 1) / 2
```

```bash
#this is a comment
$ sudo pacman -Syu

for i in $(seq 1 10); do
    echo "Hello Mars"
done
```

```cpp
#include <iostream>
#include <vector>

struct Node {
    int data;
    Node *left, 
         *right;

    Node(int val) {
        this->data = val; 
        this->left = this->right = nullptr;
    }
};

class BST {
    public:
    Node *root; 
	Node* cloneBinaryTree(Node* root) {
		if (root == nullptr) {
			return nullptr;
		}

		Node* root_copy = new Node(root->data);
		root_copy->left = cloneBinaryTree(root->left);
		root_copy->right = cloneBinaryTree(root->right);
		return root_copy;
	}
    BST() {root = nullptr;}
    void inorder() {
        inorderHelper(root);
    }
    void inorderHelper(Node *root) {
        if(root == nullptr) 
            return;
        inorderHelper(root->left);
        std::cout << root->data << " ";
        inorderHelper(root->right);
    }

    Node *insertHelper(int data, Node *root) {
        if(root == nullptr) {
            return new Node(data);
        }

        if(root->data > data) {
            root->left = insertHelper(data, root->left);
        } else {
            root->right = insertHelper(data, root->right);
        }
        return root;
    }

    void insert(int data) {
        this->root = insertHelper(data, this->root);
    } 

    Node *findMin(Node *temp) {
        while(temp->left !=nullptr) {
            temp = temp->left;
        }
        return temp;
    }

    Node *deleteHeleper(Node *root, int key) {
        if(root == nullptr) {
            return root;
        }

        if(root->data > key) {
            root->left = deleteHeleper(root->left, key);
        } else if(root->data < key) {
            root->right = deleteHeleper(root->right, key);
        } else {
            Node *temp = nullptr;
            if(root->left == nullptr) {
                temp = root->right;
                delete root;
                return temp;
            } else if(root->right == nullptr) {
                temp = root->left;
                delete root;
                return temp;
            } else {
                Node *min = findMin(root->right);
                root->data = min->data;
                root->right = deleteHeleper(root->right, min->data);
            }
        }
        return root;
    } 

    void deleteNode(int key) {
        this->root = deleteHeleper(this->root, key);
    }
};

int main() {

    BST tree;

    tree.insert(5);
    tree.insert(2);
    tree.insert(0);
    tree.insert(1);
    tree.insert(4);

	Node *clone = tree.cloneBinaryTree(tree.root);

    tree.inorderHelper(clone);
    return 0;
}
```

