## Serialization**
- `serialization` is a mechanism of converting the state of an object into a byte stream
- `deserialization` is the reverse process where the byte stream is used to recreate the actual Java object in memory
- this mechanism is used to persist the object, as the byte stream created is platform independent, meaning the object serialized on one platform can be deserialized on a different platform
- to make a Java object serializable, we implement the `java.io.Serializable` interface