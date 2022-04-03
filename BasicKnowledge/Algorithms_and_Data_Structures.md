# Algorithms and Data Structures

## Algorithm

### definition

in general: A set of steps or instructions for completing task.
in programs: A set of steps a program takes to finish a task.

### Features

- Clearly defined problem statement, input, and output.
- The steps in the algorithm need to be in a very specific order.
- The step also need to be distinct.
- The algorithm should product a result.
- The algorithm should complete in finite amount of time.

two measure for Algorithm:

- Correctness
- Efficiency
  - Time Complexity
  - Space Complexity

## Time Complexity

### Big O

`Order of magnitude of complexity`. Theoretical definition of the complexity of an algorithm as a function of the size.

- Constant time: O(1)
- Linear Search: O(n)
- Binary Search: O(log n) -> known as subLinear
- Quadratic Time: O(n ^ 2)
- Cubic Runtime: O(n ^ 3)
- QuasiLinear Runtime: O(n log n) -> like merge sort
- Polynomial Runtime: O(n^k) -> k is constant number

any algorithm under Polynomial runtime consider efficient and likely to be use in practice.

- Exponential Runtime: O(X ^ n) -> brute force for password
- Combinatorial: O(n!) -> Traveling Salesman

## Space Complexity

- for linear search space in O(1) -> constance space or equal to list size
  - time complexity O(n)
  - space complexity O(1)
- if implement binary search with recursive model -> O(log n)
  - time complexity O(log n)
  - space complexity O(log n)

- recursive function is good in some language like swift but not prefer in python.
- swift has a way to use less of memory for recursive function called `tail call optimization`.

## Data structure

a data storage format. it is the collection of value and the format they are stored in, the relationships between the values in collection as well as the operation applied on the data stored in the structure.

Homogeneous container -> array have the value of same type like in C, java and swift
Heterogeneous structure -> can store any type of value in array

contiguous data structure -> store in blocks of memory that right beside each other with no gaps
none contiguous data structure -> store pointer to follow memory location

### Operation on Data Structure

- Access and read values
- Search for an arbitrary value
- Insert values at any point into the structure
- Delete values in the structure

### Array

- insert to array -> insert to index 0 and shift all thr list -> linear time
- append to array -> insert to the end -> constant time
- Delete operation -> shift array member to left -> O(n) linear runtime

### Linked list

- Arrays is good at access and search but not good in add and delete.
- linked list is linear data structure where each element in the list is contain in the separate object called a `Node`.
- Node has 2 piece of information:
  - item of data we want to store
  - reference to next node
- first node called `Head` and last one called `Tail`
- linked list only save maintain the address of Head node
- node: self referential object
- linked list has two form
  - Singly linked list: save address of next node
  - Double linked list: save the address of the node before and after.

```py
class Node:
  data = None
  next_node = None

  def __init__(self,data):
    self.data = data

  def __repr__(self):
    return "<Node data: %s>" % self.data


class LinkedList:

  def __init__(self):
    head = None
  
  def is_empty(self):
    return self.head == None

  def size(self):
    current = self.head
    count = 0

    while current:
      count += 1
      current = current.next_node
    
    return count

  def add(self, data):
    new_node = Node(data)
    new_node.next_node = head
    head = new_node

  def search(self, key):
    current = self.head

    while current:
      if current.data == key:
        return current
      else:
        current = current.next_node
    
    return False

  def insert(self, data, index):
    if index == 0:
      self.add(data)
    
    if index > 0:
      new_node = Node(data)

      position = index
      current = self.head

      while position > 1:
        current = node.next_node
        position -= 1

      prev_node = current
      next_node = current.next_node 

      prev_node.next_node = new_node
      new_node.next_node = next_node

  def remove(self, key):
    current = self.head
    previous = None
    found = False

    while current and not found:
      if current.data == key and current is self.head:
        found = True
        self.head = current.next_node
      elif current.data == key:
        found = True
        previous.next_node = current.next_node
      else:
        previous = current
        current = current.next_node

    return current

  def node_at_index(self, index):
    if index = 0:
      return self.head
    else:
      current = self.head
      position = 0

      while position < index:
        current = current.next_node
        position += 1
      
      return current

  def __repr__(self):
    nodes = []
    current = self.head

    while current:
      if current is self.head:
        nodes.append("[Head: %s]" % current.data)
      elif current.next_node is None:
        nodes.append("[Tail: %s]" % current.data)
      else:
        nodes.append("[%s]" % current.data)
      
      current = current.next_node
      return '-> '.join(nodes) 
```

- use `-i` for run python file and keep using the python terminal like `python -i linkedList.py`

### Merge sort

