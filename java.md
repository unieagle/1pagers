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

## Lambda / Proc

```ruby
l = lambda{ |arg| puts arg }
l.call(1) #=> 1

# Or
l = ->(arg){ puts arg }
l.call(1) #=> 1
```

```ruby
# Proc is more like a code piece
p = Proc.new{ |arg| puts arg }
p.call(2) #=> 2
```

Main difference between them is `return` in Proc will return the calling function, while lambda just returns the lambda itself:

```ruby
def foo
  l = lambda{ puts "1"; return }
  p = Proc.new{ puts "2"; return }
  
  puts "A"
  l.call
  puts "B"
  p.call
  puts "C"
end

foo
# =>
# A
# 1
# B
# 2
```

`foo` returns by the Proc `return` statement

## Class / Module

### Class

```ruby
class Foo
  attr_accessor :instacne_variable
  def initialize # constructor
    @instacne_variable = 'some thing'
  end
  def foo
    puts "this is instance method"
  end
  def self.bar
    puts "this is class method"
  end
end

f = Foo.new
f.foo #=> "this is instance method"
Foo.bar #=> "this is class method"
```

Subclass

```ruby
class Bar < Foo
end

Bar.new.foo #=> "this is instance method"
```

### Module

Module is like namespace in Ruby, and also can be include or extend into a class.

```ruby
module Foo
  NAME = "Module Foo"
  def foo
    puts "foo"
  end
end

Foo::Name #=> "Module Foo"

class A
  include Foo
end

A.new.foo #=> "foo"

class B
  extend Foo
end

B.foo #=> "foo"
```
