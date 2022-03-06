# **Variables**
1. **Local Variables** - variables that are defined in a method. Local variables are not available outside the method
2. **Instance Variables** - available across methods for any particular instance or object, preceded by the at sign (@) followed by the variable name
3. **Class Variables** - available across different objects. A class variable belongs to the class and is a characteristic of a class. They are preceded by the sign (@@) and are followed by the variable name
4. **Global Variables** - not available across classes. If you want to have a single variable, which is available across classes, you need to define a global variable. The global variables are always preceded by the dollar sign ($). Uninitialized global variables have the value nil and produce warnings with the -w option
```RUBY
$global_variable = 10
class Class1
   def print_global
      puts "Global variable in Class1 is #$global_variable"
   end
end
class Class2
   def print_global
      puts "Global variable in Class2 is #$global_variable"
   end
end

class1obj = Class1.new
class1obj.print_global
class2obj = Class2.new
class2obj.print_global

OUTPUT:
Global variable in Class1 is 10
Global variable in Class2 is 10
```
5. **Constant Variables** - begin with an uppercase letter. Constants defined within a class or module can be accessed from within that class or module, and those defined outside a class or module can be accessed globally
```RUBY
class Example
   VAR1 = 100
   VAR2 = 200
   def show
      puts "Value of first Constant is #{VAR1}"
      puts "Value of second Constant is #{VAR2}"
   end
end

# Create Objects
object = Example.new()
object.show

OUTPUT:
Value of first Constant is 100
Value of second Constant is 200
```
6. **Pseudo-Variables** - special variables that have the appearance of local variables but behave like constants, cannot assign any value to these variables

| Variables | Definition                                  |
|-----------|---------------------------------------------|
| self −    | The receiver object of the current method.  |
| TRUE      | Value representing true.                    |
| FALSE     | Value representing false.                   |
| nil       | Value representing undefined.               |
| __FILE__  | The name of the current source file.        |
| __LINE__  | The current line number in the source file. |

7. **Integer Numbers** - can range from -2<sup>30</sup> to 2<sup>30-1</sup> or -2<sup>62</sup> to 2<sup>62-1</sup>. Integers within this range are objects of class *Fixnum* and integers outside this range are stored in objects of class *Bignum*. We can get the integer value, corresponding to an ASCII character or escape the sequence by preceding it with a question mark
```RUBY
123                  # Fixnum decimal
1_234                # Fixnum decimal with underline
-500                 # Negative Fixnum
0377                 # octal
0xff                 # hexadecimal
0b1011               # binary
?a                   # character code for 'a'
?\n                  # code for a newline (0x0a)
12345678901234567890 # Bignum
```
8. **Floating Numbers** - Ruby supports floating numbers, are also numbers but with decimals. Floating-point numbers are objects of class Float
```RUBY
123.4                # floating point value
1.0e6                # scientific notation
4E20                 # dot not required
4e+20                # sign before exponential
```
9. **String Literals** - simply sequences of 8-bit bytes and they are objects of class String. Double-quoted strings allow substitution and backslash notation but single-quoted strings don't allow substitution and allow backslash notation only for \\ and \'
```RUBY
puts 'escape using "\\"';
puts 'That\'s right';
# If we need to place an apostrophe within a single-quoted string literal, precede it with a backslash
# The backslash also works to escape another backslash, so that the second backslash is not itself interpreted as an escape character

OUTPUT:
escape using "\"
That's right

puts "Multiplication Value : #{24*60*60}";

OUTPUT:
Multiplication Value : 86400
```
- we need to have an instance of String object to call a String method
```RUBY
myStr = String.new("THIS IS TEST")
foo = myStr.downcase

puts "#{foo}" # prints 'this is test'
```