- use divide an conquer strategy - break down problem to sub part until it easily solve

- Divide: Find the midpoint of the list and divide into subLists -> O(k log n)
- Conquer: Recursively sort the subLists created in previous step
- Combine: Merge the sorted subLists created in previous step -> O(n)

- in overall time complexity -> O(kn log n)
- space complexity -> O(n)

```py
def merge_sort(list):
  if len(list) <= 1:
    return list
  
  left_half, right_half = split(list)

  left = merge_sort(left_half)
  right = merge_sort(right_half)

  return merge(left, right)

def split(list):
  mid = len(list)//2

  left = list[:mid]
  right = list[mid:]

  return left, right

def merge(left, right):
  l = []
  i = 0
  j = 0

  while i < len(left) and j < len(right):
    if left[i] < right[j]:
      l.append(left[i])
      i += 1
    else:
      l.append(left[j])
      j += 1
  
  while i < len(left):
    l.append(left[i])
    i += 1

  while  j < len(right):
    l.append(left[j])
    j += 1
  
  return l
```

use merge sort for linked list -> O(kn log n)

```py
def merge_sort(linked_list):
  if linked_list.size() == 1:
    return linked_list
  elif linked_list.head is None:
    return linked_list
  
  left_half, right_half = split(linked_list)

  left = merge_sort(left_half)
  right = merge_sort(right_half)

  return merge(left, right)

def split(linked_list):
  if linked_list == None or linked_list.head == None:
    left_half = linked_list
    right_half = None
    return left_half, right_half
  else:
    size = linked_list.size()
    mid = size//2

    mid_node = linked_list.node_at_index(mid-1)
    
    left_half = linked_list
    right_half = linkedList()
    right_half.head = mid_node.next_node
    mid_node.next_node = None

    return left_half, right_half

def merge(left, right):
  merged = linkedList()

  merged.add(0) # Add fake head

  current = merge.head

  left_head = left.head
  right_head = right.head

  while left_head or right_head:
    if left_head is None:
      current.next_node = right_head
      right_head = right_head.next_node
    elif right_head is None:
      current.next_node = left_head
      left_head = left_head.next_node
    else:
      left_data = left_head.data
      right_data = right_head.data
      if left_data < right_data:
        current.next_node = left_head
        left_head = left_head.next_node
      else:
        current.next_node = right_head
        right_head = right_head.next_node

    current = current.next_node
  
  head = merged.head.next_node # Discard fake head
  merged.head = head

  return merged
```

### Bogo Sort

- for get data from command line `import sys` and `first_arg = sys.argv[1]`

```py
import random
import sys

def is_sorted(values):
  for index in range(len(values) -1):
    if values[index] > values[index+1]:
      return false
  return True

def bogo_sort(values):
  while not is_sorted(values):
    random.shuffle(values)
  return values
```

### Selection Sort

- O(n^2)

```py
def selection_sort(values):
  sorted_list = []
  for i in range(0, len(values)):
    index_to_move = index_of_min(values)
    sorted_list.append(value.pop(index_to_move))
  return sorted_list

def index_of_min(values):
  min_index = 0
  for i in range(1, len(values)):
    if values[i] < values[min_index]:
      min_index = i
  return min_index
```

### Recursion

```py
def sum(numbers):
  if not numbers:
    return 0
  remain_sum = sum(number[1:])
  return numbers[0] + remain_sum
```

### Quick Sort

- best case O(n log n), worst O(n^2)

```py
def quicksort(values):
  if len(values) <= 1:
    return values
  less_than_pivot = []
  greater_than_pivot = []
  pivot = []
  for value in values[1:]:
    if value <= pivot:
      less_than_pivot.append(value)
    else:
      greater_than_pivot.append(value)
  return quicksort(less_than_pivot) + [pivot] + quicksort(greater_than_pivot)
```

### Merge Sort

- O(n log n)

```py
def merge_sort(values):
  if len(values) <= 1:
    return values
  middle_index = len(values) // 2
  left_values = merge_sort(values[:middle_index])
  right_values = merge_sort(values[middle_index:])
  sorted_values = []
  left_index = 0
  right_index = 0
  while left_index < len(left_values) and right_index < len(right_values):
    if left_values[left_index] < right_values[right_index]:
      sorted_values.append(left_values[left_index])
      left_index += 1
    else:
      sorted_values.append(right_values[right_index])
      right_index += 1
  sorted_values += left_values[left_index:]
  sorted_values += right_values[right_index:]
  return sorted_values
```

## Reference

- [Algorithms and Data Structures Tutorial Full Course for Beginners](https://www.youtube.com/watch?v=8hly31xKli0)
