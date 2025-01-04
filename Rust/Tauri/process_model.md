# **Multiple Processes**
- `Tauri` employs a **multi-process architecture** similar to [Electron](https://www.electronjs.org/) or many modern web browsers
- during the early days of GUI apps, it was common to use a single process to perform computation, draw the interface and react to user input. A long-running, expensive computation would leave the user interface unresponsive, or worse, a failure in one app component would bring the whole app crashing down
- a more resilient architecture was needed, and applications began running different components in different processes, which makes much better use of modern multi-core CPUs and creates far safer applications
- a crash in one component doesn't affect the whole system anymore, as components are isolated on different processes. If a process gets into an invalid state, we can easily restart it
- We can also limit the blast radius of potential exploits by handing out only the minimum amount of permissions to each process, just enough so they can get their job done. For eg: If we have a gardener coming over to trim your hedge, we give them the key to your garden. we would not give them the keys to our house; why would they need access to that? The same concept applies to computer programs. The less access we give them, the less harm they can do if they get compromised

# **Core Process**
- Each Tauri application has a `core process`, which acts as the application's entry point and which is the only component with full access to the operating system
- `Core`'s primary responsibility is to use that access to create and orchestrate application windows, system-tray menus, or notifications.
- Tauri implements the necessary cross-platform abstractions to make this easy
- it also routes all Inter-Process Communication through the Core process, allowing you to intercept, filter, and manipulate IPC messages in one central place
- `core process` should also be responsible for managing global state, such as settings or database connections. This allows you to easily synchronize state between windows and protect your business-sensitive data from prying eyes in the Frontend

# **Webview Process**
- `Core process` doesn't render the actual UI itself; it spins up WebView processes that leverage WebView libraries provided by the operating system. A WebView is a browser-like environment that executes your HTML, CSS, and JavaScript
- this means that most of our techniques and tools used in traditional web development can be used to create `Tauri` applications
- Security best practices apply as well; for example, you must always sanitize user input, never handle secrets in the Frontend, and ideally defer as much business logic as possible to the Core process to keep your attack surface small.