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
```

### Map

```ruby
hash = {a: 1, b: 2, c: 3}
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

## Class / Module