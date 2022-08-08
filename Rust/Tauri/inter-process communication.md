# **Isolation Pattern**
- `isolation pattern` is a way to intercept and modify **Tauri APP** messages sent by frontend before they get to **Tauri Core**, all with JavaScript. The secure JavaScript code that is injected by the `isolation pattern` is reffered to as the `isolation application`
- `isolation pattern`'s purpose is to provide a mechanism for developers to help protect their application from unwanted or malicious frontend calls to **Tauri core**
- we can utilize the secure `isolation application` to try and verify IPC inputs, to make sure they are within some expected parameters
- example: we may want to check that a call to read or write a file is not trying to access a apth outside our application's expected locations; making sure a Tauri APP HTTP fetch call is only setting the Origin header to what our application expects it to be

# **How**
- `isolation pattern` is about injecting a secure application in between our frontend and **Tauri Core** to intercept and modify any incoming IPC messages
- this is achieved by using the sandboxing feature of `<iframe>` to run the JavaScript securely alongside the main frontend application
- Tauri enforces the Isolation pattern while loading the page, forcing all IPC calls to Tauri Core to instead be routed through the sandboxed Isolation application first
- Once the message is ready to be passed to Tauri Core, it is encrypted using the browser's SubtleCrypto implementation and passed back to the main frontend application
- Once there, it is directly passed to Tauri Core, where it is then decrypted and read like normal.
- To ensure that someone cannot manually read the keys for a specific version of your application and use that to modify the messages after being encrypted, new keys are generated each time your application is run.