# **PEM Files**
- `Privacy Enchanced Mail (PEM)` is a standard, they contain text (in the format below), everything in between is base64 encoded, and this forms a block of data that can be used in other programs. A single PEM file can contain multiple blocks
- a container file format often used to store crytographic keys, it simply defines the structure and encoding type of the file used to store a bit of data
- PEM files can be used to represent all kinds of data, but its commonly used to encode keyfiles, such as `RSA keys` used for `SSH`, and certificates used for `SSQL encryption`. Usually a PEM file will tell us what it's used for in the header
```
PEM file usually start with...
-----BEGIN <type>-----

and end with:
-----END <type>-----
```

# **PEM Files with SSL Certificates**
- PEM files are used to store SSL certificates and their associated private keys. Multiple certificates are in the full SSL chain, and they work in this order:
1. The end-user certificate, which is assigned to your domain name by a certificate authority (CA). This is the file you use in nginx and Apache to encrypt HTTPS.
2. Up to four optional intermediate certificates, given to smaller certificate authorities by higher authorities.
3. The root certificate, the highest certificate on the chain, which is self-signed by the primary CA.
```
-----BEGIN CERTIFICATE-----
  //end-user
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
  //intermediate
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
  //root
-----END CERTIFICATE-----
```

# **PEM Files with SSH**
- PEM files are also used for SSH. If you’ve ever run ssh-keygen to use ssh without a password, your ~/.ssh/id_rsa is a PEM file, just without the extension.
- Most notably, Amazon Web Services gives you a PEM file containing a private key whenever you create a new instance, and you must use this key to be able to SSH into new EC2 instances.