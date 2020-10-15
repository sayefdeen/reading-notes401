# Implementation: Linked Lists

### what is linked list

A Linked List is a sequence of `Nodes` that are connected/linked to each other. The most defining feature of a Linked List is that each `Node` references the next `Node` in the link.

There are two types of Linked List - Singly and Doubly.

### Terminology

- **Linked List** : A data structure that contains nodes that links/points to the next node in the list.

- **Singly** : A Singly linked list means that there is only one reference, and the reference points to the Next node in a linked list.

- **Doubly** : Doubly linked list means that there is a reference to both the Next and Previous node.

- **Node** : Nodes are the individual items/links that live in a linked list. Each node contains the data for each link.

- **Next** : Each node contains a property called Next. This property contains the reference to the next node.

- **Head** : The Head is a reference type of type `Node` to the first node in a linked list.

- **Current** : The Current reference is a reference type of type Node that is currently being looked at.

---

<p style="text-align:center">Singly Linked List</p>
<img src="https://miro.medium.com/max/602/1*xCtvPp1mZF-Z5gKS90WjHQ.jpeg" />
    
<p style="text-align:center">Doubly Linked list</p>
<img  src="https://media.geeksforgeeks.org/wp-content/uploads/Delete_lincked_list.jpg" />

When traversing a linked list, you are not able to use a `foreach` or for `loop`. We depend on the `Next` value in each node to guide us where the next reference is pointing. The `Next` property is exceptionally important because it will lead us where the next node is and allow us to extract the data appropriately.

The best way to approach a traversal is through the use of a `while()` loop. This allows us to continually check that the `Next` node in the list is not null. If we accidentally end up trying to traverse on a node that is null, a `NullReferenceException` gets thrown and our program will crash/end.

When traversing through a linked list, the Current node is the most helpful. The Current will tell us where exactly in the linked list we are and will allow us to move/traverse forward until we hit the end.

---

## Big O

### What is Big O Notation?

Big O Notation is a way of evaluating the performance of an algorithm, There are two major points to consider when thinking about how an algorithm performs: **how much time it requires at runtime given** **how much time and memory it needs**.

One way to think about Big O notation is a way to express the amount of time that a function, action, or algorithm takes to run based on how many elements we pass to that function.

1. The Big O of time for `includes` would be O(n), at its worse case, the node we are looking for will be the very last node in the linked list. n represents the number of nodes in the linked list

2. The Big O of space for `Includes` would be O(1). This is because there is no additional space being used than what is already given to us with the linked list input.

---

### Liner Data Structure

**linear data structures**, means that there is a sequence and an order to how they are constructed and traversed, we have to go through all of the items in the list in order, or sequentially.

**non-linear data structures**, items don’t have to be arranged in order, which means that we could traverse the data structure non-sequentially.

### Differences Between arrays and linked list.

The biggest differentiator between arrays and linked lists is the way that they use memory in our machines.

- When an array is created, it needs a certain amount of memory. If we had 7 letters that we needed to store in an array, we would need 7 bytes of memory to represent that array. But, we’d need all of that memory in one contiguous block. That is to say, our computer would need to locate 7 bytes of memory that was free, one byte next to the another, all together, in one place, **Static data structure**

- On the other hand, when a linked list is born, it doesn’t need 7 bytes of memory all in one place. One byte could live somewhere, while the next byte could be stored in another place in memory altogether! Linked lists don’t need to take up a single block of memory; instead, the memory that they use can be scattered throughout,**Dynamic data structure**

---

### When do we use linked list.

a linked list is usually efficient when it comes to adding and removing most elements, but can be very slow to search and find a single element.

**Arrays**

- Searching is fast

- Finding element is fast

- Static size not easy to grow or shrink

- Allocates memory when created

- inserting and deleting can be really slow

**Linked List**

- Searching is slow

- Finding element is slow, since it can't be binary

- Dynamic size can grow and shrink

- Only allocate resources as required at tun-time

- inserting and deleting can be really fast.
