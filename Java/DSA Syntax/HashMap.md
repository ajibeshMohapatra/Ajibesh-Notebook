# HashMap in Java - Functionalities and Syntax

## Declaration and Initialization
```java
import java.util.HashMap;
import java.util.Map;

// Basic declaration
HashMap<K, V> map = new HashMap<>();

// With initial capacity
HashMap<String, Integer> map = new HashMap<>(16);

// With capacity and load factor
HashMap<String, Integer> map = new HashMap<>(16, 0.75f);

// Using Map interface (recommended)
Map<String, Integer> map = new HashMap<>();
```

## Adding Elements
```java
Map<String, Integer> map = new HashMap<>();

// Add key-value pair
map.put("key1", 100);

// Add only if key doesn't exist
map.putIfAbsent("key2", 200);

// Add multiple entries
map.putAll(otherMap);
```

## Retrieving Elements
```java
// Get value by key
Integer value = map.get("key1");

// Get with default value if key not found
Integer value = map.getOrDefault("key1", 0);
```

## Checking Presence
```java
// Check if key exists
boolean hasKey = map.containsKey("key1");

// Check if value exists
boolean hasValue = map.containsValue(100);
```

## Removing Elements
```java
// Remove by key
Integer removedValue = map.remove("key1");

// Remove by key-value pair
boolean removed = map.remove("key1", 100);

// Remove all entries
map.clear();
```

## Size and Emptiness
```java
// Get number of entries
int size = map.size();

// Check if empty
boolean isEmpty = map.isEmpty();
```

## Iterating Over HashMap
```java
// Iterate over keys
for (String key : map.keySet()) {
    System.out.println(key + " = " + map.get(key));
}

// Iterate over values
for (Integer value : map.values()) {
    System.out.println(value);
}

// Iterate over entries (recommended)
for (Map.Entry<String, Integer> entry : map.entrySet()) {
    System.out.println(entry.getKey() + " = " + entry.getValue());
}

// Using forEach (Java 8+)
map.forEach((key, value) -> System.out.println(key + " = " + value));
```

## Advanced Operations (Java 8+)
```java
// Compute value if absent
map.computeIfAbsent("key", k -> k.length());

// Compute value if present
map.computeIfPresent("key", (k, v) -> v + 1);

// General compute
map.compute("key", (k, v) -> (v == null) ? 1 : v + 1);

// Merge values
map.merge("key", 1, Integer::sum);

// Replace all values
map.replaceAll((k, v) -> v * 2);

// Replace specific entry
map.replace("key", 100);
```

## HashMap Properties
- **Order**: No guaranteed order (insertion order not maintained)
- **Null Keys/Values**: Allows one null key, multiple null values
- **Thread Safety**: Not thread-safe (use ConcurrentHashMap for concurrent access)
- **Performance**:
  - **Average Case O(1)**: `put()`, `get()`, `remove()`, `containsKey()`
  - **Worst Case O(n)**: `put()`, `get()`, `remove()`, `containsKey()` (rare, due to hash collisions)
  - **O(n)**: `containsValue()`, iteration operations, `putAll()`
  - **O(1)**: `size()`, `isEmpty()`, `clear()`
  - **Note**: Worst case occurs with poor hash distribution or deliberate hash collision attacks

## Common Use Cases
- Caching data with fast lookups
- Counting frequencies
- Grouping data
- Implementing memoization
- Storing configuration settings

## Best Practices
- Use appropriate initial capacity to avoid frequent resizing
- Prefer Map interface over HashMap for variable declarations
- Use containsKey() before get() if null values are possible
- Consider LinkedHashMap for insertion-order preservation
- Use TreeMap for sorted keys

### Load Factor
The load factor is a measure of how full the HashMap can get before it automatically increases its capacity (resizes).

- **Default Value**: 0.75 (75%)
- **How it Works**: When the number of entries exceeds `capacity × load factor`, the HashMap resizes
- **Example**: With default capacity 16 and load factor 0.75, resize occurs at 12 entries (16 × 0.75 = 12)
- **Impact**: 
  - Lower load factor = more memory usage, fewer collisions, faster lookups
  - Higher load factor = less memory usage, more collisions, slower lookups
- **Setting Custom Load Factor**: `new HashMap<>(initialCapacity, loadFactor)`

**Formula**: `threshold = capacity × loadFactor`
When `size > threshold`, HashMap doubles its capacity and rehashes all entries.

### Capacity and Unlimited Growth
- **Initial capacity is NOT a limit**: It's just the starting size of the internal array
- **Automatic growth**: HashMap can hold unlimited elements (memory permitting)
- **Resize process**: 
  - Capacity doubles each time: 16 → 32 → 64 → 128 → 256 → etc.
  - All entries are rehashed and redistributed to new array positions
  - Expensive operation (O(n)) but maintains O(1) lookup performance
- **Memory is the only constraint**: Limited by JVM heap space, not initial capacity
- **Performance consideration**: Very large HashMaps (>millions of entries) may degrade due to increased collisions and GC pressure