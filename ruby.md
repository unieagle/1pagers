# Template in Ruby

## Basic Data

```ruby
empty = nil
x = 1 / 1.1 / 1_000_000
sym = :this_is_a_symbol
range = 1..100 #[1,100] / 1...100 #[1, 100)
reg = /abc/
```

### String

```ruby
str = 'a string' # can not interpolate
str = "a string"
str = "a string of #{x}"

str.each_char{|c| puts c}

str.each_char.with_index{|c, i| puts "#{i}: #{c}"}

str[0..3] #=> "a st"
```

### Array

```ruby
array = [1,2,3,4]; array.push(5); array.pop() #=> 5; array[0] #=> 1
array.shift #=> 1; array #=> [2,3,4]
array.unshift(1) #=> [1,2,3,4]
```

### Map

```ruby
hash = {a: 1, b: 2, c: 3}
hash[:d] = 4
hash[:c] = 30
hash.delete(:d)
hash.each{|k,v| do_something}
hash.keys #=> [:a, :b, :c]
hash.values #=> [1,2,30]
```

Convert from array of key/value pair array to hash:
```ruby
[['a',1],['b',2]].to_h #=> {'a' => 1, 'b' => 2}
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
