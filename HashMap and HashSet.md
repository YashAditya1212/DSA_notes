# Hash Map Crash Course For Coding Interviews (Java)

## **What is a Hash Map?**

**Hash** = Chopping something up into small pieces  
**Map** = Taking those pieces and scrambling them into a number

Think of it like hashing meat into ground beef — you transform the original data into something completely different but still usable.

**Why is it important?**  
It's probably the **most useful data structure for coding interviews** because it maps keys to values, allowing **O(1) average time** for:
- Access
- Insertion  
- Deletion

---

## **1) Hash Map Operations in Java**

### **Basic Syntax & Operations**

```java
import java.util.HashMap;
import java.util.Map;

public class HashMapBasics {
    public static void main(String[] args) {
        // Create a HashMap
        HashMap<String, Integer> map = new HashMap<>();
        
        // ========================================
        // 1. ADD/PUT KEY-VALUE PAIR
        // ========================================
        map.put("apple", 5);
        map.put("banana", 3);
        map.put("orange", 7);
        System.out.println("Map: " + map);
        // Output: {orange=7, banana=3, apple=5} (unordered)
        
        // Overwrite existing key
        map.put("apple", 10); // Replaces old value
        System.out.println("After update: " + map);
        // Output: {orange=7, banana=3, apple=10}
        
        // putIfAbsent - only adds if key doesn't exist
        map.putIfAbsent("apple", 20); // Won't change (key exists)
        map.putIfAbsent("grape", 15); // Adds new entry
        System.out.println("After putIfAbsent: " + map);
        // Output: {grape=15, orange=7, banana=3, apple=10}
        
        
        // ========================================
        // 2. CHECK FOR KEY
        // ========================================
        if (map.containsKey("apple")) {
            System.out.println("Apple exists!");
        }
        // Output: Apple exists!
        
        boolean hasKey = map.containsKey("mango");
        System.out.println("Has mango? " + hasKey);
        // Output: Has mango? false
        
        
        // ========================================
        // 3. CHECK FOR VALUE
        // ========================================
        if (map.containsValue(7)) {
            System.out.println("Value 7 exists!");
        }
        // Output: Value 7 exists!
        
        boolean hasValue = map.containsValue(100);
        System.out.println("Has value 100? " + hasValue);
        // Output: Has value 100? false
        
        
        // ========================================
        // 4. ACCESS VALUE WITH KEY
        // ========================================
        Integer appleCount = map.get("apple");
        System.out.println("Apple count: " + appleCount);
        // Output: Apple count: 10
        
        // Get returns null if key doesn't exist
        Integer mangoCount = map.get("mango");
        System.out.println("Mango count: " + mangoCount);
        // Output: Mango count: null
        
        // getOrDefault - safer alternative
        int safeCount = map.getOrDefault("mango", 0);
        System.out.println("Mango count (safe): " + safeCount);
        // Output: Mango count (safe): 0
        
        
        // ========================================
        // 5. MODIFY VALUE
        // ========================================
        // Method 1: Direct put
        map.put("banana", map.get("banana") + 2);
        System.out.println("Banana after increment: " + map.get("banana"));
        // Output: Banana after increment: 5
        
        // Method 2: merge (cleaner for increments)
        map.merge("orange", 3, Integer::sum); // Adds 3 to existing value
        System.out.println("Orange after merge: " + map.get("orange"));
        // Output: Orange after merge: 10
        
        
        // ========================================
        // 6. REMOVE KEY-VALUE PAIR
        // ========================================
        map.remove("grape");
        System.out.println("After removing grape: " + map);
        // Output: {orange=10, banana=5, apple=10}
        
        // Remove only if key-value match
        map.remove("apple", 5); // Won't remove (value doesn't match)
        map.remove("apple", 10); // Removes (both match)
        System.out.println("After conditional remove: " + map);
        // Output: {orange=10, banana=5}
        
        
        // ========================================
        // 7. SIZE & EMPTY CHECK
        // ========================================
        System.out.println("Size: " + map.size());
        // Output: Size: 2
        
        System.out.println("Is empty? " + map.isEmpty());
        // Output: Is empty? false
        
        
        // ========================================
        // 8. CLEAR ALL ENTRIES
        // ========================================
        map.clear();
        System.out.println("After clear: " + map);
        // Output: After clear: {}
    }
}
```

