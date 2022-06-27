# **Goroutine**
- lighweight execution thread in Go programming language and a function that executes concurrently with the rest of the program
- incredibly cheap when compared to traditional threads as the overhead of creating goroutine is very low
- **main** goroutine must be running for any other goroutine to run, if **main** goroutine terminates, then the program will exit and no other goroutine will run
```golang
// Prints numbers from 1-3 along with the passed string
func foo(s string) {
    for i := 1; i <= 3; i++ {
        time.Sleep(100 * time.Millisecond)
        fmt.Println(s, ": ", i)
    }
}

func main() {
    
    // Starting two goroutines
    go foo("1st goroutine")
    go foo("2nd goroutine")

    // Wait for goroutines to finish before main goroutine ends
    time.Sleep(time.Second)
    fmt.Println("Main goroutine finished")
}
```

# **Gochannel**
- in **Golang**, channels are a means through which different **goroutine** communicate
- think of them as pipes through which we can connect with different concurrent goroutines, communication is bidirectional by default
- by default, channels send and receive until the other side is ready, allowing goroutine to synchronize without explicit locks or condition variables
```golang
make (chan [value-type]) // make a channel, where [value-type] is the data type of the values to send and recive, eg: int

// '<-' is the channel operator

// send values
channel <-

// receive values
<- channel

close (channel) // close a channel

// both sending and receiving are blockign operations by default
```

```golang
// Prints a greeting message using values received in
// the channel
func greet(c chan string) {

	name := <- c	// receiving value from channel
	fmt.Println("Hello", name)
}

func main() {

	// Making a channel of value type string
	c := make(chan string)

	// Starting a concurrent goroutine
	go greet(c)

	// Sending values to the channel c
	c <- "World"

	// Closing channel
	close(c)
}
```
- `select` statement let's a goroutine wait on multiple communication operations
- `select` blocks until one of it's cases can run, then it executes that case, it then chosoes one at random if multiple are ready
```golang
func main() {
    ninja1 := make(chan string)
    ninja2 := make(chan string)

    go captainElect(ninja1, "Ninja 1")
    go captainElect(ninja2, "Ninja 2")

    // the select statement will block until one of the cases is ready for execution
    // in the case of multiple cases are ready, it will pick one randomly
    select {
    case message := <- ninja1:
        fmt.Println(message)
    case message := <- ninja2:
        fmt.Println(message)
    default:
    // this will get executed if neither one of the cases above is fulfilled
        fmt.Printlin("Neither")
    }
}

func captainnElect(ninja chan string, message string) {
    ninja <- message
}
```

# **WaitGroup**
- an alternative for Goroutine synchronization
```golang
func main () {
    go atatck("Tommy")
}

func attack(evilNinja string) {
    fmt.Println("Attacked evil ninja:",evilNinja)
}

// if we run this program, it will not print anything out
// because the main() function will finish its execution before the goroutine attack() finishes
```
```golang
func main() {
    var beeper sync.WaitGroup
    beeper.Add(1) // specify we only need to wait for 1 goroutine
    
    go attack("Tommy",&beeper) 
    // need to pass the WaitGroup as pointer
    // else will get deadlock as the changes on WaitGroup is done on the local copy
    
    beeper.Wait() // pause until the WaitGroup has collected all the goroutine signals
    
    fmt.Println("Mission Complete")
}

func attack (ninja string, beeper *sync.WaitGorup) {
    fmt.Println("Attacked evil ninja:",ninja)
    beeper.Done()
}
```
```golang
func main() {
    var evilNinjas []string = {"Tommy","Johnny","Boby"}
    var beeper sync.WaitGroup
    beeper.Add(len(evilNinjas))
    for _,ninjas := range evilNinjas {
        go attack(ninjas,&beeper)
    }
    beeper.Wait()
    fmt.Println("Mission Completed")
}

func attack (ninja string, beeper *sync.WaitGroup) {
    fmt.Println("Attacked Ninja:",ninja)
    beeper.Done()
}
```
# **Mutex**
## **1. Regular Mutex**
```golang
var (
    count int
    lock sync.Mutex
)

func main() {
    var numIterations int = 1000
    for i:= 0; i<numIterations; i++ {
        go increment()
    }
    time.Sleep(time.Second)
    fmt.Println("Resulted count is:",count)
}

func increment() {
    lock.Lock() // acquire the Mutex
    count++
    lock.Unlock() // release the Mutex
    // using Mutex to ensure the function operation is atomic
    // ensure at any time only a single goroutine have access to the "count" var
}
```
## **Read Write Mutex**
- RWMutex is a read/writer mutual exclusion lock
- this lock can be held by any number of readers OR a single writer
```golang
var (
    lock sync.Mutex
    rwLock sync.RWMutex
    count int
)

func main() {
    go read()
    go read()
    go write()
}

func read() {
    rwLock.RLock() // acquire the READ lock
    defer rwLock.RUnlock()

    fmt.Println("Read locking")
    time.Sleep(time.Second)
    fmt.Println("Read Unlocking")
}

func write() {
    rwLock.Lock() // acquire the WRITE lock
    // this lock will block until all the READ lock has been released
    rwLock.Unlock()

    fmt.Println("Write locking")
    time.Sleep(time.Second)
    fmt.Println("Write Unlocking")
}

// output:
Read locking
Read locking
Read Unlocking
Read Unlocking
Write locking
Write Unlocking
// the Write lock can only be acquire after the all the READ lock has released the lock
```