# **Arrays** 
- created by placing a comma-separated series of object references between the square brackets. A trailing comma is ignored
## **Iterating through an Array**
```RUBY
ary = [  "fred", 10, 3.14, "This is a string", "last element", ]
ary.each do |i|
   puts i
end

OUTPUT:
fred
10
3.14
This is a string
last element
```
## **Creating Arrays**
```RUBY
names = Array.new(20)
puts names.size  # This returns 20
puts names.length # This also returns 20

OUTPUT:
20
20
```
## **Assigning Value to Array**
```RUBY
names = Array.new(4, "mac")
puts "#{names}"

OUTPUT:
["mac", "mac", "mac", "mac"]

nums = Array.new(10) { |e| e = e * 2 }
puts "#{nums}"

OUTPUT:
[0, 2, 4, 6, 8, 10, 12, 14, 16, 18]

nums = Array.[](1, 2, 3, 4,5) # Array = [1,2,3,4,5]
digits = Array(0..9) # digits = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9]
puts "#{digits.at(6)}" # print 6
```
## **Collect**
- Collect iterator returns all the elements of a collection
- The collect method is not the right way to do copying between arrays. There is another method called a clone, which should be used to copy one array into another array
-  We normally use the collect method when you want to do something with each of the values to get the new array
```RUBY
a = [1,2,3,4,5]
b = Array.new
b = a.collect
puts b

OUTPUT:
1
2
3
4
5

a = [1,2,3,4,5]
b = a.collect{|x| 10*x}
puts b

OUTPUT:
10
20
30
40
50
```

# **Hashes**
- a collection of key-value pairs like this: "employee" = > "salary"
```RUBY
hsh = colors = { "red" => 0xf00, "green" => 0x0f0, "blue" => 0x00f }
hsh.each do |key, value|
   print key, " is ", value, "\n"
end

OUTPUT:
red is 3840
green is 240
blue is 15
```
## **Creating Hashes**
```RUBY
months = Hash.new( "month" ) # Create a New Hash with a default value

or

months = Hash.new "month"

# When you access any key in a hash that has a default value, if the key or value doesn't exist, accessing the hash will return the default value −
puts "#{months[0]}"
puts "#{months[72]}"

OUTPUT:
month
month

# You can use any Ruby object as a key or value, even an array, for example:
[1,"jan"] => "January"
```
```RUBY
H = Hash["a" => 100, "b" => 200]

puts "#{H['a']}" # print 100
puts "#{H['b']}" # print 200
```
```RUBY
months = Hash.new( "month" )
months = {"1" => "January", "2" => "February"}

keys = months.keys
puts "#{keys}"

OUTPUT:
["1", "2"]
```

# **Blocks, Yields, Lambda, Procs**
## **Blocks**
- little anonymous functions that can be passed into methods
- enclosed in a **do / end** statement or between brackets **{}**, and they can have multiple arguments
- argument names are defined between two pipe | characters
```RUBY
# Form 1: recommended for single line blocks
[1, 2, 3].each { |num| puts num }

# Form 2: recommended for multi-line blocks
[1, 2, 3].each do |num|
  puts num
end
```
## **Yields**
- a Ruby keyword that calls a block
- When we use the **yield** keyword, the code inside the block will run & do its work
```RUBY
def print_once
  yield
end

print_once { puts "Block is being run" }

# "Block is being run"

def print_twice
  yield
  yield
end

print_twice { puts "Hello" }

# "Hello"
# "Hello"

def one_two_three
  yield 1 # yield statement is written followed by parameters
  yield 2
  yield 3
end
one_two_three { |number| puts number * 10 }
# 10, 20, 30

def test
   puts "You are in the method"
   yield
   puts "You are again back to the method"
   yield
end
test {puts "You are in the block"}

OUTPUT:
You are in the method
You are in the block
You are again back to the method
You are in the block
```
## **Explicit Blocks**
- Explicit means that you give it a name in your parameter list
- We can pass an explicit block to another method or save it into a variable to use later
```RUBY
def explicit_block(&block)
  block.call # same as yield
end

explicit_block { puts "Explicit block called" }
```
## **Check if a block was given**
```RUBY
def do_something_with_block
  return "No block given" unless block_given? # block_given check whether a block has been passed
  yield
end
```
# **Lambda**
- a way to define a block & its parameters with some special syntax
- we can save this lambda into a variable for later use
```RUBY
say_something = -> { puts "This is a lambda" }
# ways of calling lambda function
say_something.call
say_something.()
say_something[]
say_something.==

OUTPUT:
This is a lambda

# Lambdas can also take arguments
times_two = ->(x) { x * 2 }
times_two.call(10)
# 20
```
## **Procs**
- Lambdas are defined with -> {} and procs with Proc.new {}.
- Procs return from the current method, while lambdas return from the lambda itself.
- Procs don’t care about the correct number of arguments, while lambdas will raise an exception.
```RUBY
t = proc { |x,y| puts "I don't care about arguments!" }
t.call
# "I don't care about arguments!"
```
```RUBY
def call_proc
  puts "Before proc"
  my_proc = proc { return 2 } # returns here and doesn't execute anything beyong this line
  my_proc.call
  puts "After proc"
end
p call_proc

OUTPUT:
Before proc
2
```
# **Closures**
```RUBY
def call_proc(my_proc)
  count = 500
  my_proc.call
end
count   = 1
my_proc = Proc.new { puts count }
p call_proc(my_proc) # What does this print?
```
- because of the 'closure' effect it will print 1
- because the proc is using the value of count from the place where the proc was defined, and that’s outside of the method definition
## **Binding Class**
- When we create a **Binding** object via the binding method, you are creating an ‘anchor’ to this point in the code
- Every variable, method & class defined at this point will be available later via this object, even if we are in a completely different scope
```RUBY
def return_binding
  foo = 100
  binding
end
# Foo is available thanks to the binding,
# even though we are outside of the method
# where it was defined.
puts return_binding.class # prints 'Binding'
puts return_binding.eval('foo') # prints '100'
# If you try to print foo directly you will get an error.
# The reason is that foo was never defined outside of the method.
puts foo # undefined local variable or method 'foo'
```

