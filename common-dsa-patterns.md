# Common DSA Patterns I've Found:

## Start-End Patterns

### Questions to Ask:
- Is the order/position of elements important/relevant to the problem?
- Are the values of the elements important/relevant to the problem?
- What can we *know* from incrementing the start?
- What can we *know* from decrementing the end?

### Distances
In problems where the distance between start and end is significant, we should considering that any progression of start or end towards the center will DECREASE the distance. Doesn't matter which one is being incremented/decremented, the effect is always the same - distance decreases by 1 (generally).

Distance should be considered if the order of the values in a collection matters and is a fundamental part of the problem/question.

### Sorted Values
Sorting comes in handy because we can make assumptions about the values we're working with like:
- Incrementing a start pointer will increase the cumlative value of the elements at start and end pointers
- Decrementing an end pointer will decrease the cumlative value of the elements at the start and end pointers

This can come in handy if we're looking for a maximum or minumum cumulative value between 2 elements in the collection or if we're looking for a maximum or minumum cumulative value between a series of contiguous values in a collection (think "sliding window").

The use of sorting values should be considered if the cumulative values between two or more elements is relevant/important to the problem.

-----

## Anchor-Runner/Slow-Fast Pointers

### *"Window Arithmetic"*

Whenever we're having to compute the sum or product (or any sort of linear arithmetic operation) of the values between two pointers (a subarr of values), we can track changes to the sum/product of these values through the use of (what I call) a *"rolling sum window"*.

The way this works: 
- Whenever we increment the anchor, we can decrement the *rolling sum window* by the current value the anchor is pointing to and then increment the anchor. 

- Whenever we increment the runner, we can increment the runner and then increment the *rolling sum window* by the value the runner is now pointing to.

This way, we can track the cumulative results/sum/product of a subarr of values without having to explicitly `slice` for that subarr and re-iterate over it to compute.

### Duplicate/Unique Elements in a Subarray

This technique can be used with anchor-runner pointers in order to determine if elements in a subarray/sliding window are all unique.

This often involves the use of a hash Map in order to keep track of elements that we've encountered, with keys being the element itself and the value being the index in which it is located at.


-----