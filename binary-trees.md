# Tree Types:

## Full Binary Trees

## Complete Binary Trees

## Perfect Binary Trees

## Balanced Binary Trees

## Binary Search Tree (BST)

---

# Terms

## Nodes

## Edges

## Root

## Leaf Nodes

## 'Levels'

## 'Height'

---

# Traversal Techniques

## Node Processing Ordering Acronyms

This is a series of letters used to describe the order in which nodes are evaluated/operated on when traversing a binary tree. This order often uses `N` (representing the current node), `L` (representing the left node) and `R` (representing the right node).

## Depth-First Search (DFS)

This is a type of binary tree traversal that involves searching from the root node of a tree or subtree to the leaf node of a branch (left or right). After traversing to the end of the tree/subtree's branch, it then backtracks to the last subtree root node and traverses down the opposite branch. This happens until all root-to-leaf branches have been traversed and all nodes explored (generally speaking).

#### Pre-Order

This is a form of DFS that involves evaluating/operating on nodes in the order of NLR where the root node is evaluated first and then its' left node, and lastly its right node.

#### In-Order

This is a form of DFS that involves evaluating/operating on nodes in the order of LNR where the left node is evaluated first, then the root node, and lastly its right node.

#### Post-Order

This is a form of DFS that involves evaluating/operating on nodes in the order of LRN where the left and right nodes are evaluated/operated on first follwed by the root node last.

## Traversal/Discovery Order

This refers to the order in which nodes are discovered in the Binary Tree.

Generally, traversing nodes is done through the use of a loop or multiple loops and the reassignment of a variable (often named `curr`) to the next node from the most current node that's been discovered.

## Processing Order

This refers to the order in which nodes are processed/used. This is not the same as *discovery order*.

A stack is generally used to tailor the order in which we process nodes, whereas the discovery order determines in what order we're traversing or *"discovering"* nodes.

## Parts of a Binary Tree Traversal:

#### Discovery Loop

This is the part of a solution/algo that handles the actual traversal and discovery of nodes.
This is a common pattern found in DFS algorithms and for all of the processing orders. It looks something like this:

``` javascript
while (curr) {
  stack.push(curr);
  curr = curr.left;
}
```

Generally, this discovery loop traverses down the leftmost subtree until it reaches the end of a branch (`null`). From here, it backtracks to the last root node for a tree/subtree and then traverses down to the right node, thus exploring the right branches from the tree/subtree.

#### Back Track Stack

*"Back tracking"* refers to the process of retrieving the last root node for a tree/subtree whose other branch has not yet been traversed.

The way back tracking is achieved in these algorithms is through the use of a stack. The stack keeps track of nodes that've been most recently discovered. When the discovery loop reaches the end of a branch, the stack pops the last discovered node and reassigns the current (`curr`) node to the popped node's right node.

From here, the discovery loop can then begin again and track its way down the leftmost branch.

The back track stack is essential and is always needed when performing a DFS of a binary tree.

This pattern looks like this:

```javascript
let stack = [];
let curr = root;

// more code...
while (stack.length > 0) {
  while (curr) { // Discovery Loop
    stack.push(curr); // Stack used for: 1) backtracking, 2) deferred processing
    curr = curr.left;
  }

  let next = stack.pop(); // Back tracks to last discovered node
  curr = next.right;
}
```

The back track stack *can* have dual purpose as well, being used to implement specific processing order of nodes as well. 

#### The "Breaker" Loop

This loop is what determines when the tree needs no more processing. 
Generally, there are 2 main conditions used to determine this (either one or both):
- If the current node being discovered (`curr`) is `null`
  - This means, there are no nodes further down the branch to process
- If the stack is empty
  - The stack holds nodes that need to be processed or whose right branch needs trversing. If the stack is empty this signals that there are no more nodes that need processing nor are there any right branches that are left to explore.


```javascript
let stack = [];
let curr = root;

// more code...
while (curr || stack.length > 0) { // Breaker Loop
  while (curr) { // Discovery Loop
    stack.push(curr)
    curr = curr.left;
  }

  let next = stack.pop();
  curr = next.right;
}
```

#### The Node Processing Stack

The node processing is done through the use of a stack. The stack is used to tailor the order in which we process nodes. Depending on the processing order a stack may or may not be used and sometimes the stack can be the same stack as the *'Back Track Stack'*.

###### Pre-Order Stacking:

```javascript
let stack = [];
let curr = root;

while (curr || stack.length > 0) {
  while (curr) {
    processNode(curr);
    stack.push(curr); // Stack ONLY used for back tracking
    curr = curr.left;
  }

  let next = stack.pop();
  curr = next.right;
}
```

###### In-Order Stacking:

```javascript
let stack = []; // Stack for both back tracking AND processing
let curr = root;

while (curr || stack.length > 0) {
  while (curr) {
    stack.push(curr);
    curr = curr.left;
  }

  curr = stack.pop();
  processNode(curr);
}
```

###### Post-Order Stacking:

```javascript
const backtrack = [root]; // Stack for back tracking
const processing = [];   // Stack for processing nodes
const results = [];


while (backtrack.length > 0) {
  let node = backtrack.pop();
  processing.push(node);

  if (node.left) backtrack.push(node.left);
  if (node.right) backtrack.push(node.right);
}

while (processing.length > 0) {
  let node = processing.pop();
  processNode(node);
}

return results;
```