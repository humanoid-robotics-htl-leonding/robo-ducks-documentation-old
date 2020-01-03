# Bomberman Max Distance Grouping

## Introduction
The problem this algorithm solves is dividing a set of items into groups where an item belongs to a group if it fulfills a certain condition with at least one member of an existing group.

In our case there are points in a 2 dimensional coordinate system that should belong to a group if they are are close to each other, therefore the condition is being within a certain distance to at least one group member.

## Idea
To solve this problem, a matrix is created that shows which pairs of points fulfill the condition.
If the condition is fulfilled, there is a "bomb" on the corresponding cell.

In this example, A is close to D and B is close to C.

||A|B|C|D|
|-|-|-|-|-|
|A|B| | |B|
|B| |B|B| |
|C| |B|B| |
|D|B| | |B|

Note: A point compared to itself does not have to match the condition.

Next, the matrix is iterated through its diagonal.

At first, a new group is created which contains the first element.
Then a bomberman-like explosion is initiated in the first cell that expands in the positive and negative x and y direction.
Every time the explosion encounters a bomb, another explosion is initiated from this cell. This goes on until every explosion is done.
All items that were part of a bomb belong to the same group.

||A|B|C|D|
|-|-|-|-|-|
|A|#| | |B|
|B| |B|B| |
|C| |B|B| |
|D|B| | |B|

||A|B|C|D|
|-|-|-|-|-|
|A|#|#|#|#|
|B| |B|B| |
|C| |B|B| |
|D|B| | |B|

||A|B|C|D|
|-|-|-|-|-|
|A|#|#|#|#|
|B| |B|B|#|
|C| |B|B|#|
|D|B| | |#|

||A|B|C|D|
|-|-|-|-|-|
|A|#|#|#|#|
|B| |B|B|#|
|C| |B|B|#|
|D|#|#|#|#|

||A|B|C|D|
|-|-|-|-|-|
|A|#|#|#|#|
|B|#|B|B|#|
|C|#|B|B|#|
|D|#|#|#|#|

As you can see, the explosion did only affect A and D.

Now another group is created starting with the next diagonal item that did not explode.

||A|B|C|D|
|-|-|-|-|-|
|A| | | | |
|B| |#|B| |
|C| |B|B| |
|D| | | | |

||A|B|C|D|
|-|-|-|-|-|
|A| | | | |
|B|#|#|#|#|
|C| |B|B| |
|D| | | | |

||A|B|C|D|
|-|-|-|-|-|
|A| | |#| |
|B|#|#|#|#|
|C| |B|#| |
|D| | |#| |

||A|B|C|D|
|-|-|-|-|-|
|A| | |#| |
|B|#|#|#|#|
|C|#|#|#|#|
|D| | |#| |

||A|B|C|D|
|-|-|-|-|-|
|A| |#|#| |
|B|#|#|#|#|
|C|#|#|#|#|
|D| |#|#| |

This time only B and C were involved.

||A|B|C|D|
|-|-|-|-|-|
|A| | | | |
|B| | | | |
|C| | | | |
|D| | | | |

As C/C and D/D already exploded, the diagonal iteration skips these and finishes.

## Optimizing

The first optimization was to compare two items while iterating to prevent having to iterate n times through the collection at first.

Also, the next item is immediately added to the group when a bomb is encountered and then removed from the collection before the recursive explosion. It is still referenced in the recursive method to be compared.

After optimizing, everything stays one-dimensional, but the general idea is still the same. A typical grouping run would look like this:

|A|B|C|D|
|-|-|-|-|

Current element: A, Current group: A

|B|C|D|
|-|-|-|
|-| | |

|B|C|D|
|-|-|-|
|-|-| |

|B|C|D|
|-|-|-|
|-|-|B|

Add D to group, explode recursively.

Current element: D, Current group: A, D

|B|C|
|-|-|
|-| |

|B|C|
|-|-|
|-|-|

Recursive D explosion done.

Current element: A, Current group: A, D

A explosion done.

Save group: A, D

Current element: B, Current group: B

|C|
|-|
|B|

Add C to group, explode recursively.

Current element: C, Current group: B, C

Recursive C explosion done.

Current element: B, Current group: B, C

B explosion done.

Save group: B, C

## Results
After optimizing, there were only 6 comparisons instead of 16 which causes a massive performance increase as the comparison is the most complicated operation.

When grouping 100 items, only about 30 comparisons are needed on average.
