# **Symmteric Encryption / Private Key Encryption**
- a type of encryption that uses the same key to encrypt and decrypt data
- both sender and receiver hand identical copies of the key, which is kept secretly without sharing to the others
1. sender use an encryption key (usually a string of letters and numbers) to encrypt their data
2. recipient use a decryption key (same as encryption key) to transform the ciphertext back into readable text
- issue arised when the private key is stolen or leaked, hence key management requires prevention of these risks and necessitates changing the encryption key often, and appropriately distributing the key
![Symmetric Encryption](https://www.thesslstore.com/blog/wp-content/uploads/2020/11/how-encryption-works-symmetric-encryption.png)
- For more details, [read here](https://www.thesslstore.com/blog/symmetric-encryption-101-definition-how-it-works-when-its-used/)

# **Public Key Cryptography**
- also called `RSA encryption`
- involves a pair of keys known as `public key` and `private key`, which are associated with an entity that needs to authenticate its identity electronically or to sign or encrypt data
- each `public key` is published and the corresponding `private key` is kept secret
- data is encrypted with `public key` and can be decrypted with the corresponding `private key`
- enables the following:
1. encryption and decryption, which allow 2 communicating parties to disguise their data send to each other. Sender encrypts, or scramble the data before sending it; receiver decrypts or unscramble the data after receiving it. While in transit, the encrypted data is not understood by any intruder
2. non-repudiation, which prevents the sender of the data from claiming, at a later date that the data was never sent; and also the data from being altered

![Public Key Cryptography](https://www.ibm.com/docs/en/SSB23S_1.1.0.14/gtps7/ssldig02.gif)
- to send encrypted data to someone, we must encrypt the data with the recevier's public key (usually is published and anyone can access), and the receiver should decrypt it with the corresponding private key
- compared to `symmetric-key encryption`, `public-key encryption` requires more calculation, there is not always suitable for larage amount of datas

# **Digital Signature Algorithm**
- similar to [RSA encryption](#public-key-cryptography)
1. original message is first passed to a hash function dentoed by `H#` to create a digest
2. next, it bundles the message together with the hash digest `h` and encrypts it using the sender's private key
3. it sends the encrypted bundle to the receiver, who can decrypt it using the sender’s public key.
4. Once it decrypts the message, it is passed through the same hash function (H#), to generate a similar digest.
5. It compares the newly generated hash with the bundled hash value received along with the message. If they match, it verifies data integrity.
![DSA algorithm](https://www.simplilearn.com/ice9/free_resources_article_thumb/ds_process-DSA_Algorithm.PNG)
## **Benefits:**
1. `Message Authentication`: You can verify the origin of the sender using the right key combination.
2. `Integrity Verification`: You cannot tamper with the message since it will prevent the bundle from being decrypted altogether.
3. `Non-repudiation`: The sender cannot claim they never sent the message if verifies the signature




# **Difference between DSA & RSA**

|             | RSA                                                                                                                                  | DSA                                                                                                                                                |
|-------------|--------------------------------------------------------------------------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------|
| Differences | more on private conversation, 1-to-1 or many-to-1 interaction, since only the person who has the private key can decrypt the message | more on broadcasting, since anyone with public key (usually published widely) can decrypt the message |