# **Annotations**
- Annotations start with ‘@’
- Annotations do not change the action of a compiled program.
- Annotations help to associate metadata (information) to the program elements, eg instance variables, constructors, methods, classes, etc.
- Annotations are not pure comments as they can change the way a program is treated by the compiler. See below code for example.
- Annotations basically are used to provide additional information, so could be an alternative to XML and Java marker interfaces.

# **Built-In Annotations**
## **@Override**
- assures that the subclass method is overring the parent class method, if it is not so, compile time error occurs
```java
class Animal{  
void eatSomething(){System.out.println("eating something");}  
}  
  
class Dog extends Animal{  
@Override  
void eatsomething(){System.out.println("eating foods");} 
// spelling mistake, should be eatSomething  
}  
  
class TestAnnotation1{  
public static void main(String args[]){  
Animal a=new Dog();  
a.eatSomething();  
}} 
// Output: Compile Time Error
```
## **@SuppressWarnings**
- used to suppress warnings issued by the compiler
## **@Deprecated**
- marks a particular method is deprecated so compiler prints warning
- informs user that it may be removed in future version

# **Custom Annotations**
- create a Java custom annotation as below:
```java
@interface MyAnnotation{}
```
- java custom annotation signatures:
1. Method should not have any throws clauses
2. Method should return one of the following: primitive data types, String, Class, enum or array of these data types.
3. Method should not have any parameter.
4. We should attach @ just before interface keyword to define annotation.
5. It may assign a default value to the method.

# **Types of Annotation**
## **Marker Annotation**
- an annotation that has no method, eg: `@Override` and `@Deprecated`
## **Single-Value Annotation**
- an annotation that has one method
```java
@interface MyAnnotation{
    int value();
}

// we can provide the default value also
@interface MyAnnotation{
    int value() default 0;
}

// to apply single-value annotation
@MyAnnotation(value=10)
```
## **Multi-Value Annotation**
- an annotation that has more than one method
```java
@interface MyAnnotation{
    int value1();
    String value2();
    String value3();
}

// we can provide the default value also
@interface MyAnnotation{
    int value1() default 1;
    String value2() default "";
    String value3() default "xyz";
}

// to apply multi-value annotation
@MyAnnotation(value1=10,value2="Hello World",value3="This is Java")
```