# **Ranges**
```RUBY
(1..5)        #==> 1, 2, 3, 4, 5
(1...5)       #==> 1, 2, 3, 4
('a'..'d')    #==> 'a', 'b', 'c', 'd'
```
```RUBY
(10..15).each do |n| 
   print n, ' ' 
end

OUTPUT:
10 11 12 13 14 15
```
## **Creating Ranges**
```RUBY
$, =", "   # Array value separator
range1 = (1..10).to_a # to_a converts the range to a list
range2 = ('bar'..'bat').to_a

puts "#{range1}"
puts "#{range2}"

OUTPUT:
[1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
["bar", "bas", "bat"]
```
```RUBY
# Assume a range
digits = 0..9

puts digits.include?(5)
ret = digits.min
puts "Min value is #{ret}"

ret = digits.max
puts "Max value is #{ret}"

ret = digits.reject {|i| i < 5 }
puts "Rejected values are #{ret}"

digits.each do |digit|
   puts "In Loop #{digit}"
end

OUTPUT:
true
Min value is 0
Max value is 9
Rejected values are 5, 6, 7, 8, 9
In Loop 0
In Loop 1
In Loop 2
In Loop 3
In Loop 4
In Loop 5
In Loop 6
In Loop 7
In Loop 8
In Loop 9
```
## **Ranges in Case Statements**
```RUBY
score = 70

result = case score
   when 0..40 then "Fail"
   when 41..60 then "Pass"
   when 61..70 then "Pass with Merit"
   when 71..100 then "Pass with Distinction"
   else "Invalid Score"
end

puts result # prints 'Pass with Merit'
```
```RUBY
if ((1..10) === 5) # use '===' inside 'when' or 'if' clause
   puts "5 lies in (1..10)"
end

if (('a'..'j') === 'c')
   puts "c lies in ('a'..'j')"
end

if (('a'..'j') === 'z')
   puts "z lies in ('a'..'j')"
end

OUTPUT:
5 lies in (1..10)
c lies in ('a'..'j')
```

# **Operators**
- **.eql?** => True if the receiver and argument have both the same type and equal values. eg: 1 == 1.0 returns true, but 1.eql?(1.0) is false
- **.equal?** => True if the receiver and argument have the same object id, eg: if aObj is duplicate of bObj then aObj == bObj is true, a.equal?bObj is false but a.equal?aObj is true.
- ** => power operator, a**b == a<sup>b</sup>

# **Class**
```RUBY
class Customer
   @@no_of_customers = 0
   def initialize(id, name, addr)
      @cust_id = id
      @cust_name = name
      @cust_addr = addr
   end
end

cust1 = Customer.new("1", "John", "Wisdom Apartments, Ludhiya")
cust2 = Customer.new("2", "Poul", "New Empire road, Khandala")
```
```RUBY
MR_COUNT = 0         # constant defined on main Object class
module Foo
   MR_COUNT = 0
   ::MR_COUNT = 1    # set global count to 1
   MR_COUNT = 2      # set local count to 2
end
puts MR_COUNT        # this is the global constant
puts Foo::MR_COUNT   # this is the local "Foo" constant

OUTPUT:
1
2
```
```RUBY
CONST = ' out there'

class Inside_one
   CONST = proc {' in there'}
   def where_is_my_CONST
      ::CONST + ' inside one'
   end
end

class Inside_two
   CONST = ' inside two'
   def where_is_my_CONST
      CONST
   end
end
puts Inside_one.new.where_is_my_CONST
puts Inside_two.new.where_is_my_CONST
puts "#{CONST}" + Inside_two::CONST
puts Inside_two::CONST + CONST
puts Inside_one::CONST
puts Inside_one::CONST.call + Inside_two::CONST

OUTPUT:
out there inside one
inside two
out there inside two
inside two out there
#<Proc:0x0055a030ff61c8@main.rb:5>
in there inside two
```

