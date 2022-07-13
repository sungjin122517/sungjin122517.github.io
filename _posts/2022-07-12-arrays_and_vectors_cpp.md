---
title:  "Arrays and vectors in C++"
excerpt: "Advantages and disadvantages of arrays / Features of a vector and its member functions"

categories:
  - oop
tags:
  - [arrays, vectors, C++]

permalink: /oop/arrays_and_vectors/

toc: true
toc_sticky: true
 
date: 2022-07-13
last_modified_at: 2022-07-13
---

## Arrays
A vector in C++ is a class in STL that represents an array.   

### Advantages of array
* Code optimization: data can be retrieved or sorted efficiently.
* Random access: Any data located at an index position can be retrieved.

### Disadvantages of array
* Size limit: fixed size of elements in the array. It doesn't grow its size at runtime.  


```cpp
int arr[6] = {10, 20, 30, 40};
// same as int arr[] = {10, 20, 30, 40, 0, 0}
```


---
## Vectors
* They have the ability to resize itself automatically when an element is inserted or deleted. 
* Their storage is handled automatically by the container.
* Vector elements are placed in contiguous storage so that they can be accessed and traversed using iterators.
* In vectors, data is inserted at the end. This takes `differential time`, as sometimes the array may need to be extended.
* Removing the last element takes only `constant time` since no resizing happens.
* Inserting and erasing at the beginning or in the middle takes `linear time`.


1. `begin()`: returns an iterator pointing to the first element in the vector.
2. `end()`: returns an iterator pointing to the last element in the vector.
3. `rbegin()`: returns a reverse iterator pointing to the last element in the vector (reverse beginning).
4. `rend()`: returns a reverse iterator pointing to the first element in the vector (considered as reverse end).
5. `cbegin()`: returns a constant iterator pointing to the first element in the vector.
6. `cend()`: returns a constant iterator pointing to the last element in the vector.
7. `crbegin() and crend()`: constant reverse iterators.


### Capacity
1. `size()`: returns number of elements.
2. `max_size()`: returns maximum number of elements that the vector can hold.
3. `capacity()`: returns the size of the storage space currently allocated to the vector.
4. `resize(n)`: resizes the container so that it contains n elements.
5. `empty()`: returns whether the container is emtpy.
6. `shrink_to_fit()`: reduces the capacity of the container to fit its size and destroys all elements beyond the capacity. 
7. `reverse(n)`: requests that the vector capacity be at least enough to contain n elements.


### Element access
1. reference operator `[g]`: returns a reference to element at position g.
2. `at(g)`: returns a reference to element at position g.
3. `front()`: returns a reference to first element.
4. `back()`: returns a reference to last element.
5. `data()`: returns a **direct pointer** to the first element. 


### Modifiers
1. `assign()`: assigns new value to the vector elements by replacing old ones.
2. `push_back()` and `pop_back()`
3. `insert()`: inserts new elements before the element at the specified position.
4. `erase()`: remove elements from the speficied position or range.
5. `swap()`: swap contents between two vectors of same type. Sizes may differ.
6. `clear()`: remove all the elements.
7. `embrace()`: extends the container by inserting new element at position.
8. `embrace_back()`: extends the container by inserting new element at the end of the vector.


### Time complexity for operations on vectors
* random access: constant O(1)
* insertion/removal of elements at the end: constant O(1)
* insertion/removal of elements - linear O(N)
* knowing the size: constant O(1)
* resizing the vector: linear O(N)


Reference:   
https://www.geeksforgeeks.org/arrays-in-c-cpp/
https://www.geeksforgeeks.org/vector-in-cpp-stl/