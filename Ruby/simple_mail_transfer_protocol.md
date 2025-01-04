# **Simple Mail Transfer Protocol**
- Simple Mail Transfer Protocol (SMTP) is a protocol, which handles sending e-mail and routing e-mail between mail servers
- Ruby provides Net::SMTP class for Simple Mail Transfer Protocol (SMTP) client-side connection and provides two class methods new and start
1. The new takes two parameters:
- The server name defaulting to localhost.
- The port number defaulting to the well-known port 25.
2. The start method takes these parameters:
- The server − IP name of the SMTP server, defaulting to localhost.
- The port − Port number, defaulting to 25.
- The domain − Domain of the mail sender, defaulting to ENV["HOSTNAME"].
- The account − Username, default is nil.
- The password − User password, defaulting to nil.
- The authtype − Authorization type, defaulting to cram_md5