---

### **Iteration Over Hash Map**

```java
import java.util.HashMap;
import java.util.Map;

public class HashMapIteration {
    public static void main(String[] args) {
        HashMap<String, Integer> map = new HashMap<>();
        map.put("apple", 5);
        map.put("banana", 3);
        map.put("orange", 7);
        
        // ========================================
        // METHOD 1: Iterate over KEYS
        // ========================================
        System.out.println("Iterating over keys:");
        for (String key : map.keySet()) {
            System.out.println(key + " = " + map.get(key));
        }
        // Output:
        // orange = 7
        // banana = 3
        // apple = 5
        
        
        // ========================================
        // METHOD 2: Iterate over VALUES
        // ========================================
        System.out.println("\nIterating over values:");
        for (Integer value : map.values()) {
            System.out.println(value);
        }
        // Output: 7, 3, 5
        
        
        // ========================================
        // METHOD 3: Iterate over KEY-VALUE PAIRS (Best)
        // ========================================
        System.out.println("\nIterating over entries:");
        for (Map.Entry<String, Integer> entry : map.entrySet()) {
            System.out.println(entry.getKey() + " -> " + entry.getValue());
        }
        // Output:
        // orange -> 7
        // banana -> 3
        // apple -> 5
        
        
        // ========================================
        // METHOD 4: forEach with Lambda (Java 8+)
        // ========================================
        System.out.println("\nUsing forEach:");
        map.forEach((key, value) -> {
            System.out.println(key + ": " + value);
        });
        // Output: Same as above
    }
}
```

---

## **Complete HashMap Method Reference**

```java
import java.util.HashMap;

public class HashMapMethodReference {
    public static void main(String[] args) {
        HashMap<String, Integer> map = new HashMap<>();
        
        // ADDING
        map.put(key, value)              // Add or update
        map.putIfAbsent(key, value)      // Add only if key doesn't exist
        map.putAll(otherMap)             // Add all entries from another map
        map.merge(key, value, remappingFunction) // Merge values
        
        // ACCESSING
        map.get(key)                     // Returns value or null
        map.getOrDefault(key, defaultValue) // Returns value or default
        
        // CHECKING
        map.containsKey(key)             // Returns true/false
        map.containsValue(value)         // Returns true/false
        map.isEmpty()                    // Returns true if empty
        map.size()                       // Returns number of entries
        
        // REMOVING
        map.remove(key)                  // Removes entry
        map.remove(key, value)           // Removes if both match
        map.clear()                      // Removes all entries
        
        // ITERATION
        map.keySet()                     // Returns Set of keys
        map.values()                     // Returns Collection of values
        map.entrySet()                   // Returns Set of Map.Entry
        map.forEach((k, v) -> {})        // Lambda iteration (Java 8+)
        
        // REPLACEMENT
        map.replace(key, newValue)       // Replace value
        map.replace(key, oldValue, newValue) // Replace if value matches
        map.replaceAll((k, v) -> newValue)   // Replace all values
        
        // COMPUTATION (Advanced)
        map.compute(key, (k, v) -> newValue)      // Compute new value
        map.computeIfAbsent(key, k -> newValue)   // Compute if absent
        map.computeIfPresent(key, (k, v) -> newValue) // Compute if present
    }
}
```

---

## **2) Common Use Cases for Hash Maps**

### **Use Case 1: Pair Sum Problems**

**Problem:** Find two numbers in an array that add up to a target.