# **Once**
- a feature in sync package that allows us to call a certain function for only one time
```golang
// global variable
var (
    completed bool
)

func main() {
    var once sync.Once
    var waitGroup sync.WaitGroup

    waitGroup.Add(100)
    for i:= 0; i<100;i++ {
        go func() {
            if foundTreasure() {
                once.Do(markMissionCompleted)
                // the once.Do() here ensure the funciton inside is only executed once
            }
            waitGroup.Done()
        }()
    }

    waitGroup.Wait()
    checkMissionCompletion()
}

func checkMissionCompletion() {
    if completed {
        fmt.Println("Mission Completed!")
    } else {
        fmt.Println("Mission Failed")
    }
}

func markMissionCompleted() {
    completed = true
    fmt.Println("Found Treasure!")
}

func foundTreasure() bool {
    rand.Seed(time.Now().UnixNano())
    return 0 == rand.Intn(10)
}

// output:
Found Treasure!
Mission Completed!
```

# **Resource Pool**
- Pool in golang is to create a fixed number or a pool of things for us
- Commonly used to constraint things that are expensive
- A fixed number of resources (pool) will be created, and subsequent request will be able to gain access to these resources
- `GET()` method will check whether are any available instances in the pool to return to the caller, if no it will use `NEW()` member to create the instances required
- when the caller finish using the instances that the caller had acquired access to, it will call the `PUT()` method to place the instances back to the pool
```golang
func main() {
    var numMemPieces int
    memPool := &sync.Pool{
        New : func() interface() {
            numMemPieces++
            mem := make([]byte,1024)
            return &mem
        }
    }

    const numWorkers = 1024*1024

    var wg sync.WaitGroup
    wg.Add(numWorkers)
    for i:= 0; i<numWorkers; i++ {
        go func() {
            mem := memPool.Get().(*[]byte)
            // tries to get the resources from the Pool
            // if failed to get the resources
            // then call the "New" method defined in sync.Pool
            memPool.Put(mem)
            // return the resource back to the Pool
            wg.Done()
        }
    }
    wg.Wait()
    fmt.Println("%d numMemPieces were created",numMemPieces)
}
```

# **Signal & Broadcast**
- can think of it as a mutex that waits on other goroutines (singal)
- blocks until the mutex releases a signal
- Broadcasting - passing a message to multiple goroutines
```golang
var ready bool

func signalFunction() {
    cond := sync.NewCond(&sync.Mutex{})
    go gettingReady(cond)
    var workIntervals int = 0
    cond.L.Lock()
    for !ready {
        workIntervals++
        cond.Wait() // blocks here until "cond" releases the signal
    }
    cond.L.Unlock()
}

func gettingReady(cond *sync.Cond) {
    randTime := rand.Seed(time.Now().UnixNano())
    time.Sleep(time.Second*randTime*10)
    ready = true
    cond.Signal()
}
```
```golang
func stanbyForMission(fn func(), broadcaster *sync.Cond) {
    var wf sync.WaitGroup
    wg.Add(1)
    go func() {
        wg.Done()
        broadcaster.L.Lock()
        defer broadcaster.L.Unlock()
        broadcaster.Wait() // wait for the broadcasting signal
        fn()
    }()
    wg.Wait()
}

func main() {
    beeper := sync.NewCond(&sync.Mutex{})
    var wg sync.WaitGroup
    wg.Add(3)
    stanbyForMission(func(){
        fmt.Println("Ninja 1 starting mission")
        wg.Done()
    },beeper)
    stanbyForMission(func(){
        fmt.Println("Ninja 2 starting mission")
        wg.Done()
    },beeper)
    stanbyForMission(func(){
        fmt.Println("Ninja 3 starting mission")
        wg.Done()
    },beeper)
    beeper.Broadcast()
    wg.Wait()
    fmt.Println("All Ninjas have started their missions")
}
```

# **Concurrent Maps**
- regular maps do not support concurrent operations
- `Store()` to put / insert a new key-value pair
- `Load()` to get a value by key
- `Delete()` to delete a key-value pair (with key as input)
- `LoadAndDelete()` deletes the value for a key, and try to return the previous value if any
- `LoadOrStore()` try to get the value from the map, and if there isnt a value for the key then INSERT
```golang
// REGULAR MAPS
map := make(map[int]interface{})

map[0] = 0
map[1] = 1
map[2] = 2

value, ok = map[0] // ok returns true if the key exists

map[0] = nil // delete in regular map

// SYNC MAP
syncMap := sync.Map{}

syncMap.Store(0,a) // 0 is the key and a is the value
syncMap.Store(1,b)
syncMap.Store(2,c)

syncValue, syncOk := syncMap.Load(0) // check and try to retrieve the value of "0" key

syncMap.Delete(1) // Delete the key "1"

syncMap.LoadAndDelete(1) // delete the value for "1", and try to return the value if possible
```
```golang
func main() {
    syncMap := sync.Map{}
}
```