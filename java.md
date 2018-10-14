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

```ruby
If true
	# do something
elsif true
	# in another condition
else
	# else
end
```

Switch statement

```ruby
case condition
when 1
	# do something when 1 === condition
when /abc/
	# do something when condition matches reg exp /abc/
when 1..100
	# do something when condition in (1..100) range (1 <= condition <= 100), still calls (1..100).===(condition)
when a_proc
	# do something when a_proc.call(condition) returns true condition, because Proc#===(arg) implements as proc.call(arg)
else
	# do else if none of the above matches
end
```

While / Until loop

```ruby
while true # `do` here is optional
	# do something
	# break / next / redo
end

begin
	# do something
end while true

until false
	# do something / is similar to while but with reversed condition check
end
```

For loop

```ruby
for x in [1,2,3,4,5] do
	# do something
end
```

Other set iterations

```ruby
[1,2,3,4,5].each do |x|
end

{a: 1, b: 2, c: 3}.each do |key, value|
end

5.times{|i| puts i} #=> 0,1,2,3,4

5.upto(10){|i| puts i} #=> 5,6,7,8,9,10

(1..5).step(1){|i| puts i} #=> 1,2,3,4,5
```

## Methods / Functions

```ruby
def foo
  # do something
end

def bar(arg1, arg2='default value')
end
```

Viable length of arguments list

```ruby
def foo(*remaining_args) # place in the end of argument list, collects all the remaining args
  p remaining_args
end

foo #=> []
foo 1,2,3 #=> [1,2,3]
```

Hash map arguments

```ruby
def foo(options={}) # place in the end of argument list, collects all the remaining hash k-v pairs
  p options
end

foo #=> {}
foo a: 1, b: 2, c: 3 #=> {:a=>1, :b=>2, :c=>3}
```

With block

```ruby
def foo
  yield 1 if block_given?
end

foo {|i| p i} #=> 1

# passing block through methods
def bar(&block)
  foo(&block) if block_given?
end

bar {|i| p i} #=> 1
```

Ruby method returns the value of the last statement executed in the method if no `return` specified.

Return multiple values:

```ruby
def foo
  return [1,2]
end

a,b = foo
p a #=> 1
p b #=> 2
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
