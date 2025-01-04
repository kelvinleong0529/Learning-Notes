# **Network**
- Go's `net` package provides a protable interface for network I/O, including TCP/IP, UDP, domain name resolution and Unix domain sockets
- `net.Dial()` and `net.Listen()` return data types that implements the io.Reader and io.Writer interfaces, meaning we can use regular `File I/O` functions to send and receive data from a TCP/IP connection
- 
## **TCP Client**
```golang
func main() {
    arguments := os.Args 
    // the first value / argument is the path to the program
    if len(arguments) == 1 {
        fmt.Println("Please provide host:port.")
        return
    }

    CONNECT := arguments[1]
    c, err := net.Dial("tcp", CONNECT)
    if err != nil {
        fmt.Println(err)
        return
    }

    for {
        reader := bufio.NewReader(os.Stdin)
        fmt.Print(">> ")
        text, _ := reader.ReadString('\n')
        fmt.Fprintf(c, text+"\n")
        // writes to the 'c' (io.Writer) passed to it
        // send user input server over the network

        message, _ := bufio.NewReader(c).ReadString('\n')
        // reads input from 'c' (server response)
        fmt.Print("->: " + message)
        if strings.TrimSpace(string(text)) == "STOP" {
            fmt.Println("TCP client exiting...")
            return
        }
    }
}
```
## **TCP Sever**
```golang
func main() {
    arguments := os.Args
    if len(arguments) == 1 {
        fmt.Println("Please provide port number")
        return
    }

    PORT := ":" + arguments[1]
    l, err := net.Listen("tcp", PORT)
    if err != nil {
        fmt.Println(err)
        return
    }
    defer l.Close()

    c, err := l.Accept()
    if err != nil {
        fmt.Println(err)
        return
    }

    for {
        netData, err := bufio.NewReader(c).ReadString('\n')
        if err != nil {
            fmt.Println(err)
            return
        }
        if strings.TrimSpace(string(netData)) == "STOP" {
            fmt.Println("Exiting TCP server!")
            return
        }

        fmt.Print("-> ", string(netData))
        t := time.Now()
        myTime := t.Format(time.RFC3339) + "\n"
        c.Write([]byte(myTime))
    }
}
```
## **Concurrent TCP Server**
```golang
var count = 0

func handleConnection(c net.Conn) {
    fmt.Print(".")
    for {
        netData, err := bufio.NewReader(c).ReadString('\n')
        if err != nil {
                fmt.Println(err)
                return
        }

        temp := strings.TrimSpace(string(netData))
        if temp == "STOP" {
                break
        }
        fmt.Println(temp)
        counter := strconv.Itoa(count) + "\n"
        // strconv.Itoa(x) returns the string representation of x when the base is 10
        c.Write([]byte(string(counter)))
    }
    c.Close()
}

func main() {
    arguments := os.Args
    if len(arguments) == 1 {
        fmt.Println("Please provide a port number!")
        return
    }

    PORT := ":" + arguments[1]
    l, err := net.Listen("tcp4", PORT)
    if err != nil {
        fmt.Println(err)
        return
    }
    defer l.Close()

    for {
        c, err := l.Accept()
        if err != nil {
                fmt.Println(err)
                return
        }
        go handleConnection(c)
        count++
    }
}
```