## **Methods**
- names should begin with a lowercase letter
- If begin with an uppercase letter, Ruby might think that it is a constant and hence can parse the call incorrectly
- should be defined before calling them
```RUBY
def test(a1 = "Ruby", a2 = "Perl")
   puts "The programming language is #{a1}"
   puts "The programming language is #{a2}"
end
test "C", "C++"
test

OUTPUT:
The programming language is C
The programming language is C++
The programming language is Ruby
The programming language is Perl
```
## **Return Values from Methods**
- every method returns a value by **DEFAULT**
- returned valued will be the value of the last statement
``` RUBY
def test
   i = 100
   j = 10
   k = 0    # 'k' will be the return value
end
```
```RUBY
def test
    i = 100
    j = 200
    k = 300
    return i, j, k
end
var = test
puts var

OUTPUT:
100
200
300
```
## **Variable Parameter**
- Ruby allows us to declare methods that work with a variable number of parameters, menaing that the parameter can take in any number of variables
```RUBY
def sample (*test)
   puts "The number of parameters is #{test.length}"
   for i in 0...test.length
      puts "The parameters are #{test[i]}"
   end
end
sample "Zara", "6", "F"
sample "Mac", "36", "M", "MCA"

OUTPUT:
The number of parameters is 3
The parameters are Zara
The parameters are 6
The parameters are F
The number of parameters is 4
The parameters are Mac
The parameters are 36
The parameters are M
The parameters are MCA
```

# **Member Functions**
```RUBY
class Sample
   def hello
      puts "Hello Ruby!"
   end
end

# Now using above class to create objects
object = Sample. new
object.hello

OUTPUT:
Hello Ruby!
```
```RUBY
class Customer
   @@no_of_customers = 0
   def initialize(id, name, addr)
      @cust_id = id
      @cust_name = name
      @cust_addr = addr
   end
   def display_details()
      puts "Customer id #@cust_id"
      puts "Customer name #@cust_name"
      puts "Customer address #@cust_addr"
   end
   def total_no_of_customers()
      @@no_of_customers += 1
      puts "Total number of customers: #@@no_of_customers"
   end
end


# Create Objects
cust1 = Customer.new("1", "John", "Wisdom Apartments, Ludhiya")
cust2 = Customer.new("2", "Poul", "New Empire road, Khandala")

# Call Methods
cust1.display_details()
cust1.total_no_of_customers()
cust2.display_details()
cust2.total_no_of_customers()

OUTPUT:
Customer id 1
Customer name John
Customer address Wisdom Apartments, Ludhiya
Total number of customers: 1
Customer id 2
Customer name Poul
Customer address New Empire road, Khandala
Total number of customers: 2
```
- Ruby gives us a way to access a method without instantiating a class
```RUBY
class Accounts
   def reading_charge # can only be accessed with the instantiation of a class
   end
   def Accounts.return_date # can be accessed without instantiating a class
   end
end

Accounts.reading_charge # ERROR (ILLEGAL)
Accounts.return_date # NO ERROR (LEGAL)
```
## **UNDEF**
- cancels the method definition
```RUBY
undef bar # undefine a method called 'bar'
```

# **Alias**
## **ALIAS**
```RUBY
alias print_something puts # calling 'print_something' is the same as calling 'puts'
print_something 1 # prints '1'
```
## **ALIAS METHODS**
```RUBY
class Microwave
    def on
        puts "The microwave is on"
    end
    alias :start :on
end
m = Microwave.new
m.start # same as m.on, prints "The microwave is on"

class Cat
    def speak
        "meow"
    end
    alias_method "#{name.downcase}_speak", :speak
end
p Cat.new.cat_speak # prints "meow"

class Foo
  alias_method :print_something, :puts
end
```
- Ruby creates a copy of the method, alias is not only a new name
```RUBY
def bacon
  123
end

alias :x :bacon

def bacon
  234
end

x # 'x' stays the same but bacon has been redefined
# 123
bacon # bacon is redefined, it will return '234' instead of '123'
# 234
```

