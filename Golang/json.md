# **JSON**
- `json.Decode` buffers the entire JSON value in memory before unmarshalling it into a Go value. So in most case it wont be any more memory efficient
- Use `json.Decoder` if our data is coming from an `io.Reader` stream, or if we need to decode multiple values from a stream of data
- Use `json.Unmarhsal` if we already have the JSON data in memory