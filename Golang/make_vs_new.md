# **Make VS New**
## **Similarities**
- both are building functions that allocates memory to instantiate variable for given type

## **Data Types**
- `make()` only works with **slices, maps and channels**
- `new()` works with any data types
```golang
s := make([]int,0)
m := make(map[int]int)
c := make(chan bool)

i := new(int)
```

## **Returned Types**
- `make()` returns the target type
- `new()` returns the address (returns a pointer to nil)
```golang
var v map[int]int = make(map[int]int)
var p *map[int]int = new(map[int]int)
```

## **Memory Initialization**
- `make()` initializes memory
- `new()` zeros memory
```golang
var mMake map[int]int = make(map[int]int) // Initializes a map
var mNew *map[int]int = new(map[int]int) // Doesnt initialize a map object, zeros a map pointer to nil

mMake[0] = 1    // Runs
(*mNew)[0] = 1  // Crashes, because map object hasnt been instantiated yet, and we are dereferencing a nil pointer
```