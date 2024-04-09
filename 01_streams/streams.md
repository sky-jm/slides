---
theme: gaia
_class: lead
paginate: true
backgroundColor: #fff
zoom: 20%
backgroundImage: url('https://marp.app/assets/hero-background.svg')
---


# Streams

![bg left:40% 80%](java8.webp)
* Added in Java 8 (2014)
    * with updates in Java 9
* Not to be confused with I/O Streams
* Not an extensive guide, just really quick intro with examples
* Shout if you hear me say something stupid! Correct me on the spot, definitely don't wait for the end! :)
---

# What are those?
* Wrappers around a provided data source (think: arrays, collections, etc.)
* The classic taste of functional programming - think `map` `filter` `reduce` etc.
# What aren't those?
* Not a data structure 
* Never modifies original data source
---
# Stream operations
* Stuff you can perform on a `Stream`!
* 2 types
---
## Intermediate operations
* Another stream
    * Chaining!
## Terminal operations
* End result with a definite type
* Stream is over, cannot be used any further
---

# Benefits 
* Intermediate ops not executed until needed
* Computation happens only when terminal operation initiated
* Source elements are consumed as needed
* Ready for paralelization - `parallel()`
---

# Stream pipeline
**3 steps:**
1) Source
    * (e.g. `Collection`)
2) 0 or more intermediate operations
    * (e.g. `map`)
3) Terminal operation
    * (e.g. `collect`)

---
# Let's dive in with examples
![bg left:40%](https://cdn1.vectorstock.com/i/1000x1000/61/45/man-jump-in-big-mug-vector-40366145.jpgg)

<style scoped>
    img {
        width: 50%;
    }
    p {
        font-size: 10px;
    }
</style>
![20%](dive.png)
**Prompt:**
Create an image of a swimmer jumping into a large coffee cup, with the goal of achieving maximum stability and control during the dive. The swimmer should be shown in the act of taking off from the edge of the pool, their body positioned to make a smooth and controlled descent into the cup. The coffee cup should be depicted as a round, stainless steel container, with a lid that is securely closed. The background should be a bright and colorful one, with a clear sky and white clouds. The lighting should be bright and warm, with the sun shining down on the scene. The swimmer should be shown in their full splendor, with a confident and powerful look on their face. The overall theme of the image should be one of athleticism and skill, as the swimmer is demonstrating their ability to jump into a large coffee cup with precision and control.

--- 


## Demo preparation
Let's create an `Employee` class and an array of Employee objects that we're gonna run the following examples on:
```java
// Base array - our "source"
Employee[] arrayOfEmps = {
        new Employee(1, "John", 55000.0),
        new Employee(2, "Larry", 65000.0),
        new Employee(3, "Mark", 45000.0)
};
```

![bg left:40% width: 80%](class.png)

--- 

## Creating a stream
Whole array:
```java
Stream.of(arrayOfEmps); // The whole array
```
Individual objects:
```java
Stream.of(arrayOfEmps[0], arrayOfEmps[2]); // Individual objects
```
From existing list:
```java
List<Employee> empList = Arrays.asList(arrayOfEmps); // Convert to List
empList.stream();
```

[//]: # (Other ways of creating a `Stream`, this is not exhaustive)

---
<style scoped>
code {
    font-size: 20px;
}
p {
    font-size: 22px;
}
</style>
# `forEach`
* Terminal
* Loops over elements
* `Iterable`, `HashMap` have this directly

Example:
```java
// Raise salary by 2000 for all employees
employeeList.parallelStream().forEach(e -> e.setSalary(e.getSalary() + 2000));
```
Equivalent to:
```java
for (Employee e : employeeList) {
    e.setSalary(e.getSalary() + 2000);
}
```

---

# `map`
* Intermediate op
* => return new stream after applying a function to each element of the stream

```java
List<String> employeeNames = Arrays.stream(arrayOfEmps).
        map(Employee::getName).
        collect(Collectors.toList());
```

---
# `collect`
* Terminal
* accumulates elements into data structures, etc.
    * `toSet`, `toCollection`, etc.
* strategy defined by the Collectors interface, example for string (`joining`):

```java
String allNamesSingleString = Arrays.stream(arrayOfEmps).
        map(Employee::getName). // or e -> e.getName()
        collect(Collectors.joining(", "));
System.out.println("Hello, %s. We've raised your pay by 2000!".formatted(allNamesSingleString));
```

```shell
Hello, John, Larry, Mark. We've raised your pay by 2000!
```

---

# `peek`
* like forEach, but!

```java
employeeList.stream().peek(e -> e.setSalary(e.getSalary() + 2000))
                .map(e -> e.getSalary())
                .peek(System.out::println).
                collect(Collectors.toList());
```
* `collect` is required here, as `peek` is not terminal :)


---
# `count` & `filter`
* `filter` => new stream of elems that pass a predicate
* `count` => terminal, get the number of objects in the stream
```java
Long empCount = employeeList.stream()
        .filter(e -> e.getSalary() > 60000.0)
        .count();
System.out.println("Number of employees with salary over 60,000: %d".formatted(empCount));
```
Output:
```bash
Number of employees with salary over 60,000: 1
```

---
# `reduce` (*fold*)
* => to single value
* Terminal 
```java
Double salaryCosts = employeeList.stream()
        .map(e -> e.getSalary())
        .reduce(0.0, Double::sum);
System.out.println("Salary costs of the company: %f".formatted(salaryCosts));
```

Output: 
```java
Salary costs of the company: 151000.000000
```

---
# `distinct`
* Intermediate op
* Eliminates duplicates
---

# Infinite streams
* Can be useful if elements are still being generated
    * => Don't know length yet

`generate` example:
```java
Stream.generate(Math::random)
        .limit(5) // We have to provide a condition to terminate, here limit() function is used for that
        .forEach(System.out::println);
```

---

# Stuff I haven't mentioned
* `allMatch`, `anyMatch`, and `noneMatch`
    * boolean; processing stopped as soon as answer found (*short-circuiting*)
* `findFirst`, `flatMap`, 
* `sorted`, `min`, `max`, `sum`, `range`, `average`, ...
* Collectors: `summarizingDouble`, `partitioningBy`, `groupingBy`, `mapping`, `reducing` 
* `iterate`
* Java 9: `takeWhile`,
* And many others

---

# Bonus knowledge share
These slides were made using **Marp**, a slides/presentation framework that uses Markdown as source, so it's really straightforward to use!

---

# Sources / resources to read
* https://stackify.com/streams-guide-java-8/
* https://www.baeldung.com/java-8-streams-introduction