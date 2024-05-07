# Data Structures

For data structures it's really important to understand the basic material than have exposure to more advanced topics.

## Contiguous vs Linked

Data structures can be neatly classified as either **contiguous** or **linked**, depending upon whether they are based on arrays or pointers.

- **Contiguously-allocated structures** are composed of single slabs of memory, and include arrays, matrices, heaps, and hash tables.
- **Linked structures** are composed of distinct chunks of memory bound together by pointers, and include lists, trees, and graph adjacency lists.

## Arrays

Arrays are structures of fixed-size data records such that each element can be efficiently located by its index or equivalent address.

### Advantages

1. **Constant time access given the index**: Each index maps directly to the memory address.
2. **Space efficiency**: Arrays consist purely of data so no space is wasted on links or other formatting information.
3. **Memory locality**: If iterating over elements it is advantageous if elements are located adjacent to each other in memory.

### Disadvantages & Dynamic Arrays

The downside of arrays is that their size can't be changed during runtime. This can be overcome by allocating really large arrays but this isn't space efficient.
We can though overcome this by using **dynamic arrays**. We can double an array each time we run out of space by creating a new array of twice it's current capacity and copying over the elements from the initial array.

## Pointers & Linked Structures

Pointers are the connections that hold the pieces of linked structures together. They represent the address of a location in memory.

```mermaid
graph LR
    A[value: T next: Pointer] --> B[value: T next: Pointer]
    B --> C[value: T next: Pointer]
    C --> D[NULL]
```

> Linked list with nodes containing a value of generic type `T` and pointer to the next node. A special NULL pointer value is used to denote structure-terminating or unassigend pointers.

### Generic Properties

1. Each node contains one or more data fields.
2. Each node contains a pointer field to at least one other node.
3. Finally, we need a pointer the the head of the structure.

The list is the simplest linked structure. The three basic operations supported are `search`, `insert`, and `delete`. In **doubly-linked lists**, each node points to both the next and previous nodes. This simplifies certain operations.

### Searching a List

```rs
pub struct ListNode<T> {
    value: T,
    next: Option<Box<ListNode<T>>>,
}

pub fn search_list(node: &Option<Box<ListNode<i32>>>, x: i32) -> Option<&ListNode<i32>> {
    match node {
        Some(node) => {
            if node.value == x {
                Some(node)
            } else {
                search_list(&node.next, x)
            }
        },
        None => None,
    }
}
```
