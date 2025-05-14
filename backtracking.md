# Backtracking

Backtracking is a technique used in computer science when solving problems that involve a collection of values that are naturally a combination or permutation of the input values. Backtracking is best used for problems where there's a natural tree structure to finding the solution values.

Implementation wise, backtracking involves taking a value (candidate) from the collection of inputs (candidates) and testing it against different states. Each state it's tested in generally opens up a series of other related states that it can further be tested against. Going down this "state space tree" will result in leafs/ends that each give us one of our output values. It's important to note that not all leafs/ends will result in a valid output value.

-----

## Terminology

### State Space

This is all possible states within our problem. These are situations or outcomes we could encounter in a series of computations from state to state while solving for the problem.

### State Space Tree

A state space tree is tree-like structure that represents the relationships between states and how they're connected. A state space tree gives us a visual representation of the transitions between one state to the next.

### Candidate

This is a value associated with a state. It's known as a "candidate" because it *could be* a value to add to our solution/output.

### Candidates



### Solution

### Dead-end

### Terminal Condition

### A backtrack step

### Pruning
