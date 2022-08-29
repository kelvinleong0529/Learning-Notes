# **Proxy Auto-Configuration**
- `proxy auto-configuration (PAC)` files is a JavaScript function definition that determines whether web requests (HTTP, HTTPS, and FTP) go direct to the destination or are forwarded to a web proxy server
- `PAC` files are used to support explicit proxy deployments in which client browser are explicitly configured to send traffic to the web proxy
- advantage of `PAC` files are that they are usually relatively easu to create and maintain
- the use of a PAC file is highly recommended with explicit proxy deployments of Websense Web Security Gateway (for the Content Gateway -- web proxy -- component) and is required to support the hybrid web filtering feature of Web Security Gateway Anywhere
- **PAC files is**:
1. Flexible and extensible
2. Supported by all popular browsers
3. Easy to administer and maintain in any size network; however, as this paper explains, PAC files are easiest to administer when the browser is Internet Explorer
4. Able to support mobile devices that use standard browsers
- A PAC file can:
1. Be stored on any server in your network. Small networks may store the file on the proxy itself, but large, enterprise-class networks should use a separate server for storing the PAC file
2. Determine where Internet and intranet requests are routed
3. Allow for exceptions in the form of bypassing the proxy for specified destinations
4. Perform load distribution
5. Handle proxy failover

# **Why use PAC File?**
1. The PAC file provides critical security, ensuring that traffic is always proxied when it should be, while allowing secure requests to go direct to the destination.
- Typically, Internet-bound HTTP, HTTPS, and FTP traffic is sent to the proxy.
- Typically, intranet traffic goes direct to the destination.
- Exceptions can be made for internal or external sites that, for whatever reason, must go to or bypass the proxy.
2. The PAC file locks down the web browser's LAN egress configuration. The PAC file should be appropriately permission-protected so that end-users cannot change it. This is most easily accomplished when the PAC file is administered with a Group Policy Object. See How do I configure a Group Policy so that Internet Explorer uses the PAC file?
3. The PAC file provides a flexible, easy to maintain, script-driven method of controlling the routing of web requests.
4. The PAC file can include code that handles proxy load distribution and failover.