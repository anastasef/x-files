## Links

- [ArrayList snippets](https://www.dotnetperls.com/arraylist-integer-java)
- [HashMap snippets](https://www.dotnetperls.com/hashmap-java)

## List
### ArrayList

**Time Complexity:**
read $O(1)$, write $O(n)$

- Access $O(1)$
- Search $O(n)$ ($O(1)$ at the front of the ArrayList) 
- Insert $O(n)$ ($O(1)$ at the back of the ArrayList) 
- Delete $O(n)$ ($O(1)$ at the back of the ArrayList) 

```java
import java.util.ArrayList;

ArrayList<Integer> list = new ArrayList<>();
List<Integer> list = new ArrayList<>();

list.add(1);
list.set(0, 100);

list.remove(0); // Remove index 0
list.clear(); // Remove all elements

list.size();

for (int i = 0; i < list.size(); i++) { 
    System.out.println(list.get(i)); 
}

for (String s : list) { 
    System.out.println(s); 
}
```

### Sorting
Time complexity $O(nlog(n)$

```java
import java.util.Collections;

Collections.sort(list); // Sort ascending
Collections.sort(list, Collections.reverseOrder()); // Sort descending
```

### `int[] -> ArrayList<Integer>`

```java
import java.util.List;
import java.util.ArrayList;

int[] arr = { 1, 2, 3, 4, 5 };
List<Integer> list = new ArrayList<>(arr.length); 

for (int i: arr) {
    list.add(Integer.valueOf(i));
}
```

Java 8
```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.Collectors;

int[] arr = { 1, 2, 3, 4, 5 };

// (1) ====
List<Integer> list = Arrays.stream(arr) // IntStream
                           .boxed()     // Stream<Integer>
                           .collect(Collectors.toList());

// (2) ====                          
// using `IntStream.of()`
List<Integer> list = IntStream.of(arr)    // returns IntStream
                            .boxed()
                            .collect(Collectors.toList());

// (3) ====                            
// Converting primitive integer array to an Integer array
Integer[] boxedArray = Arrays.stream(arr).boxed().toArray(Integer[]::new);
 
// add all elements of the Integer array to a list of Integer
List<Integer> list = new ArrayList<>();
Collections.addAll(list, boxedArray);
```
### Comparing
`list.get(0) == list.get(1)` Does not auto-unbox! It compares the references to Integer
objects.

## LinkedList

A linear collection of data elements, called nodes, each pointing to the next node by means of a pointer. It is a data structure consisting of a group of nodes which together represent a sequence.

**Time Complexity:**
read $O(n)$, write $O(1)$

- Access $O(n)$
- Search $O(n)$ ($O(1)$ at the front of the ArrayList) 
- Insert $O(1)$
- Delete $O(1)$ 

```java
import java.util.LinkedList;

LinkedList<Integer> list = new LinkedList<>();

list.add(1);
list.set(0, 100);   // Update index 0’s value to 100
list.remove(0);     // Remove index 0
list.clear();       // Remove all elements

list.size();

for (int i = 0; i < list.size(); i++) { 
    System.out.println(list.get(i)); 
}

for (int i : list) { 
    System.out.println(s); 
}
```

## Map
### HashMap

**Time Complexity:**
read $O(1)$, write $O(1)$

- Access $O(1)$
- Search $O(n)$ 
- Insert $O(1)$
- Delete $O(1)$ 

```java
import java.util.HashMap;

hm.put(“gopha”, “ok”); // add
hm.put(“gopha”, hm.getOrDefault(“gopha”, “run”)); // update
hm.remove(“gopha”);

hm.size();

for (Map.Entry<String, String> entry : hm.entrySet()) {
    System.out.println(entry.getKey() + “ “ + entry.getValue());
}
```

## Set
### HashSet

**Time Complexity:**
read $O(1)$, write $O(1)$

- Access $O(1)$
- Search $O(1)$ 
- Insert $O(1)$
- Delete $O(1)$ 

```java
import java.util.HashSet;

HashSet<String> hs = new HashSet<>();
hs.add(“gopha ok”);
hs.remove(“gopha ok”);
hs.contains(“gopha ok”);
hs.size();

for (String s : hs) {
    System.out.println(s);
}
```

## Heap

**Time Complexity:**
read $O(1)$, write $O(1)$

- Access $O(1)$
- Insert $O(log(n))$
- Delete $O(log(n))$ 

```java
import java.util.PriorityQueue;

// Max heap
PriorityQueue<Integer> pq = new PriorityQueue<>(Collections.reverseOrder); 
// “Collections.reverseOrder” for a min heap by default

PriorityQueue<Map.Entry<String, Integer>> pq = new PriorityQueue<>(
    (a, b) -> a.getValue().equals(b.getValue()) ?
        a.getKey().compareTo(b.getKey()) :
        a.getValue() - b.getValue()
); 
// Max heap that contains pairs - if values for pairs are the same,
// then they will be sorted ascending (a-z) according to key

pq.add(10);
pq.peek(); // Returns but does not remove the top element
pq.poll(); // Returns and removes the top element

pq.size();
```

## Queue

A collection of elements, supporting two principle operations: enqueue, which inserts an element into the queue, and dequeue, which removes an element from the queue.

**Time Complexity:**
read $O(n)$, write $O(1)$

- Access $O(n)$
- Search $O(n)$
- Insert $O(1)$
- Delete $O(1)$

```java
import java.util.Queue;

Queue<Integer> q = new LinkedList<>(); // Specify as a LinkedList!

q.add(10);
q.peek(); // View top element: Returns head or null if empty
q.poll(); // Remove element: Returns head or null if empty

q.size();
q.isEmpty(); // Returns true if the queue is empty
``` 

## Stack

A collection of elements, with two principle operations: push, which adds to the collection, and pop, which removes the most recently added element.

**Time Complexity:**
read $O(n)$, write $O(1)$

- Access $O(n)$
- Search $O(n)$
- Insert $O(1)$
- Delete $O(1)$

```java
import java.util.Stack;

Stack<Integer> st = new Stack<>();

st.push(10);   // Add element
st.peek();     // View top element: Returns but does not remove the top element
st.pop();      // Remove element: Returns and removes the top element

st.size();
st.isEmpty(); // Returns true if the stack is empty
```

## Copying a Collection

🤔 Как связаны исходник и копия? Если исходная коллекция поменяется, отразится ли это на копии? 

🤔 Нужна изменяемая или неизменяемая копия?


- Прокси (ссылки те же)
    - (Mutable) `refList = list`
    - (Immutable) `Collections.unmodifiableList(list)`
- Список с копиями ссылок
    - (Mutable) `list.stream().collect(toList())`
    - (Immutable)  `List.copyOf(list)`

### Прокси
#### Изменяемый прокси
Прокси означает, что новый объект работает с теми же ссылками, что и старый.
Изменяемый — что манипуляции с новым списком разрешены и приведут к изменениям в исходнике.
Реализация простейшая: `refList = list`

#### Неизменяемый прокси
```java
ummodifiable = Collections.unmodifiableList(list)
```

Методы add, remove и replace у нового списка выбрасывают исключение. Менять исходную коллекцию никто не запрещает. Все изменения отобразятся во всех прокси.

### Копии
Каждый список — это набор ссылок. Исходный лист можно представить так: 

```
ref1 → Order1 
ref2 → Order2 
list → структура данных, которая работает со ссылками ref1 и ref2
```

В прокси вариантах мы работаем с тем же list и с тем же набором [ref1, ref2].
В команде "копий" создаётся новый набор ссылок на те же объекты: 
```
ref3 → Order1 
ref4 → Order2
```

"Копии" работают с другим набором ссылок: [ref3, ref4]. Изменение исходного набора никак не влияет на набор ссылок в "копиях".

#### Изменяемая копия
```java
collectedList = list.stream().collect(toList())
```

#### Неизменяемая копия
```java
copy = List.copyOf(list)
```
