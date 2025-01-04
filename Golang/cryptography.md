# **RSA**

[PEM](../Encryption/privacy_enhanced_mail)
- we will try to use `Go` built-in library to encrypt and decrypt PEM files
```golang
// use crypto/rsa lib to generate a private key
privateKey, err := rsa.GenerateKey(rand.Reader, 2048)
// rand.Reader is a secure random number generator

// obtain the public key from private key
publicKey := &privateKey.PublicKey

// ---------------------------------------------------------------------
// export these RSA key pair created into a PEM file
// ---------------------------------------------------------------------
pemPrivateFile, err := os.Create("private_key.pem")
// encode our private key with x509 package
var pemPrivateBlock = &pem.Block{
    Type: "RSA PRIVATE KEY",
    Bytes: x509.MarshalPKCS1PrivateKey(privateKey),
}
// write this block inside the file with the correct PEM format and close the file
err = pem.Encode(pemPrivateFile, pemPrivateBlock)

// ---------------------------------------------------------------------
// Import RSA keys from PEM files
// ---------------------------------------------------------------------
privateKeyFile, err := os.Open("private_key.pem")
// read the content of the file using "buffer" from bufio package
pemfileinfo, _ := privateKeyFile.Stat()
// Stat() returns the FileInfo structure describing file, if there is an error, it willbe of type *PathError
var size int64 = pemfileinfo.Size()
pembytes := make([]byte, size)
buffer := bufio.NewReader(privateKeyFile)
_, err = buffer.Read(pembytes)
data, _ := pem.Decode([]byte(pembytes))
privateKeyFile.Close()

privateKeyImported, err := x509.ParsePKCS1PrivateKey(data.Bytes)
if err != nil {
    fmt.Println(err)
    os.Exit(1)
}
fmt.Println("Private Key : ", privateKeyImported)
```
