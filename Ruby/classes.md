# **Classes**
## **Classess Definition**
- **Initialize Method** works the same as **constructor** in other OOP
```RUBY
class Box
   def initialize(w,h) 
      @width, @height = w, h
   end
end
```
## **Accessor & Setter Methods**
- To make the variables available from outside the class, they must be defined within accessor methods, these accessor methods are also known as a getter methods
```RUBY
class Box
   # constructor method
   def initialize(w,h)
      @width, @height = w, h
   end

   # accessor methods
   def printWidth
      @width
   end

   def printHeight
      @height
   end
end

# create an object
box = Box.new(10, 20)

# use accessor methods
x = box.printWidth()
y = box.printHeight()

puts "Width of the box is : #{x}"
puts "Height of the box is : #{y}"

OUTPUT:
Width of the box is : 10
Height of the box is : 20
```
- Similar to accessor methods, which are used to access the value of the variables, Ruby provides a way to set the values of those variables from outside of the class using setter methods
```RUBY
class Box
    # constructor method
    def initialize(w,h)
        @width, @height = w, h
    end

    # accessor methods
    def getWidth
        @width
    end
    def getHeight
        @height
    end

    # setter methods
    def setWidth=(value)
        @width = value
    end
    def setHeight=(value)
        @height = value
    end
end

# create an object
box = Box.new(10, 20)

# use setter methods
box.setWidth = 30
box.setHeight = 50
```

## **Instances Method**
```RUBY
class Box
   # constructor method
   def initialize(w,h)
      @width, @height = w, h
   end
   # instance method
   def getArea
      @width * @height
   end
end

# create an object
box = Box.new(10, 20)

# call instance methods
a = box.getArea()
```

## **Class Methods & Variables**
```RUBY
class Box
    # Initialize our class variables
    @@count = 0
    def initialize(w,h)
        # assign instance avriables
        @width, @height = w, h

        @@count += 1
    end

    def self.printCount()
        puts "Box count is : #@@count"
    end
end

# create two object
box1 = Box.new(10, 20)
box2 = Box.new(30, 100)

# call class method to print box count
Box.printCount()

OUTPUT:
Box count is : 2
```

## **to_s method**
- Any class we define should have a to_s instance method to return a string representation of the object
```RUBY
class Box
   # constructor method
   def initialize(w,h)
      @width, @height = w, h
   end
   # define to_s method
   def to_s
      "(w:#@width,h:#@height)"  # string formatting of the object.
   end
end

# create an object
box = Box.new(10, 20)

# to_s method will be called in reference of string automatically.
puts "String representation of box is : #{box}"

OUTPUT:
String representation of box is : (w:10,h:20)
```

## **Access Control**
1. Public Methods − Public methods can be called by anyone. Methods are public by default except for initialize, which is always private.
2. Private Methods − Private methods cannot be accessed, or even viewed from outside the class. Only the class methods can access private members.
3. Protected Methods − A protected method can be invoked only by objects of the defining class and its subclasses. Access is kept within the family.
```RUBY
class Box
   # constructor method
   def initialize(w,h)
      @width, @height = w, h
   end

   # instance method by default it is public
   def getArea
      getWidth() * getHeight
   end

   # define private accessor methods
   def getWidth
      @width
   end
   def getHeight
      @height
   end
   # make them private
   private :getWidth, :getHeight

   # instance method to print area
   def printArea
      @area = getWidth() * getHeight
      puts "Big box area is : #@area"
   end
   # make it protected
   protected :printArea
end

# create an object
box = Box.new(10, 20)

# call instance methods
a = box.getArea()
puts "Area of the box is : #{a}"

# try to call protected or methods
box.printArea()

OUTPUT:
Area of the box is : 200
test.rb:42: protected method `printArea' called for #
<Box:0xb7f11280 @height = 20, @width = 10> (NoMethodError)
```

## **Inheritance**
- Ruby does not support multiple levels of inheritances but Ruby supports **mixins**
- When creating a class, instead of writing completely new data members and member functions, the programmer can designate that the new class should inherit the members of an existing class. This existing class is called the **base class** or **superclass**, and the new class is referred to as the **derived class** or **sub-class**