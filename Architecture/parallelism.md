# **CPU-intensive & I/O-intensive**
- CPU-intensive => CPU needs to actively compute and process (machine learning)
- I/O-intensive => reading files from file system, making network request

# **Concurrency & Parallelism**
- **Concurrent** means an application is making progress on more than one task at the same time, if the computer has only one CPU then it may not make progress on more than one task exactly at the same time, but more than one task is being processed at a time inside the application, it does not completely finish one task before it begins the next task
- **Concurrent** means executing multiple tasks at the same time but not necessarily simultaneously
- **Parallelism** means an app splits its task up into smaller subtask which can be processed at the same time (parallel), with multi-core infrastructure, usually by assigning one core to each task or sub-task (require hardware with multiple processing units, impossible to achieve with single-core)
- A system is said to be concurrent if it can support two or more actions in progress at the same time.  A system is said to be parallel if it can support two or more actions executing simultaneously
- Concurrency is about dealing with lots of things at once. Parallelism is about doing lots of things at once
- Threads are lighter than process, and they share the same memory space
- PARALLELISM IS A SUBSET OF CONCURRENCY

# **Web Crawling**
- I/O is the bottleneck here, the act of going to the net to retrieve a page (I/O) is slower than analysing the page (CPU)
- So making the CPU bit 10 times faster will have little effect on the overall time taken, whereas doubling the I/O speed will have a very beneficial effect, right to the point where the CPU starts being the bottleneck

# **Python**
### **Global Interpreter Lock (GIL)**
- Python GIL allow us to run multiple threads, but at any point of time only one thread will be working
- In case of python, multithreading will not have impact on cpu intensive jobs
- The GIL is an interpreter-level lock. This lock prevents execution of multiple threads at once in the Python interpreter. Each thread that wants to run must wait for the GIL to be released by the other thread
- GIL is the thing that limit the work that the threads do at the Python layer, only one thread is allowed to modify the state of the Python interpreter at a time, any additional threads trying to do so will sit idle until it’s their turn to operate
### **Python Multiprocessing**
- Only **multi-processing** will allow Python code to be truly parallel, but it comes with a cost, the entire memory of the script is copied into each subprocess that is spawned, causing memory overhead
- This could be a serious issue when we want to run some long-running back-end applications, as it could spin up a bunch of sub-processes or threads on the same machine that needs to run for a long time, which will definitely degrade the performance
- If code is **I/O bound**, multiprocessing and multithreading will work; if code is **CPU bound**, multiprocessing is better than multithreading, cause more time is needed for context switching
- Main process spawn => new threads, main process has the knowledge about every thread that was created, and by using **“join”** it can wait for these threads to finish processing
- The threading module uses threads, the multiprocessing module uses processes. The difference is that threads run in the same memory space, while processes have separate memory. This makes it a bit harder to share objects between processes with multiprocessing. Since threads use the same memory, precautions have to be taken or two threads will write to the same memory at the same time. This is what the global interpreter lock is for
- SPAWNING PROCESSES IS SLOWER THAN SPAWNING THREADS
![alt text](https://devopedia.org/images/article/280/6110.1593611188.png)

# **Tips from StackOverflow**
The rule of thumb when deciding whether to use threads in Python or not is to ask the question, whether the task that the threads will be doing, is that CPU intensive or I/O intensive. If the answer is I/O intensive, then you can go with threads.
Because of the GIL, the Python interpreter will run only one thread at a time. If a thread is doing some I/O, it will block waiting for the data to become available (from the network connection or the disk, for example), and in the meanwhile the interpreter will context switch to another thread. On the other hand, if the thread is doing a CPU intensive task, the other threads will have to wait till the interpreter decides to run them.
Web crawling is mostly an I/O oriented task, you need to make an HTTP connection, send a request, wait for response. Yes, after you get the response you need to spend some CPU to parse it, but besides that it is mostly I/O work. So, I believe, threads are a suitable choice in this case.