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

The elements can now be looked-up with their last known position recorded by index value.

The space from anchor to runner is the current subarray/sliding window that we're working with.

For each iteration we can look up the element at the runner, using our Map, to see if we've encountered the element before and if that element is present in our current subarray/sliding window.

**IF** the element has been encountered before **AND** it occurs on or after the anchor's position *(then we know that its within our current subarray/sliding window)*
**THEN** we move the anchor 1 space past the last know position for that element.

Then we add the element that the runner points to to the Map with its index, increment the runner and continue to the next iteration.

This works for finding subarrays or substrings from a given input because we can determine if the elements in a current subarray/sliding window are unique, and if the condition is to have all elements be unique, then we can know that the subarray/sliding window will always be shortened if an element is found to be within that window.

-----
-----

## Binary Search

### Sorted Elements

If elements of a collection are in a sorted order, then binary search is a good choice. The reason binary search works for sorted elements is similar to why start-end pointers are preferred for sorted elements: because we can make assumptions about elements on either side of a chosen position in the collection.

In the case with binary search, we use the `middle` index position as our evaluation point. From here we can evaluate if which side of the collection we need to search in order to reach a given target (which can also just be a condition).

### Extremities

Analyzing the extremes in a subject or topic in general, makes it easy for us to conceptualize a concept of idea, and then we can later filter ourselves towards a given end of the spectrum once we've looked at both opposing sides of it. 

This same type of principle relates to Binary Search. In problems where we can identify a spectrum with extremes *(like values going from 'falsy' to 'truthy' or sorted numeric values)* then we can easily use these extremes in order to make judgements on which way to go on that spectrum based on a condition we're trying to discover/find.

If you can identify a spectrum with extreme ends, then we can consider using Binary Search. If the problem description uses opposing extremes like *"greatest"* and *"least"* or *"is"* and *"is not"* - then consider Binary Search.

**Examples of spectrums with extremes:**
- The length of an Array. It ranges, ascending in order, from a size of 1 to N.
- Sorted numeric values. One end is the **least** and the other end is the **greatest**.
- The alphabet (ranges in ascending order from `'a'` to `'z'`).
- `true` and `false`
- `1` and `0` (Binary)
- Arrays where elements are sorted by some condition (truthy to falsy, or vice versa)
- Anything that's *"low to high"* or vice versa.
- Anything that's *"short to long"* or vice versa.
- *"Maximum"* and *"Minimum"*

### "Binary Search On Answer"

-----

## Binary Trees

### Recusion Trees

Recusive functions can be mapped out as trees. Specifically, when there's two recursive function calls per each function invocation, this forms a *"Recursion Tree"*, a binary tree where each node is a function call and the child-nodes being function calls itself makes and so on...

##### Depth-First
Plain, recursive functions *branch-out* in a Depth-first fashion, branching out the left branch from the root until the leaf is reached. The leaf node of a branch represents the *base case* of the recursive function and then backtracking.

##### Order of Processing
Mapped out as a Binary Tree, the actual processing/return of a recursive function is based on where the processing is placed within the function's definition.

Examples:
```javascript
// Pre-order processing
function countdown(n) {
  if (n === 0) return;
  console.log(n);
  countdown(n - 1);
}

countdown(5); 
/*  
5
4
3
2
1
*/
```

```javascript
// Post-order processing
function countdown(n) {
  if (n === 0) return;
  countdown(n - 1);
  console.log(n);
}

countdown(5); 
/*  
1
2
3
4
5
*/
```

------
------