# **Comments**
## **Multiline Comments**
```RUBY
=begin
This is a multiline comment and con spwan as many lines as you
like. But =begin and =end should come in the first line only. 
=end
```

# **LOOPS**
```RUBY
x = 1
if x > 2
   puts "x is greater than 2"
elsif x <= 2 and x!=0
   puts "x is 1"
else
   puts "I can't guess the number"
end

OUTPUT:
1
```

```RUBY
$debug = 1
print "debug\n" if $debug # prints '1'
```

## **UNLESS**
- execute statement when condition is **FALSE**
```RUBY
x = 1 
unless x>=2
   puts "x is less than 2"
 else
   puts "x is greater than 2"
end

OUTPUT:
x is less than 2
```

## **CASE**
```RUBY
$age =  5
case $age
    when 0 .. 2
    puts "baby"
    when 3 .. 6
    puts "little child"
    when 7 .. 12
    puts "child"
    when 13 .. 18
    puts "youth"
    else
    puts "adult"
end

OUTPUT:
little child
```

## **WHILE**
```RUBY
SYNTAX1:
$i = 0
$num = 5

while $i < $num  do
   puts("Inside the loop i = #$i" )
   $i +=1
end

SYNTAX2:
$i = 0
$num = 5
begin
   puts("Inside the loop i = #$i" )
   $i +=1
end while $i < $num

OUTPUT:
Inside the loop i = 0
Inside the loop i = 1
Inside the loop i = 2
Inside the loop i = 3
Inside the loop i = 4
```

## **UNTIL**
- executes code while conditional is **FALSE**
```RUBY
SYNTAX1:
$i = 0
$num = 5
until $i > $num  do
   puts("Inside the loop i = #$i" )
   $i +=1;
end

SYNTAX2:
$i = 0
$num = 5
begin
   puts("Inside the loop i = #$i" )
   $i +=1;
end until $i > $num

OUTPUT:
Inside the loop i = 0
Inside the loop i = 1
Inside the loop i = 2
Inside the loop i = 3
Inside the loop i = 4
Inside the loop i = 5
```

## **FOR**
```RUBY
SYNTAX1:
for i in 0..5
   puts "Value of local variable is #{i}"
end

SYNTAX2:
(0..5).each do |i|
   puts "Value of local variable is #{i}"
end

OUTPUT:
Value of local variable is 0
Value of local variable is 1
Value of local variable is 2
Value of local variable is 3
Value of local variable is 4
Value of local variable is 5
```

## **NEXT / BREAK**
```RUBY
for i in 0..5
   if i > 2 then
        break
    if i == 1
        next # same as CONTINUE
   end
   puts "Value of local variable is #{i}"
end

OUTPUT:
Value of local variable is 0
Value of local variable is 2
```

## **REDO**
```RUBY
for i in 0..5
   if i < 2 then
      puts "Value of local variable is #{i}"
      redo
   end
end

OUTPUT:
Value of local variable is 0
Value of local variable is 0
............................
```

## **RETRY**
- If retry appears in rescue clause of begin expression, restart from the beginning of the begin body
```RUBY
begin
   do_something # exception raised
rescue
   # handles error
   retry  # restart from beginning
end
```
```RUBY
for i in 0..5
   retry if i > 2
puts "Value of local variable is #{i}"
end

OUTPUT:
Value of local variable is 1
Value of local variable is 2
Value of local variable is 1
Value of local variable is 2
Value of local variable is 1
Value of local variable is 2
............................
```

## **BEGIN & END**
- Ruby source file can declare blocks of code to be run as the file is being loaded (the BEGIN blocks) and after the program has finished executing (the END blocks)
- a program may include multiple BEGIN and END blocks. BEGIN blocks are executed in the order they are encountered, while END blocks are executed in reverse order 
```RUBY
BEGIN { 
   # BEGIN block code 
   puts "BEGIN code block 1"
} 

BEGIN { 
   # BEGIN block code 
   puts "BEGIN code block 2"
}

END { 
   # END block code 
   puts "END code block 1"
}

END { 
   # END block code 
   puts "END code block 2"
}

   # MAIN block code 
puts "MAIN code block"

OUTPUT:
BEGIN code block 1
BEGIN code block 2
MAIN code block
END code block 2
END code block 1
```

