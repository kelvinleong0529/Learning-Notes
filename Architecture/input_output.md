# **I/O Models**
- `polling` means checking the status of some resource at a regular interval
- suppose we are in a car, stuck on a red light:
1. We can stare at the traffic light, do nothing and wait until it turns green, this is a `busy wait`
2. if we are playing phone and check on the traffic light every 10 seconds, we are `polling` with a frequency of 10 seconds
3. if we are playing phone until the car behind honks us, we are using `interrupts`
- `I/O multiplexing` is the capability to tell the kernel that we want to notified if one or more I/O conditions are ready, eg: input ready to be read, or descriptor is capable of taking more output
- `I/O multiplexing` is used for the following scenarios:
1. when client is handling multiple descriptors (eg: standard input, network socket)
2. when client handles multiple sockets at the same time, eg: web client
3. when TCP server handles both listening and its connected sockets
4. when server handles both TCP and UDP
5. when server handles multiple services and perhaps multiple protocols
