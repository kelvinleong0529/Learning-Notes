## Serialization**
- `serialization` is a mechanism of converting the state of an object into a byte stream
- `deserialization` is the reverse process where the byte stream is used to recreate the actual Java object in memory
- this mechanism is used to persist the object, as the byte stream created is platform independent, meaning the object serialized on one platform can be deserialized on a different platform
- to make a Java object serializable, we implement the `java.io.Serializable` interface

## **Transient**
- `transient` is a variable modifier used in serialization
- at time of serialization, if we don't want to save value of a particular variable in a file, we can use the `transient` keyword; when JVM comes across the `transient` keyword it ignores original value of the variable and save default value of that variable data type
- `transient` is useful when we don't want to save private data in file, or when we want to not serialize a variable whose value can be calculated / derived using other serialized objects or system such as age of a person, current date, etc
- practically we only serialize those fields which represent a state of instance
- `transient` has no effect on `static` and `final` variables