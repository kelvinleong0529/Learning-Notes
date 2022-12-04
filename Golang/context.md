# **Context**
- when developing a large application, especially in server software, seomtimes it's helpful for a function to know more about the environment it's being executed
- for example, if a client made a response to the server, and the client got disconnected before receiving the response. If the server function serving the response doesn't know the client disconnected, the server software may end up spending more computing time and resources that it needs to calculating a response that will never be used
- if the above case, being aware of the context of the request, such as the client's connection status, allowas the server to stop processing the request once the clients got disconnected. This saves valuable compute resources on a busy server and frees them up to handle another client's request. This type of information can also be helpful in other contexts where functions take time to execute, such as making database calls
- to enable ubiquitous access to this type of information, Go has included a `context` package in its standard library
- by using the `context.Context` interface in the `context` package and passing it from function to function, programs can convey that information from the beginning function of a program, such as `main`, all the way to the deepest function call in the program

# **Using Data Within a Context**
- we can access data stored inside a `context.Context`
- by adding data to a context and passing the context from function to function, each layer of a program can add additional information about what's happening
- eg: the 1st function may add a username to the context, the 2nd function may add the file path to the content the user is trying to access, then the 3rd function could read the file from the system's disk and log whether it was loaded successfuly or not as well as which user tried to load it
- we can add a new value to a context using the `context.WithValue` function, and we can access the those values using `context.Context.Value()` method
- values stored in `context.Context` are immutable, meaning they can't be changed, when we called the `context.WithValue`, we passed in the parent context and we also received a context back; we received a context back because the `context.WithValue` function didn't modify the context we provided, instead it wrapped our parent context inside another one with the new value
```golang
func doSomething(ctx context.Context) {
	fmt.Printf("doSomething: myKey's value is %s\n", ctx.Value("myKey"))
}

func main() {
	ctx := context.Background()
	ctx = context.WithValue(ctx, "myKey", "myValue")
	doSomething(ctx)
}
// output:
// doSomething: myKey's value is myValue
```

# **Ending a conext**
- another powerful tool `context.Context` provides is a way to signal to any functions using it that the context has ended and should be considered complete; by signaling to these functions that the context is done, they know to stop processing any work related to the context that they may stil be working on
- using this feature of a context allows our program to be more efficient because instead of fully completing every function, even if the result will be thrown out, that processing can be used for something else
- no matter the cause of a context ending, determining if a context is done happens the same way; the `context.Context.Done()` can be called to check and see whether a context has ended or not
- `context.Context.Done()` returns a channel that is **closed** when the context is done, and any functions watching for it to be closed will know they should consider their execution context completed and should stop any processing related to the context
- `context.Context.Done()` method works because no values are ever written to its channel, and when a channel is closed that channel will start to return `nil` values for every read attempt
- by periodically checking whether the `Done()` channel has closed and doing processing work in-between, we are able to implement a function that can do work but also knows if it should stop processing early; combining the processing work, the periodic check of the `Done()` channel, and the `select` statement goes even further by allowing us to send data or receive data from other channels simultaneously
```golang
ctx := context.Background()
resultsCh := make(chan *WorkResult)
for {
	select {
	case <- ctx.Done():
		// The context is over (ended), stop processing results
		return
	case result := <- resultsCh:
		// Process the results received
	}
}
```
- in the code execution above, the for loop will continue forever until the ctx.Done channel is closed
because the only return statement is inside that case statement
- even though the `case <- ctx.Done()` doesn't assign values to any variables, it will still be triggered when `ctx.Done` is closed because the channel still has a value that can be read even if it's ignored
- if the `ctx.Done` channel isn't closed, the `select` statement will wait until it is, or if `resultsCh` has a value that can be read
- if the `select` statement had a `default` branch without any code in it, it would just cause the `select` statement to end right away and the `for` loop would start another iteration of the `select` statement, leads to a **BUSY LOOP** as the loop is busy running over and over again, consuming a lot of CPU resources

# **Canceling a Context**
- canceling a context is the most straightforward and controllable way to end a context
- we can cancel a contxt using the `context.Context.WithCancel()` function
- `context.Context.WithCancel()` receives a parent context as a parameter and returns a new context as well as a function that can be used to cancel the returned context
- calling the cancel function returned will only cancel the context returned and any context that use it as a parent context
```golang
func doSomething(ctx context.Context) {
	ctx, cancelCtx := context.WithCancel(ctx)
	printCh := make(chan int)
	go doAnother(ctx, printCh)
	for num := 1; num <= 3; num++ {
		printCh <- num
	}
	cancelCtx()
	time.Sleep(100 * time.Millisecond)
	fmt.Printf("doSomething: finished\n")
}

func doAnother(ctx context.Context, printCh <-chan int) {
	for {
		select {
		case <-ctx.Done():
			if err := ctx.Err(); err != nil {
				fmt.Printf("doAnother err: %s\n", err)
			}
			fmt.Printf("doAnother: finished\n")
			return
		case num := <-printCh:
			fmt.Printf("doAnother: %d\n", num)
		}
	}
}

// Output
// doAnother: 1
// doAnother: 2
// doAnother: 3
// doAnother err: context canceled
// doAnother: finished
// doSomething: finished
```

# **Giving context a Deadline**
- using `context.WithDeadline` with a context allows us to set a deadline for when the context needs to be finsihed, and it will automatically end when the deadline passes
- we tell the context the time it needs to be finished, and Go automatically cancels the context for us if that time is exceeded
- to use the `context.Context.WithDeadline()` function, provide the parent context and a `time.Time` value for when the context should be canceled, we'll then received a new context and a function to cancel the new context as return values
- the context can also be canceled manually by calling the cancel function the same as we would for `context.Context.WithCancel()`
```golang
func doSomething(ctx context.Context) {
    deadline := time.Now().Add(1500 * time.Millisecond)
    ctx, cancelCtx := context.WithDeadline(ctx, deadline)
    defer cancelCtx()
}
```

# **Giving a Context a Time Limit**
- `context.Context.WithTimeout()` function can almost be considered more of a helpful function around `context.Context.WithDeadline()`
- with `context.Context.WithDeadline()` we provide a specific `time.Time` for the context to end, but by using `context.Context.WithTimeout()` function we only need to provide a `time.Duration` value for how long we want the context to last
```golang
func doSomething(ctx context.Context) {
	ctx, cancelCtx := context.WithTimeout(ctx, 1500*time.Millisecond)
	defer cancelCtx()
	...
}
```