```java
import java.util.HashMap;

public class TwoSum {
    // LeetCode #1: Two Sum
    public static int[] twoSum(int[] nums, int target) {
        HashMap<Integer, Integer> map = new HashMap<>();
        
        for (int i = 0; i < nums.length; i++) {
            int complement = target - nums[i];
            
            // Check if complement exists in map
            if (map.containsKey(complement)) {
                return new int[] {map.get(complement), i};
            }
            
            // Store current number with its index
            map.put(nums[i], i);
        }
        
        return new int[] {}; // No solution found
    }
    
    public static void main(String[] args) {
        int[] nums = {2, 7, 11, 15};
        int target = 9;
        
        int[] result = twoSum(nums, target);
        System.out.println("Indices: " + result[0] + ", " + result[1]);
        // Output: Indices: 0, 1 (nums[0] + nums[1] = 2 + 7 = 9)
    }
}
```

**How it works:**
1. Store each number with its index as we iterate
2. For each number, check if `target - number` exists in the map
3. If it exists, we found the pair!

**Time Complexity:** O(n)  
**Space Complexity:** O(n)

---

### **Use Case 2: Duplicate Detection**

**Problem:** Check if an array contains duplicates.

```java
import java.util.HashMap;
import java.util.HashSet;

public class DuplicateDetection {
    // Method 1: Using HashMap to count occurrences
    public static boolean containsDuplicateMap(int[] nums) {
        HashMap<Integer, Integer> map = new HashMap<>();
        
        for (int num : nums) {
            // If we've seen this number before, it's a duplicate
            if (map.containsKey(num)) {
                return true;
            }
            map.put(num, 1);
        }
        
        return false;
    }
    
    // Method 2: Using HashSet (simpler for this case)
    public static boolean containsDuplicateSet(int[] nums) {
        HashSet<Integer> set = new HashSet<>();
        
        for (int num : nums) {
            // add() returns false if element already exists
            if (!set.add(num)) {
                return true;
            }
        }
        
        return false;
    }
    
    // Find the first duplicate
    public static int findFirstDuplicate(int[] nums) {
        HashSet<Integer> seen = new HashSet<>();
        
        for (int num : nums) {
            if (seen.contains(num)) {
                return num;
            }
            seen.add(num);
        }
        
        return -1; // No duplicate
    }
    
    public static void main(String[] args) {
        int[] nums1 = {1, 2, 3, 1};
        int[] nums2 = {1, 2, 3, 4};
        
        System.out.println("nums1 has duplicates? " + containsDuplicateSet(nums1));
        // Output: true
        
        System.out.println("nums2 has duplicates? " + containsDuplicateSet(nums2));
        // Output: false
        
        System.out.println("First duplicate in nums1: " + findFirstDuplicate(nums1));
        // Output: 1
    }
}
```

---

### **Use Case 3: Counting (Frequency Map)**

**Problem:** Count the frequency of characters/elements.

```java
import java.util.HashMap;
import java.util.Map;

public class FrequencyCounter {
    // Count character frequency in a string
    public static HashMap<Character, Integer> countCharacters(String s) {
        HashMap<Character, Integer> freq = new HashMap<>();
        
        for (char c : s.toCharArray()) {
            // Method 1: Using getOrDefault
            freq.put(c, freq.getOrDefault(c, 0) + 1);
            
            // Method 2: Using merge (cleaner)
            // freq.merge(c, 1, Integer::sum);
        }
        
        return freq;
    }
    
    // Find first non-repeating character
    public static char firstNonRepeating(String s) {
        HashMap<Character, Integer> freq = countCharacters(s);
        
        for (char c : s.toCharArray()) {
            if (freq.get(c) == 1) {
                return c;
            }
        }
        
        return '_'; // No non-repeating character
    }
    
    // Find most frequent character
    public static char mostFrequent(String s) {
        HashMap<Character, Integer> freq = countCharacters(s);
        
        char maxChar = s.charAt(0);
        int maxCount = 0;
        
        for (Map.Entry<Character, Integer> entry : freq.entrySet()) {
            if (entry.getValue() > maxCount) {
                maxCount = entry.getValue();
                maxChar = entry.getKey();
            }
        }
        
        return maxChar;
    }
    
    public static void main(String[] args) {
        String s = "leetcode";
        
        HashMap<Character, Integer> freq = countCharacters(s);
        System.out.println("Character frequencies: " + freq);
        // Output: {c=1, d=1, e=3, l=1, o=1, t=1}
        
        System.out.println("First non-repeating: " + firstNonRepeating(s));
        // Output: l
        
        System.out.println("Most frequent: " + mostFrequent(s));
        // Output: e
    }
}
```

