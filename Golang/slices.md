# **Slices**
- lightweight data structure of variable length sequence for storing homogeneous data, **more convenient, powerful and flexible** than array
- has 3 components:
1. pointer - This is used for pointing to the first element of the array accessible via slice, doesn’t need to be the first element of the array
2. length - This is used for representing the total elements count present in the slice.
3. capacity - This represents the capacity up to which the slice can expand.

![slice](https://d3n0h9tb65y8q.cloudfront.net/public_assets/assets/000/001/744/original/slice.png?1637335112)

- In `Go` when we assign or pass around an array between functions, we will need to make a copy of the entire content (not efficient)
- slices is more efficient, it doesnt copy the slice / array data, it creates a new slice value that points to the original array. Therefore modifying the slement of re-slice modifies the elements of original slices
- slices cannot grown beyond its capacity
- to increase a slices capacity we must create a new & larger slice, and copy the contents of the original slice into it
```golang
// arrays, we specify the element count
var a [4] int
b := [2]string{"Penn","Taylor"}
b := [...]string{"Penn","Taylor"} // let the compiler count number of elements for us

// slices, we leave out the element count
letters := []strings{"a","b","c","d"}
```
```golang
s := make([]byte,5)
len(s) // == 5
cap(s) // == 5

s = s[2:4] 
len(s) // == 2, as it's containing the 2nd and 3rd element of s
cap(s) // == 3, as we slice 's' starting from the 2nd element onwards
```
- slice doesn't make a copy of the underlying array, the full array will be kept in memory until it's no longer referenced (the garbage collecter will do the cleaning itself). Hence its a good practice to make a new slice and copy the results / value that we need and return in a function (so the garbage collecter can release the array)
## **Append**
- `Go` provides built-in `append` function to append new elements to the end of a slice, and grows the slice if a greater capacity is needed
```golang
a := make([]int,1)
// a == []int {0}
a = append(a,1,2,3)
// a == []int{0,1,2,3}

a := []string{"John","Paul"}
b := []string{"Kelvin","Alex"}
a = append(a,b...) // equivalent to append(a,b[0],b[1],b[2])
// a == []string{"John","Paul","Kelvin","Alex"}
```