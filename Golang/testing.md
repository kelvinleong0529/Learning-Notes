# **Testing**
- `testing` package is used for testing in Golang
- **test files** must end with `_test.go` suffix, and every test functions must begin with `Test...(function name)` prefix, with `(t *testing.T)` as the function parameter 
- consider the following directory structure:
```
├───numbers
        numbers.go
        numbers_test.go
```
```golang
// numbers.go
package main 

func Add(x int, y int) int {
    return x + y
}

func Minus (x int, y int) int {
    return x - y
}

// numbers_test.go
package main

import "fmt"

func TestAdd(t *testing.T) {P
    num1 := 10
    num2 := 20
    actualResult := Add(num1, num2)
    expectedResult := 30
    if actualResult != expectedResult {
        t.Errorf("Expected result = %d, actual result = %d",expectedResult, actualResult)
    }
}

func TestMinus(t *test) {
    num1 := 100
    num2 := 20
    actualResult := Add(num1, num2)
    expectedResult := 80
    if actualResult != expectedResult {
        t.Errorf("Expected result = %d, actual result = %d",expectedResult, actualResult)
    }
}
```
- run the following command to perform / execute the testing (remember to cd to **numbers** folder):
```
go test
```