---

## **HashSet vs HashMap: When to Use Which?**

### **HashSet Basics**

```java
import java.util.HashSet;

public class HashSetBasics {
    public static void main(String[] args) {
        // HashSet stores ONLY values (no keys)
        HashSet<String> set = new HashSet<>();
        
        // ========================================
        // ADD ELEMENTS
        // ========================================
        set.add("apple");
        set.add("banana");
        set.add("orange");
        set.add("apple"); // Duplicate - won't be added
        System.out.println("Set: " + set);
        // Output: [banana, orange, apple] (unordered, no duplicates)
        
        
        // ========================================
        // CHECK FOR ELEMENT
        // ========================================
        System.out.println("Contains apple? " + set.contains("apple"));
        // Output: true
        
        
        // ========================================
        // REMOVE ELEMENT
        // ========================================
        set.remove("banana");
        System.out.println("After remove: " + set);
        // Output: [orange, apple]
        
        
        // ========================================
        // SIZE & EMPTY
        // ========================================
        System.out.println("Size: " + set.size());
        // Output: 2
        
        System.out.println("Is empty? " + set.isEmpty());
        // Output: false
        
        
        // ========================================
        // ITERATION
        // ========================================
        for (String fruit : set) {
            System.out.println(fruit);
        }
        // Output: orange, apple (order not guaranteed)
        
        
        // ========================================
        // CLEAR
        // ========================================
        set.clear();
        System.out.println("After clear: " + set);
        // Output: []
    }
}
```

### **HashSet Method Reference**

```java
import java.util.HashSet;

public class HashSetMethods {
    public static void main(String[] args) {
        HashSet<String> set = new HashSet<>();
        
        // ADDING
        set.add(element)           // Returns true if added, false if duplicate
        set.addAll(collection)     // Adds all elements from another collection
        
        // CHECKING
        set.contains(element)      // Returns true/false
        set.containsAll(collection) // Checks if all elements exist
        set.isEmpty()              // Returns true if empty
        set.size()                 // Returns number of elements
        
        // REMOVING
        set.remove(element)        // Removes element
        set.removeAll(collection)  // Removes all specified elements
        set.retainAll(collection)  // Keeps only specified elements
        set.clear()                // Removes all elements
        
        // ITERATION
        for (String item : set) {} // Enhanced for loop
        set.forEach(item -> {})    // Lambda (Java 8+)
        
        // CONVERSION
        set.toArray()              // Convert to array
    }
}
```

---

## **HashMap vs HashSet Decision Tree**

```
Do you need to store KEY-VALUE pairs?
├─ YES → Use HashMap
│   ├─ Example: Word frequency counter (word → count)
│   ├─ Example: Two Sum (number → index)
│   └─ Example: Person → Age mapping
│
└─ NO → Do you just need to track EXISTENCE?
    └─ YES → Use HashSet
        ├─ Example: Check for duplicates
        ├─ Example: Visited nodes in graph
        └─ Example: Unique elements only
```

---

## **3) How Hash Maps Work Under the Hood**

### **Internal Structure**

