# ArrayList in Java - Functionalities and Syntax

## Declaration and Initialization
```java
import java.util.ArrayList;
import java.util.List;

// Basic declaration
ArrayList<String> list = new ArrayList<>();

// With initial capacity
ArrayList<Integer> list = new ArrayList<>(10);

// From another collection
ArrayList<String> list = new ArrayList<>(anotherList);

// Using List interface (recommended)
List<String> list = new ArrayList<>();
```

## Adding Elements
```java
List<String> list = new ArrayList<>();

// Add to end
list.add("element");

// Add at specific index
list.add(0, "first element");

// Add multiple elements
list.addAll(anotherList);

// Add at specific index
list.addAll(1, anotherList);
```

## Retrieving Elements
```java
// Get element by index
String element = list.get(0);

// Get first/last element
String first = list.get(0);
String last = list.get(list.size() - 1);

// Check if contains element
boolean contains = list.contains("value");

// Find index of element
int index = list.indexOf("value");
int lastIndex = list.lastIndexOf("value");
```

## Removing Elements
```java
// Remove by index
String removed = list.remove(0);

// Remove by value (first occurrence)
boolean removed = list.remove("value");

// Remove by condition (Java 8+)
list.removeIf(s -> s.length() < 3);

// Remove range of elements
list.subList(1, 3).clear(); // or list.removeRange(1, 3);

// Clear all elements
list.clear();
```

## Size and Capacity
```java
// Get current size
int size = list.size();

// Check if empty
boolean isEmpty = list.isEmpty();

// Ensure minimum capacity
list.ensureCapacity(100);

// Trim capacity to current size
list.trimToSize();
```

## Iterating Over ArrayList
```java
// Traditional for loop
for(int i = 0; i < list.size(); i++) {
    System.out.println(list.get(i));
}

// Enhanced for loop
for(String element : list) {
    System.out.println(element);
}

// Iterator
Iterator<String> iterator = list.iterator();
while(iterator.hasNext()) {
    System.out.println(iterator.next());
}

// ListIterator (bidirectional)
ListIterator<String> listIterator = list.listIterator();
while(listIterator.hasNext()) {
    System.out.println(listIterator.next());
}

// Using forEach (Java 8+)
list.forEach(element -> System.out.println(element));

// Stream API (Java 8+)
list.stream().forEach(System.out::println);
```

## ArrayList Properties
- **Order**: Maintains insertion order
- **Duplicates**: Allows duplicate elements
- **Null Values**: Allows multiple null values
- **Thread Safety**: Not thread-safe (use Vector or Collections.synchronizedList() for concurrent access)
- **Performance**:
  - **O(1)**: `get()`, `set()`, `add()` (end), `size()`, `isEmpty()`
  - **O(n)**: `add(index)`, `remove(index)`, `contains()`, `indexOf()`
  - **Amortized O(1)**: `add()` (end) - occasional resize
- **Capacity**: Automatically grows when needed (doubles current capacity)

### Dynamic Capacity
- **Initial Capacity**: Default 10 (empty constructor)
- **Growth Factor**: Capacity doubles when limit reached
- **Resize Trigger**: When `size == capacity`
- **Memory Usage**: May have unused capacity, use `trimToSize()` to minimize

## Common Use Cases
- Dynamic arrays where size changes frequently
- Stacks and queues implementation
- Storing ordered collections of data
- When you need indexed access to elements
- Temporary data storage during processing

## Best Practices
- Use `List` interface for variable declarations
- Set initial capacity if approximate size is known to avoid frequent resizing
- Use `trimToSize()` when ArrayList size won't change to save memory
- Prefer `ArrayList` over `Vector` (Vector is synchronized and slower)
- Use `LinkedList` if frequent insertions/deletions in middle are needed
- Consider `Arrays.asList()` for fixed-size lists from arrays