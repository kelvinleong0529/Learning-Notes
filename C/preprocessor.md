# **C Preprocessor and Macros**
![Preprocessor and Macros](https://cdn.programiz.com/sites/tutorial2program/files/c-preprocessor.jpg)
- `C preprocessor` is a `macro processor` (allow users to define macros) that transforms our program before it is compiled
- all preprocessing directivves begin with a `#` symbol, for example:
```C
# define PI 3.14
```

## **Header files**
- `# include` preprocessor is used to include header files to C program, for example:
```C
# include <stdio.h>
# include "myheader.h"
```
- `studio.h` is a header file, the `# include` preprocessor directive replaces the above line with the contents of `studio.h` header file, and this is the reason why we need to use `# include <studio.h>` before we can use functions like `scanf()` and `printf()`

## **Macros**
- `macro` is a fragment of code that is given a name
```C
#include <stdio.h>
#define PI 3.1415

int main()
{
    float radius, area;
    printf("Enter the radius: ");
    scanf("%f", &radius);

    // Notice, the use of PI
    area = PI*radius*radius;

    printf("Area=%.2f",area);
    return 0;
}
```
- we can also define macros that work in a similar way as a function call, this is knows as **function-like macros**
```C
# define circleArea(r) (3.1415*(r)*(r))
// everytime thr program encounters circleArea(argument), it is replaced by (3.1415**argument*argument)

// for example:
// circleArea(5) => (3.1415*5*5)
```

## **Conditional Compilation**
- In `C` programming, we can instruct the preprocessor whether to include a block of code or not by using `conditional directives`
- it's similar to `if` statement, major difference being is that `if` statement is being tested during the execution time to check whether a block of code should be executed or not, whereas the conditionals are used to include (or skip) a block of code in our program before execution
- uses of `conditional compilation`:
1. use different code depending on the mahcine, OS
2. compile the same source file into 2 different programs
3. exclude certain code from the program but to keep it as a reference for future purposes

```C
# ifdef MACRO
    // conditional codes
# endif
// here the conditional codes are included in the program only in MACRO is defined
```
```C
# if expression
    conditional codes if expression is non-zero
# elif expression 1
    conditional codes if expression1 is non-zero
# else
    conditional if expression is 0
# endif
// expression is an expression on integer type, conditional codes will only be included if the expression is evaluated to a non-zero value
```
```C
# if defined BUFFER_SIZE && BUFFER_SIZE >= 2048
// defined keyword is used to test whether a macro is defined or not
```

## **Predefined Macros**
1. **__DATE__** => string containing the current date
2. **__FILE__** => string containing the file name
3. **__LINE__** => integer representing the current line number
4. **__TIME__** => string containing the current time

## **typedef**
- we can use `typedef` to give a type a new name, and usually we use uppercase letters for these definitions to remind the user that the type name is really a symbolic abbreviation
```C
typedef unsigned char BYTE
```
- we can use `typedef` to give name to self-defined data types as well
```C
#include <stdio.h>
#include <string.h>
 
typedef struct Books {
   char title[50];
   char author[50];
   char subject[100];
   int book_id;
} Book;
 
int main( ) {

   Book book;
 
   strcpy( book.title, "C Programming");
   strcpy( book.author, "Nuha Ali"); 
   strcpy( book.subject, "C Programming Tutorial");
   book.book_id = 6495407;
 
   printf( "Book title : %s\n", book.title);
   printf( "Book author : %s\n", book.author);
   printf( "Book subject : %s\n", book.subject);
   printf( "Book book_id : %d\n", book.book_id);

   return 0;
}

// output:
Book title : C Programming
Book author : Nuha Ali
Book subject : C Programming Tutorial
Book book_id : 6495407
```
- `typedef` is limited to giving symbolic names to types only where as `#define` can be used to define alias for values as well
- `typedef` interpretation is performed by the compiler whereas `#define` statements are processed by the pre-processor