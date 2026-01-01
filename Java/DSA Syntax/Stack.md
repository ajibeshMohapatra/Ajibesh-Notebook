# Stack in Java - Functionalities and Syntax

## Declaration and Implementations
```java
import java.util.Stack;
import java.util.ArrayDeque;
import java.util.Deque;

// Traditional Stack class (extends Vector)
Stack<String> stack = new Stack<>();

// ArrayDeque (recommended for new code)
Deque<String> stack = new ArrayDeque<>();

// With initial capacity (ArrayDeque)
Deque<Integer> stack = new ArrayDeque<>(16);
```

## Pushing Elements
```java
// Using Stack class
Stack<String> stack = new Stack<>();
stack.push("first");
stack.push("second");
stack.push("third");

// Using ArrayDeque
Deque<String> stack = new ArrayDeque<>();
stack.push("first");  // or stack.addFirst("first")
stack.push("second");
stack.push("third");

// Add to bottom (less common)
stack.addLast("bottom");
```

## Popping Elements
```java
// Remove and return top element (throws exception if empty)
String top = stack.pop();

// Using ArrayDeque
String top = stack.pop();  // or stack.removeFirst()

// Safe pop (check before popping)
if (!stack.isEmpty()) {
    String top = stack.pop();
}
```

## Peeking Elements (View Without Removal)
```java
// View top element without removing (throws exception if empty)
String top = stack.peek();

// Using ArrayDeque
String top = stack.peek();  // or stack.getFirst()

// Safe peek
if (!stack.isEmpty()) {
    String top = stack.peek();
}
```

## Size Operations
```java
// Get number of elements
int size = stack.size();

// Check if empty
boolean isEmpty = stack.isEmpty();

// Check if contains element
boolean contains = stack.contains("value");
```

## Iterating Over Stack
```java
// Iterate from top to bottom (LIFO order)
while(!stack.isEmpty()) {
    String element = stack.pop();
    System.out.println("Processing: " + element);
}

// Iterate without modifying (top to bottom)
for(String element : stack) {
    System.out.println(element);
}

// Iterator (top to bottom)
Iterator<String> iterator = stack.iterator();
while(iterator.hasNext()) {
    System.out.println(iterator.next());
}

// Convert to array
Object[] array = stack.toArray();
String[] stringArray = stack.toArray(new String[0]);
```

## Stack Implementations Comparison

### Stack Class
```java
Stack<String> stack = new Stack<>();
// - Extends Vector (synchronized)
// - Legacy class, less efficient
// - Methods: push(), pop(), peek(), empty(), search()
// - Thread-safe but slower
```

### ArrayDeque (Recommended)
```java
Deque<String> stack = new ArrayDeque<>();
// - Modern, high-performance implementation
// - Not thread-safe (use for single-threaded)
// - Methods: push(), pop(), peek() + Deque methods
// - Better performance than Stack class
```

### Concurrent Access
```java
// For thread-safe stack
Deque<String> stack = new ConcurrentLinkedDeque<>();
// or
Stack<String> stack = new Stack<>(); // already synchronized
```

## Stack Properties
- **Order**: LIFO (Last In, First Out)
- **Duplicates**: Allowed
- **Null Values**: Allowed
- **Thread Safety**:
  - `Stack` class: Thread-safe (synchronized)
  - `ArrayDeque`: Not thread-safe
- **Performance**:
  - **O(1)**: `push()`, `pop()`, `peek()`, `size()`, `isEmpty()`
  - **O(n)**: `contains()`, `search()` (Stack class), iteration
- **Memory**: ArrayDeque is more memory efficient

## Common Use Cases
- Function call stack (recursion)
- Undo/redo operations
- Expression evaluation (infix to postfix)
- Backtracking algorithms
- Browser history (back button)
- Text editor undo functionality
- Depth-first search algorithms
- Parsing expressions (parentheses matching)

## Best Practices
- Use `Deque` interface with `ArrayDeque` for new code (better performance)
- Use `Stack` class only for legacy code compatibility
- Prefer `ArrayDeque` over `Stack` for single-threaded applications
- Use `ConcurrentLinkedDeque` for thread-safe concurrent access
- Always check `isEmpty()` before `pop()` or `peek()` to avoid exceptions
- Consider using `Deque` methods for more flexibility (`addFirst`, `removeFirst`, etc.)
- For concurrent scenarios, consider `BlockingDeque` implementations
- Use stacks for LIFO semantics, not for random access (use List instead)