```java
// Simplified internal structure of HashMap
public class HashMapInternals {
    /*
     * HashMap is implemented as an ARRAY of BUCKETS
     * 
     * [Bucket 0] → Entry(key1, val1) → Entry(key2, val2) → null
     * [Bucket 1] → null
     * [Bucket 2] → Entry(key3, val3) → null
     * [Bucket 3] → Entry(key4, val4) → Entry(key5, val5) → null
     * 
     * Each bucket is a LINKED LIST (chaining) to handle collisions
     * 
     * DEFAULT CAPACITY: 16 buckets
     * LOAD FACTOR: 0.75 (resize when 75% full)
     */
    
    public static void demonstrateHashing() {
        // Step 1: HASH FUNCTION
        String key = "apple";
        int hashCode = key.hashCode(); // Java's built-in hash function
        System.out.println("Hash code of 'apple': " + hashCode);
        // Output: 93029210
        
        // Step 2: COMPRESS TO BUCKET INDEX
        int bucketCount = 16; // Default HashMap size
        int bucketIndex = hashCode % bucketCount;
        System.out.println("Bucket index: " + bucketIndex);
        // Output: 10 (93029210 % 16 = 10)
        
        // This is where "apple" would be stored in the internal array
    }
    
    public static void main(String[] args) {
        demonstrateHashing();
    }
}
```

### **Hash Collision Resolution**

```java
import java.util.HashMap;

public class HashCollisions {
    /*
     * COLLISION: When two different keys hash to the same bucket
     * 
     * Example:
     * key1.hashCode() % 16 = 5
     * key2.hashCode() % 16 = 5  ← COLLISION!
     * 
     * RESOLUTION METHODS:
     * 1. CHAINING (Java HashMap uses this)
     * 2. OPEN ADDRESSING (Linear Probing, Quadratic Probing)
     */
    
    public static void main(String[] args) {
        HashMap<String, Integer> map = new HashMap<>();
        
        // These strings might collide in the same bucket
        map.put("apple", 1);
        map.put("banana", 2);
        map.put("orange", 3);
        
        /*
         * CHAINING:
         * 
         * Bucket 5 → [apple → 1] → [orange → 3] → null
         * Bucket 7 → [banana → 2] → null
         * 
         * When getting "orange":
         * 1. Hash "orange" → Bucket 5
         * 2. Traverse linked list in Bucket 5
         * 3. Compare keys until "orange" is found
         * 4. Return value 3
         */
        
        System.out.println(map.get("orange")); // Output: 3
    }
}
```

### **Resizing & Rehashing**

```java
import java.util.HashMap;

public class HashMapResizing {
    public static void main(String[] args) {
        /*
         * DEFAULT CAPACITY: 16 buckets
         * LOAD FACTOR: 0.75
         * 
         * RESIZE TRIGGER: size > capacity * loadFactor
         * Example: 16 * 0.75 = 12 entries
         * 
         * WHEN RESIZING:
         * 1. Create new array with double capacity (16 → 32)
         * 2. REHASH all existing entries
         * 3. Insert them into new array
         * 
         * WHY REHASH?
         * - Bucket index = hashCode % capacity
         * - Capacity changed, so indices change too!
         */
        
        HashMap<Integer, String> map = new HashMap<>();
        
        // Adding 13 entries will trigger resize (threshold = 12)
        for (int i = 0; i < 13; i++) {
            map.put(i, "Value" + i);
        }
        
        /*
         * After 12th insertion:
         * - HashMap resizes from 16 → 32 buckets
         * - All entries are rehashed and redistributed
         * - This is O(n) operation but happens rarely
         */
        
        System.out.println("Size: " + map.size());
        // Output: 13
    }
}
```

---

## **Performance Characteristics**

### **Time Complexity**