# **Modules**
- Modules are a way of grouping together methods, classes, and constants
- Modules provide a namespace and prevent name clashes
- Modules implement the mixin facility
- Modules define a **namespace**, a sandbox in which your methods and constants can play without having to worry about being stepped on by other methods and constants
- Module constants are named just like class constants, with an **initial uppercase letter**
- Whenever you define a method in a module, you specify the module name followed by a dot and then the method name
- If a third program wants to use any defined module, it can simply load the module files using the Ruby **require** statement
```RUBY
# Module defined in trig.rb file

module Trig
   PI = 3.141592654
   def Trig.sin(x)
   # ..
   end
   def Trig.cos(x)
   # ..
   end
end

# Module defined in moral.rb file

module Moral
   VERY_BAD = 0
   BAD = 1
   def Moral.sin(badness)
   # ...
   end
end
```
## **Importing Modules**
```RUBY
$LOAD_PATH << '.' 
# we use '$LOAD_PATH' to make Ruby aware that included files must be searched in current directory
# we can use 'require_relative' to include files from a relative directory

require 'trig.rb'
require 'moral'

y = Trig.sin(Trig::PI/4)
wrongdoing = Moral.sin(Moral::VERY_BAD)

# although the files contain the same function name, we resolve the ambiguity by using the module name
```
## **INCLUDE Statement**
```RUBY
# module defined in support.rb file

module Week
   FIRST_DAY = "Sunday"
   def Week.weeks_in_month
      puts "You have four weeks in a month"
   end
   def Week.weeks_in_year
      puts "You have 52 weeks in a year"
   end
end
```
```RUBY
$LOAD_PATH << '.'
require "support"

class Decade
include Week # include "week" module from support.rb into "Decade" class
   no_of_yrs = 10
   def no_of_months
      puts Week::FIRST_DAY
      number = 10*12
      puts number
   end
end
d1 = Decade.new
puts Week::FIRST_DAY
Week.weeks_in_month
Week.weeks_in_year
d1.no_of_months

OUTPUT:
Sunday
You have four weeks in a month
You have 52 weeks in a year
Sunday
120
```
## **MIXIN**
- **Mixin** give us a wonderfully controlled way of adding functionality to classes
- **Mixin** is similar to multiple inheritance in Object Oriented Programming
```RUBY
module A
   def a1
   end
   def a2
   end
end
module B
   def b1
   end
   def b2
   end
end

class Sample
include A
include B
   def s1
   end
end
# "Sample" can access all four methods, namely a1,a2,b1 & b2
# We can say that "Sample" shows multiple inheritance or a mixin

samp = Sample.new
samp.a1
samp.a2
samp.b1
samp.b2
samp.s1
```

# **Date & Time**
## **Getting Current Date & Time**
```RUBY
time = Time.new

# Components of a Time
puts "Current Time : " + time.inspect
puts time.year    # => Year of the date 
puts time.month   # => Month of the date (1 to 12)
puts time.day     # => Day of the date (1 to 31 )
puts time.wday    # => 0: Day of week: 0 is Sunday
puts time.yday    # => 365: Day of year
puts time.hour    # => 23: 24-hour clock
puts time.min     # => 59
puts time.sec     # => 59
puts time.usec    # => 999999: microseconds
puts time.zone    # => "UTC": timezone name

OUTPUT:
Current Time : Mon Jun 02 12:03:08 -0700 2008
2008
6
2
1
154
12
3
8
247476
UTC
```
```RUBY
# Components in the "Time" array are stored in the format below
[sec,min,hour,day,month,year,wday,yday,isdst,zone]

time = Time.new
values = time.to_a
p values

# [26, 10, 12, 2, 6, 2008, 1, 154, false, "MST"]
```
```RUBY
time = Time.new
values = time.to_a
puts Time.utc(*values)

# Mon Jun 02 12:15:36 UTC 2008
```
## **Formatting Times and Date**
```RUBY
time = Time.new
puts time.strftime("%Y-%m-%d %H:%M:%S")
# 2008-06-02 12:35:19
```

