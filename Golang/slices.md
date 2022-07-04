# **Slices**
- In `Go` when we assign or pass around an array between functions, we will need to make a copy of the entire content (not efficient)
- slices is more efficient, it doesnt copy the slice / array data, it creates a new slice value that points to the original array. Therefore modifying the slement of re-slice modifies the elements of original slices
- 3 main parts of slices: pointer to the array, length of the segment, capacity (maximum length of the segment)
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