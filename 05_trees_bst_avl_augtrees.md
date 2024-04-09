[[_main|<-- Back to main]]
# BST/AVL
```c
// Returns updated node height
template <typename T> int _insert_update_height(Node<T> *current) {
  int left_height = current->left ? current->left->height : -1;
  int right_height = current->right ? current->right->height : -1;
  return MAX(left_height, right_height) + 1;
}

// Right rotation for balancing
template <typename T> Node<T>* _insert_right_rotate(Node<T>* target) {
    Node<T>* pivot = target->left;
    Node<T>* subtree = pivot->right;

    pivot->right = target;
    target->left = subtree;

    target->height = _insert_update_height(target);
    pivot->height = _insert_update_height(pivot);
	return pivot;
}

// Left rotation for balancing
template <typename T> Node<T>* _insert_left_rotate(Node<T>* target) {
    Node<T>* pivot = target->right;
    Node<T>* subtree = pivot->left;

    pivot->left = target;
    target->right = subtree;
    
    target->height = _insert_update_height(target);
    pivot->height = _insert_update_height(pivot);
    return pivot;
}

// Returns balance factor of a node
template <typename T> int _insert_get_balance(Node<T>* node) {
  if (node == nullptr) return 0;
  int left_height = node->left ? _insert_update_height(node->left) : -1;
  int right_height = node->right ? _insert_update_height(node->right) : -1;
  return left_height - right_height;
}

// Helper function for insert
template <typename T> Node<T> *_insert(Node<T> *current, Node<T> *new_node) {
  if (current == nullptr) return new_node;
  
  if (new_node->element < current->element) {
    current->left = _insert(current->left, new_node);
  }
  else if (new_node->element > current->element) {
    current->right = _insert(current->right, new_node);
  }
  else return current;

  current->height = _insert_update_height(current);
  int balance = _insert_get_balance(current);

  // Left Left Case
  if (balance > 1 && new_node->element < current->left->element) {
    return _insert_right_rotate(current);
  }
  // Right Right Case
  if (balance < -1 && new_node->element > current->right->element) {
    return _insert_left_rotate(current);
  }
  // Left Right Case
  if (balance > 1 && new_node->element > current->left->element) {
    current->left = _insert_left_rotate(current->left);
    return _insert_right_rotate(current);
  }
  // Right Left Case
  if (balance < -1 && new_node->element < current->right->element) {
    current->right = _insert_right_rotate(current->right);
    return _insert_left_rotate(current);
  }
  return current;
}

// Inserts an element
template <typename T> void Tree<T>::insert(T element) {
  Node<T> *new_node = new Node<T>(element, 0);
  if (m_root == nullptr) m_root = new_node;
  else m_root = _insert(m_root, new_node);
  m_size++;
}
```

```c
// Helper fucntion for pre_order
template <typename T> string _pre_order(Node<T> *node) {
  return my_to_string(node->element)
    + (node->left == nullptr ? "" : " " + _pre_order(node->left))
    + (node->right == nullptr ? "" : " " + _pre_order(node->right));
}

// Prints the tree in pre-order
template <typename T> string Tree<T>::pre_order() {
  if (m_root == nullptr) return "";
  return _pre_order(m_root);
}

// Helper fucntion for in_order
template <typename T> string _in_order(Node<T>* node) {
  return (node->left == nullptr ? "" : _in_order(node->left) + " ")
  + my_to_string(node->element)
  + (node->right == nullptr ? "" : " " + _in_order(node->right));
}

// Prints the tree in in-order
template <typename T> string Tree<T>::in_order() {
  if (m_root == nullptr) return "";
  return _in_order(m_root);
}

// Helper fucntion for post_order
template <typename T> string _post_order(Node<T>* node) {
  return (node->left == nullptr ? "" : _post_order(node->left) + " ")
  + (node->right == nullptr ? "" : _post_order(node->right) + " ")
  + my_to_string(node->element);
}

// Prints the tree in post-order
template <typename T> string Tree<T>::post_order() {
  if (m_root == nullptr) return "";
  return _post_order(m_root);
}
```