# **File I/O**
## **PUTS**
- Instructs the program to display the value stored in the variable
- Add a new line at the end of each line it writes

## **GETS**
- can be used to take any input from the user from standard screen called STDIN
```RUBY
puts "Enter a value :"
val = gets # get inputs from user
puts val
```

## **PUTC**
- Unlike the puts statement, which outputs the entire string onto the screen, the putc statement can be used to output one character at a time
```RUBY
str = "Hello Ruby!"
putc str # prints 'H'
```

## **PRINT**
- similar to the puts statement
- only difference is that the puts statement goes to the next line after printing the contents, whereas with the print statement the cursor is positioned on the same line
```RUBY
print "Hello World"
print "Good Morning"

OUTPUT:
Hello WorldGood Morning
```

## **Opening and Closing Files**
- We can create a File object using **File.new** method for reading, writing, or both, according to the mode string, we can then use **File.close** method to close that file
```RUBY
aFile = File.new("filename", "mode")
   # ... process the file
aFile.close

# The difference between File.open and File.new is that the File.open method can be associated with a block, whereas you cannot do the same using the File.new method
File.open("filename", "mode") do |aFile|
   # ... process the file
end
```

## **Sysread & Syswrite**
- we can use the method sysread to read the contents of a file
```RUBY
# input.txt
This is a simple text file for testing purpose.

aFile = File.new("input.txt", "r")
if aFile
   content = aFile.sysread(20) # output the first 20 characters of the file
   puts content
else
   puts "Unable to open file!"
end

aFile = File.new("input.txt", "r+")
if aFile
   aFile.syswrite("ABCDEF") # write "ABCDEF" into 'input.txt'
else
   puts "Unable to open file!"
end
```

# **Exceptions**
Everything from begin to rescue is protected. If an exception occurs during the execution of this block of code, control is passed to the block between rescue and end.

For each rescue clause in the begin block, Ruby compares the raised Exception against each of the parameters in turn. The match will succeed if the exception named in the rescue clause is the same as the type of the currently thrown exception, or is a superclass of that exception.

In an event that an exception does not match any of the error types specified, we are allowed to use an else clause after all the rescue clauses
```RUBY
begin  
# -  
rescue OneTypeOfException  
# -  
rescue AnotherTypeOfException  
# -  
else  
# Other exceptions
ensure
# Always will be executed
end
```

## **RAISE**
```RUBY
begin  
   puts 'I am before the raise.'  
   raise 'An error has occurred.'  
   puts 'I am after the raise.'  
rescue  
   puts 'I am rescued.'  
end  
puts 'I am after the begin block.' 

OUTPUT:
I am before the raise.  
I am rescued.  
I am after the begin block. 
```
```RUBY
begin  
   raise 'A test exception.'  
rescue Exception => e  
   puts e.message  
   puts e.backtrace.inspect  
end  

OUTPUT:
A test exception.
["main.rb:4"]
```

## **ENSURE**
- ensure goes after the last rescue clause and contains a chunk of code that will always be executed as the block terminates. It doesn't matter if the block exits normally, if it raises and rescues an exception, or if it is terminated by an uncaught exception, the ensure block will get run
```RUBY
begin
   raise 'A test exception.'
rescue Exception => e
   puts e.message
   puts e.backtrace.inspect
ensure
   puts "Ensuring execution"
end

OUTPUT:
A test exception.
["main.rb:4"]
Ensuring execution
```

## **ELSE**
- The body of an else clause is executed only if no exceptions are raised by the main body of code
```RUBY
begin
   # raise 'A test exception.'
   puts "I'm not raising exception"
rescue Exception => e
   puts e.message
   puts e.backtrace.inspect
else
   puts "Congratulations-- no errors!"
ensure
   puts "Ensuring execution"
end

OUTPUT:
I'm not raising exception
Congratulations-- no errors!
Ensuring execution
```

## **THROW & CATCH**
```RUBY
def promptAndGet(prompt)
   print prompt
   res = readline.chomp
   throw :quitRequested if res == "!"
   return res
end

catch :quitRequested do
   name = promptAndGet("Name: ")
   age = promptAndGet("Age: ")
   sex = promptAndGet("Sex: ")
   # ..
   # process information
end
promptAndGet("Name:")

OUTPUT:
Name: Ruby on Rails
Age: 3
Sex: !
Name:Just Ruby
```