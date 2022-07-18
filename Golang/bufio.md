# **Bufio**
- Go `bufio` implements buffered IO operations
- Buffering is a technique which improves the performance of IO operations
- Since system calls are costly, the performance of IO operations is greatly improved when we accumulate data into a buffer when reading or writing it, which reduces the number of system calls needed
```go
type Reader
type Writer
type Scanner
```
## **1. Reader**
```go
func NewReader (rd io.Reader) *Reader
// returns a New Reader whose buffer has the default size
func NewReaderSize (rd io.Reader, size int) *Reader
// returns a new Reader whose buffer has at least the specified size
-----------------------------------------------------------------------

func main() {
    reader := bufio.NewReader(os.Stdin)
    // create a new reader from the standard input

    name, err := reader.ReadString("\n")
    // reads until the first occurence of the given delimeter in the input

    if err != nil {
        log.Fatal(err)
    }

    fmt.Printf("Hello %s!\n",strings.TrimSpace(name))
}
```
## **2. Writer**
```go
func main() {

    // this function write a few strings into a file with Writer.WriteString

    data := []string{"an old falcon", "misty mountains",
        "a wise man", "a rainy morning"}

    f, err := os.Create("words.txt")
    if err != nil {
        log.Fatal(err)
    }

    defer f.Close()
    wr := bufio.NewWriter(f)
    // create a new writer with a default size of 4KB

    for _, line := range data {
        wr.WriteString(line + "\n")
    }

    wr.Flush()
    // bufio.Writer only sends data when buffer is either full or when explicitly requested with Flush method
    // since our data is smaller than the default 4KB buffer size, we have to call Flush for the data to be actually written to the file

    fmt.Println("data written")
}
```
## **3. Scanner**
```txt
// words.txt file

sky
nice
cup
```
```go
func main() {

    // this function reads a small file containing words on each line

    f, err := os.Open("words.txt")
    if err != nil {
        log.Fatal(err)
    }

    defer f.Close()
    scanner := bufio.NewScanner(f)

    for scanner.Scan() {
        fmt.Println(scanner.Text())
    }
    // Scan function advances the Scanner to the next token, which will then be available through the Bytes or Text method
    // By default, Scan function advances by lines

    if err := scanner.Err(); err != nil {
        log.Fatal(err)
    }
}
```

- `fmt.Fprintf` writes to the io.Writer passed to it
- `fmt.Printf` writes to the standard output