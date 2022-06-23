# **Goroutine**
- lighweight execution thread in Go programming language and a function that executes concurrently with the rest of the program
- incredibly cheap when compared to traditional threads as the overhead of creating goroutine is very low
- **main** goroutine must be running for any other goroutine to run, if **main** goroutine terminates, then the program will exit and no other goroutine will run
```golang
package main
import (
    "fmt"
    "time"
)

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
package main
import "fmt"

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

# **Resource Pool**
- Pool in golang is to create a fixed number or a pool of things for us
- Commonly used to constraint things that are expensive
- A fixed number of resources (pool) will be created, and subsequent request will be able to gain access to these resources
- `GET()` method will check whether are any available instances in the pool to return to the caller, if no it will use `NEW()` member to create the instances required
- when the caller finish using the instances that the caller had acquired access to, it will call the `PUT()` method to place the instances back to the pool