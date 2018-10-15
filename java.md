# Java 1 Pager

## Basic Data

```java
Object empty = null;
int i = 100;
float f = 50.0f;
double d = 100.00;
char c = 'A';
String str = "abcdefg";
```

### String

```java
String str = "a string";
String str = String.format("a string interpolating example: %s", "some other string");

// each char:
for (int i = 0; i < str.length(); i++) {
    System.out.print(str.charAt(i));
}

// substring:
str.substring(2, 4); // "st", [startIndex, endInded)
```

### Array

Basic array:

```java
int [] arr1 = new int[5];
int arr2 [] = new int[5];
int [] arr3 = {1,2,3,4,5};

// modify
arr3[4] = 6;

// each element
for (int var : arr3) {
    System.out.println(var); // 1,2,3,4,5,6
}
```

`ArrayList` as `List` from `util`:

```java
// ArrayList from util
List<Integer> arr = new ArrayList<Integer>(); // or LinkedList<Integer>
// add element
arr.add(Integer.valueOf(1));
arr.add(Integer.valueOf(50));
arr.add(Integer.valueOf(200));
// access element
Integer i = arr.get(2);
System.out.println(i);
// modify element
arr.set(1, Integer.valueOf(100));
// delete element
arr.remove(2);
// loop through elements
for (int var : arr) {
    System.out.println(var);
}
```

### Map

```java
Map<Integer, String> map = new LinkedHashMap<>(); // Or HashMap (not reserving the inserting order)
// add pair
map.put(1, "a");
map.put(2, "b");
map.put(3, "c");
// modify pair
map.put(1, "aa");
// access
String v = map.get(1); // null if key does not exist
System.out.println(v);
// delete
map.remove(3); // skip if key does not exist
// check has key
boolean hasKey = map.containsKey(4); // false
boolean hasValue = map.containsValue("aa"); // true
// check each element
for (Integer key : map.keySet()) {
    System.out.println(String.format("%d : %s", key, map.get(key)));
}
```

## Flow Control

If statement

```java
if(true) {
    // do something
} else if (true) {
    // do something else
} else {
    // do something else
}
```

Switch statement

```ruby
int key = 100;
switch (key) {
    case 1:
        // do something with key == 1
        break;
    case 100:
        // do something with key == 100
        break;
    default:
        break;
}
```

While / Until loop

```java
int var = 1;
while(var < 5){
    System.out.println(var++);
}

do {
    System.out.println(var--);
} while (var > 0); // NOTICE this ;
```

For loop

```java
for(int i = 10 ; i < 15; ++i) {
    System.out.println(i);
}
```

## Methods / Functions

```java
int foo() {
    // do something
}

int bar(int arg1, String arg2) { // no default arg value support, primitive by val, objects by ref
    // do something
}
```

Viable length of arguments list

```java
void foo(Object... args) {
    for (Object var : args) {
        System.out.println(var);
    }
}

foo(1,2,"a","b"); // print: 1,2,a,b
```

With block

```java
// Consumer is for accespt a single arg and return void
// and you can find a lot predefined Handlers in java.util.function
void bar(java.util.function.Consumer l) {
    l.accept(100);
}
bar((arg)->{System.out.println(arg);}); // print 100
```

Overloading (重载)

```java
void foo(int arg) {
    System.out.println("Int:" + arg);
}

void foo(String arg) {
    System.out.println("String:" + arg);
}

foo(100); // Int: 100
foo("abc"); // String: abc
```

## Lambda / Proc

```java
java.util.function.Consumer lambda = (arg)->{ System.out.println(arg); };
lambda.accept(200);
```

## Class / Module

### Class

```java
interface TestInterfaceFoo {
    public void foo();
}

interface TestInterfaceBar {
    public void bar();
}

// Java class can impements multiple interfaces
class Base implements TestInterfaceFoo, TestInterfaceBar {
    int instance_field;
    static int class_field;

    // Constructor
    public Base() {
        this.instance_field = 100;
    }

    public void foo() {
        System.out.println("Base foo");
    }

    public void bar() {
        System.out.println("Base bar");
    }
}

// Java class can only extends from single super class
class TestClass extends Base {
    void test() {
        foo();
        bar();
    }

    public void foo() {
        System.out.println("Sub foo");
    }
}

(new TestClass()).test(); // prints "Sub foo" and "Base bar"
```

### Package

Package is the namespace concept in Java, it needs proper directory structure to compile properly. e.g.

```java
// net/unieagle/MyClass.java
package net.unieagle;
public class MyClass {
    public void test() {
        System.out.println("MyClass test");
    }
}
```

Need has the following file system stucture:

```bash
$tree .
.
├── main.java
└── net
    └── unieagle
        └── MyClass.java
```

## Stream / Parallel Stream

Stream in Java is a collection of elements, on the steam, defined a lot useful operations like `map`, `filter`, `reduce`, `matchAll`, `matchAny`, `collect`, etc.

Can do those operations to a collection of elements with single thread `stream` or paralleled with `parallelStream`, very convenient.

```java
int [] arr = {1,2,3,4,5,6,7,8,9,10};
List<Integer> arr2 = Arrays.stream(arr).boxed().collect(Collectors.toList());

arr2.forEach(arg -> System.out.println(arg));
arr2.stream().filter(arg -> arg % 2 == 0).forEach(arg -> System.out.println(arg));
arr2.parallelStream()
    .filter(arg -> arg % 2 == 0)
    .map(arg -> arg * 10)
    .forEachOrdered(arg -> System.out.println(arg));
```
