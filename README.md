# Stack

A Stack is an abstract data type. The stack works such that the last element added to it is the first element removed. This implementation is referred to as Last in, First out, or LIFO. As we've seen with recursion, the call stack for functions and navigation controller in iOS development those constructs use the stack methodology for execution.

Some of the key functions of a stack are `peek` or top, `push`, `pop`, `isEmpty` and `count`. 

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
