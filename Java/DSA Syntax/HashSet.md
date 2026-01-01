# HashSet in Java - Functionalities and Syntax

## Declaration and Initialization
```java
import java.util.HashSet;
import java.util.Set;

// Basic declaration
HashSet<String> set = new HashSet<>();

// With initial capacity
HashSet<Integer> set = new HashSet<>(16);

// With capacity and load factor
HashSet<String> set = new HashSet<>(16, 0.75f);

// From another collection
HashSet<String> set = new HashSet<>(anotherCollection);

// Using Set interface (recommended)
Set<String> set = new HashSet<>();
```

## Adding Elements
```java
Set<String> set = new HashSet<>();

// Add element (returns true if added, false if already exists)
boolean added = set.add("element");

// Add multiple elements
set.addAll(Arrays.asList("a", "b", "c"));

// Note: Duplicates are automatically ignored
set.add("duplicate"); // added
set.add("duplicate"); // ignored, returns false
```

## Checking Presence
```java
// Check if element exists
boolean contains = set.contains("value");

// Check if all elements from another collection exist
boolean containsAll = set.containsAll(anotherCollection);

// Check if set is empty
boolean isEmpty = set.isEmpty();
```

## Removing Elements
```java
// Remove specific element
boolean removed = set.remove("value");

// Remove all elements from another collection
set.removeAll(anotherCollection);

// Keep only elements that are in another collection
set.retainAll(anotherCollection);

// Remove all elements
set.clear();
```

## Size Operations
```java
// Get number of elements
int size = set.size();

// Check if empty
boolean isEmpty = set.isEmpty();
```

## Iterating Over HashSet
```java
// Enhanced for loop
for(String element : set) {
    System.out.println(element);
}

// Iterator
Iterator<String> iterator = set.iterator();
while(iterator.hasNext()) {
    System.out.println(iterator.next());
}

// Using forEach (Java 8+)
set.forEach(element -> System.out.println(element));

// Stream API (Java 8+)
set.stream().forEach(System.out::println);
```

## Set Operations
```java
Set<String> set1 = new HashSet<>(Arrays.asList("a", "b", "c"));
Set<String> set2 = new HashSet<>(Arrays.asList("b", "c", "d"));

// Union (addAll)
Set<String> union = new HashSet<>(set1);
union.addAll(set2); // {"a", "b", "c", "d"}

// Intersection (retainAll)
Set<String> intersection = new HashSet<>(set1);
intersection.retainAll(set2); // {"b", "c"}

// Difference (removeAll)
Set<String> difference = new HashSet<>(set1);
difference.removeAll(set2); // {"a"}

// Check subset
boolean isSubset = set2.containsAll(set1);

// Check disjoint (no common elements)
boolean isDisjoint = Collections.disjoint(set1, set2);
```

## HashSet Properties
- **Order**: No guaranteed order (iteration order may vary)
- **Duplicates**: Automatically prevents duplicate elements
- **Null Values**: Allows one null value
- **Thread Safety**: Not thread-safe (use Collections.synchronizedSet() for concurrent access)
- **Performance**:
  - **O(1) average case**: `add()`, `remove()`, `contains()`, `size()`
  - **O(n) worst case**: Same operations (due to hash collisions)
  - **O(n)**: Iteration operations
- **Backing**: Implemented using HashMap internally (elements as keys)

## Common Use Cases
- Storing unique elements (removing duplicates)
- Fast membership testing
- Implementing mathematical sets
- Removing duplicates from collections
- Caching unique identifiers
- Graph algorithms (visited nodes)

## Best Practices
- Use `Set` interface for variable declarations
- Choose appropriate initial capacity to avoid frequent resizing
- Use `HashSet` for fast lookups when order doesn't matter
- Consider `LinkedHashSet` for insertion-order preservation
- Use `TreeSet` for sorted unique elements
- Prefer `HashSet` over `TreeSet` unless sorting is required
- Use bulk operations (`addAll`, `removeAll`, `retainAll`) for efficiency

### Load Factor (inherited from HashMap)
- **Default Value**: 0.75 (75%)
- **Purpose**: Controls when HashSet resizes its internal HashMap
- **Impact**: Same as HashMap - balances memory usage vs. performance
- **Custom Setting**: `new HashSet<>(initialCapacity, loadFactor)`