```java
/*
 * AVERAGE CASE (good hash function, few collisions):
 * - put(key, value):    O(1)
 * - get(key):           O(1)
 * - remove(key):        O(1)
 * - containsKey(key):   O(1)
 * 
 * WORST CASE (all keys hash to same bucket):
 * - put(key, value):    O(n)
 * - get(key):           O(n)
 * - remove(key):        O(n)
 * - containsKey(key):   O(n)
 * 
 * ITERATION:
 * - keySet():           O(n)
 * - values():           O(n)
 * - entrySet():         O(n)
 * 
 * Note: Java 8+ uses TREE (Red-Black Tree) instead of linked list
 * when bucket has > 8 entries, improving worst case to O(log n)
 */
```

### **Space Complexity**

```java
/*
 * SPACE: O(n) where n = number of entries
 * 
 * ACTUAL MEMORY:
 * - Array of buckets: capacity * reference_size
 * - Each entry: key + value + metadata
 * - Overhead: ~36-48 bytes per entry (depends on JVM)
 * 
 * For 1000 entries:
 * - ArrayList<Integer>: ~4KB
 * - HashMap<Integer, Integer>: ~40-50KB
 * 
 * Trade-off: HashMap uses more memory but gives O(1) operations
 */
```

---

## **Important Notes & Tips**

```java
/*
 * 1. ORDERING
 * - HashMap: UNORDERED (random iteration order)
 * - LinkedHashMap: Maintains INSERTION order
 * - TreeMap: Maintains SORTED order (slower, O(log n))
 * 
 * 2. NULL HANDLING
 * - HashMap allows ONE null key and multiple null values
 * - HashSet allows ONE null element
 * 
 * 3. THREAD SAFETY
 * - HashMap is NOT thread-safe
 * - Use ConcurrentHashMap for multi-threaded environments
 * 
 * 4. EQUALS & HASHCODE
 * - Custom objects as keys MUST override:
 *   - equals()
 *   - hashCode()
 * - Violating this causes bugs!
 * 
 * 5. LOAD FACTOR
 * - Higher = less memory, more collisions
 * - Lower = more memory, fewer collisions
 * - Default 0.75 is well-balanced
 */
```

---

## **Common Interview Patterns**

### **Pattern 1: Frequency Map**
```java
// Count occurrences
HashMap<T, Integer> freq = new HashMap<>();
freq.put(item, freq.getOrDefault(item, 0) + 1);
```

### **Pattern 2: Two-Pointer with Map**
```java
// Two Sum, Subarray Sum, etc.
HashMap<Integer, Integer> map = new HashMap<>();
for (int i = 0; i < arr.length; i++) {
    int target = k - arr[i];
    if (map.containsKey(target)) {
        // Found pair
    }
    map.put(arr[i], i);
}
```

### **Pattern 3: Sliding Window with Map**
```java
// Longest substring without repeating characters
HashMap<Character, Integer> lastSeen = new HashMap<>();
int maxLen = 0, start = 0;
for (int end = 0; end < s.length(); end++) {
    char c = s.charAt(end);
    if (lastSeen.containsKey(c)) {
        start = Math.max(start, lastSeen.get(c) + 1);
    }
    lastSeen.put(c, end);
    maxLen = Math.max(maxLen, end - start + 1);
}
```

---

## **Quick Reference Cheat Sheet**

```java
// HASHMAP
HashMap<K, V> map = new HashMap<>();
map.put(k, v)              // Add/update
map.get(k)                 // Get value
map.getOrDefault(k, def)   // Get with default
map.containsKey(k)         // Check key
map.remove(k)              // Remove
map.size()                 // Size
map.keySet()               // All keys
map.values()               // All values
map.entrySet()             // All entries

// HASHSET
HashSet<T> set = new HashSet<>();
set.add(item)              // Add (returns true/false)
set.contains(item)         // Check existence
set.remove(item)           // Remove
set.size()                 // Size

// WHEN TO USE
HashMap → Store key-value pairs, need O(1) lookup by key
HashSet → Track unique elements, check existence
```

---

This is everything you need to master HashMap and HashSet for coding interviews. Practice implementing the common patterns, and you'll be able to solve 80% of hash-based interview problems!
