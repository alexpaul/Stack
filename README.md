# Stack

A Stack is an abstract data type. The stack works such that the last element added to it is the first element removed. This implementation is referred to as Last in, First out, or LIFO. As we've seen with recursion, the call stack for functions and navigation controller in iOS development those constructs use the stack methodology for execution.

Some of the key properties and functions of a stack are `peek` or top, `push`, `pop`, `isEmpty` and `count`. 

`peek`. Returns the element at the top of the stack without removing the element from the stack. 

`push`. Adds an element to the top of the stack. peek, push and pop operations are done from the top of the stack. This leads to constant time O(1) operations. 

`pop`. Allows for the removal of an element from the top of the stack. 


## Implement a Stack using an Array

```swift 
// implement a Stack using an Array

struct Stack<T> {
  // data structure
  private var elements = [T]()
  
  public var isEmpty: Bool {
    return true
  }
  
  public var count: Int {
    return elements.count
  }
  
  public var top: T? { // or peek
    return elements.last
  }
  
  public mutating func push(_ element: T) {
    elements.append(element)
  }
  
  @discardableResult
  public mutating func pop() -> T? {
    elements.popLast()
  }
}

var stackArr = Stack<String>()
stackArr.push("Big O Notation")
stackArr.push("String")
stackArr.push("Array")
stackArr.push("Dictionary")

print(stackArr.count) // 4

stackArr.pop()

print(stackArr) // ["Big O Notation", "String", "Array"]

stackArr.pop()
stackArr.pop()
stackArr.pop()

print(stackArr.isEmpty) // true
```

## Implement a Stack using a Linked List

#### `Node` 

```swift 
class Node<T: Equatable>: Equatable {
  var value: T
  var next: Node<T>?
  weak var previous: Node<T>? // doubly list, use of weak to prevent retain cycle
  init(_ value: T) {
    self.value = value
  }
  static func ==(lhs: Node, rhs: Node) -> Bool {
    return lhs.value == rhs.value && lhs.next == rhs.next
  }
}
```

#### `LinkedList` 

```swift
struct LinkedList<T: Equatable> {
  // data structure
  private var head: Node<T>?
  private var tail: Node<T>?
  
  private(set) public var count = 0
  
  public var isEmpty: Bool {
    return head == nil
  }
  
  public var peek: T? {
    return tail?.value
  }
  
  public mutating func append(_ element: T) {
    count += 1
    let newNode = Node(element)
    guard let lastNode = tail else {
      head = newNode
      tail = newNode
      return
    }
    lastNode.next = newNode
    newNode.previous = lastNode
    tail = newNode
  }
  
  @discardableResult
  public mutating func removeLast() -> T? {
    // 1
    // empty state
    guard let lastNode = tail else {
      return nil
    }
    count -= 1
    // 2
    // one element in the list
    if head == tail { // Node needs to conform to Equatable
      let removedValue = head?.value
      head = nil
      tail = nil
      return removedValue
    }
    // 1 -> 2 -> 3 -> nil
    
    // 3
    // more than one element in the list
    let removedValue = lastNode.value
    tail = lastNode.previous
    lastNode.previous = nil
    return removedValue
  }
}

var list = LinkedList<Int>()

list.append(1)
list.append(2)
list.append(3)

print(list.count) // 3

list.removeLast()
list.removeLast()

print(list.count) // 1

print(list.peek ?? -1) // 1
```

#### Imlementation of a `Stack` using a LinkedList

```swift
struct Stack<T: Equatable> {
  // data structure
  private var elements = LinkedList<T>()
  
  public var count: Int {
    return elements.count
  }
  
  public var isEmpty: Bool {
    return elements.isEmpty
  }
  
  public var peek: T? {
    return elements.peek
  }
  
  public mutating func push(_ element: T) {
    elements.append(element)
  }
  
  @discardableResult
  public mutating func pop() -> T? {
    return elements.removeLast()
  }
}

var navigationStack = Stack<String>()

navigationStack.push("viewController1")
navigationStack.push("viewController2")
navigationStack.push("viewController3")

navigationStack.pop()

print(navigationStack.peek ?? "no vc's") // viewController2

print(navigationStack.isEmpty) // false

print(navigationStack.count) // 2

navigationStack.pop()
navigationStack.pop()

print(navigationStack.isEmpty) // true
```

## Challenges 

#### Challenge 1 - Min Stack

[LeetCode](https://leetcode.com/problems/min-stack)


#### Challenge 2 - Valid Parentheses

[LeetCode](https://leetcode.com/problems/valid-parentheses)


#### Challenge 3 - Backspace String Compare

[LeetCode](https://leetcode.com/problems/backspace-string-compare)


#### Challenge 4 - Remove Outermost Parentheses

[LeetCode](https://leetcode.com/problems/remove-outermost-parentheses)


#### Challenge 5 - Build an Array with Stack Operations

[LeetCode](https://leetcode.com/problems/build-an-array-with-stack-operations)



