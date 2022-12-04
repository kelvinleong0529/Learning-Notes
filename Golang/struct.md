# **Empty Structs**
- empty struct `struct{}` is realized in a special way in Go
1. it's the smallest building block in Go, it's size is literally **0 bytes**
2. if it has zero size, we may create a slice of 1000's empty structures and this slice will be very tiny, because Go stores only a number of them in the slice but not them itself, this logic applies for channels as well
3. all pointer to it always point to the same special place in memory
4. it's very useful in channels when we notify about some event but we don't need to pass any information about it, only a fact. Best solution is to pass an empty structure because it will only increment a counter in the channel not assign memory, copy elements and so on. Sometime people use boolean values for this purpose, but it's much worse
5. zero size containers for methods, sometimes we may want to have a mock for testing interfaces, often we don't need data on it, just methods with predefined input and output
6. go has no `Set` object, bit can be easily realized as a `map[KeyType]struct{}`, this way map keeps only keys and no values

# **Signal Channels**
- `channels` are a great way to communicate data between goroutines, but we can also use them just for signalling
- when doing this, it's a good practice to use `empty struct` as the type of the channel, since they're pretty useless for anything other than signalling, and it does not taking up much space in memory - since `empty struct` has no fields inside it, hence the memory consumption is very low
```golang
var signal chan struct{} // a signal channel that takes empty struct as the type
signal := make(chan struct{}) // make a signal channel

// code can block waiting for something to be sent on the channel
<- signal

// since it's only a signaling channel, we don't really care about the value, which is why we don't assign it to anything
// closing the channel "signal", will unblock the above statement, allowing execution to continue
```

## **Wait for something to finish**
- by blocking on a signal channel, we can wait for a task in another gorotuine to finish:
```golang
done := make(chan struct{})
go func() {
  doLongRunningThing()
  close(done)
}()
// do some other bits
// wait for that long running thing to finish
<-done
// do more things
```

## **Start lots of things at the same time**
- if we queue up lots of goroutines, we can have them all start at the same time by closing the signal channel
```golang
start := make(chan struct{})
for i := 0; i < 10000; i++ {
  go func() {
    <-start // wait for the start channel to be closed
    doWork(i) // do something
 }()
}
// at this point, all goroutines are ready to go - we just need to 
// tell them to start by closing the start channel
close(start)
```

## **Stopping things**
- we can use the technique above to stop goroutines too
- if the `stop` channel below is closed the for loop will exit and no more emails will be sent
```golang
loop:
for {
  select {
  case m := <-email:
    sendEmail(m)
  case <-stop: // triggered when the stop channel is closed
    break loop // exit
  }
}
```