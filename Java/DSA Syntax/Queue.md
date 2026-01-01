# Queue in Java - Functionalities and Syntax

## Declaration and Common Implementations
```java
import java.util.Queue;
import java.util.LinkedList;
import java.util.ArrayDeque;
import java.util.PriorityQueue;

// LinkedList implementation (most common)
Queue<String> queue = new LinkedList<>();

// ArrayDeque (faster for stack/queue operations)
Queue<Integer> queue = new ArrayDeque<>();

// PriorityQueue (natural or custom ordering)
Queue<Integer> queue = new PriorityQueue<>();

// With initial capacity (ArrayDeque)
Queue<String> queue = new ArrayDeque<>(16);
```

## Adding Elements
```java
Queue<String> queue = new LinkedList<>();

// Add element (throws exception if capacity restricted)
queue.add("element");

// Add element (returns false if capacity restricted)
boolean added = queue.offer("element");

// Note: offer() is preferred over add() for capacity-restricted queues
```

## Retrieving Elements (Without Removal)
```java
// Get head element without removing (throws exception if empty)
String head = queue.element();

// Get head element without removing (returns null if empty)
String head = queue.peek();

// Check if queue is empty
boolean isEmpty = queue.isEmpty();
```

## Removing Elements
```java
// Remove and return head element (throws exception if empty)
String removed = queue.remove();

// Remove and return head element (returns null if empty)
String removed = queue.poll();

// Note: poll() is preferred over remove() to avoid exceptions
```

## Size Operations
```java
// Get number of elements
int size = queue.size();

// Check if empty
boolean isEmpty = queue.isEmpty();
```

## Iterating Over Queue
```java
// Enhanced for loop (not recommended for queue semantics)
for(String element : queue) {
    System.out.println(element);
}

// Iterator
Iterator<String> iterator = queue.iterator();
while(iterator.hasNext()) {
    System.out.println(iterator.next());
}

// While loop with poll (proper queue processing)
while(!queue.isEmpty()) {
    String element = queue.poll();
    System.out.println("Processing: " + element);
}

// Stream API (Java 8+)
queue.stream().forEach(System.out::println);
```

## Queue Implementations Comparison

### LinkedList
```java
Queue<String> queue = new LinkedList<>();
// - Implements both Queue and List interfaces
// - Good for: General purpose queue
// - Performance: O(1) for add/remove operations
// - Memory: Higher overhead (node-based)
```

### ArrayDeque
```java
Queue<String> queue = new ArrayDeque<>();
// - Faster than LinkedList for queue operations
// - Good for: High-performance queue/stack
// - Performance: O(1) for add/remove operations
// - Memory: Lower overhead (array-based)
// - Can be used as Stack with push/pop methods
```

### PriorityQueue
```java
Queue<Integer> queue = new PriorityQueue<>();
// - Elements ordered by natural ordering or comparator
// - Good for: Priority-based processing
// - Performance: O(log n) for add/remove operations
// - Not suitable for FIFO requirements
```

## Queue Properties
- **Order**: FIFO (First In, First Out) - except PriorityQueue
- **Duplicates**: Generally allowed (depends on implementation)
- **Null Values**: Generally not allowed (except LinkedList)
- **Thread Safety**: Not thread-safe (use ConcurrentLinkedQueue for concurrent access)
- **Performance** (varies by implementation):
  - **LinkedList**: O(1) for add/remove, O(n) for search
  - **ArrayDeque**: O(1) for add/remove, O(n) for search
  - **PriorityQueue**: O(log n) for add/remove, O(n) for search
- **Bounded vs Unbounded**: Can be capacity-restricted

## Common Use Cases
- Task scheduling and processing queues
- Breadth-first search algorithms
- Print job queues
- Message queues in concurrent systems
- Event handling systems
- Cache implementations (LRU)
- Producer-consumer patterns

## Best Practices
- Use `Queue` interface for variable declarations
- Prefer `offer()` over `add()` and `poll()` over `remove()` to handle capacity restrictions
- Choose implementation based on needs:
  - `ArrayDeque` for general purpose high-performance queue
  - `LinkedList` when you need List operations too
  - `PriorityQueue` for priority-based ordering
- Use `ConcurrentLinkedQueue` for thread-safe operations
- Consider `BlockingQueue` implementations for producer-consumer scenarios
- Avoid using queue for random access (use List instead)
- Process queues with while loops using `poll()` rather than iterators for proper FIFO semantics