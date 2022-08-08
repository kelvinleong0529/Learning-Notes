# **Cryptographic Checksum**
- `cryptographic checksum` is a mathematical value assigned to a file sent through a network for verifying that the data contained in that file is unchanged
- the cryptographic hash function takes an input value (for instance, a string) and produces a fixed-length sequence of numbers and letters
- the algorithm peforms numerous mathematical operations to create a `hash` value, or fixed string of digits

# **MD5**
- produces a `128-bit` hash value
- vulnerabilities was discovered over the course of time, so it is no longer recommended for cryptography, not resistant to **Hash Collisions**
- however, it is sill used for database partitioning and computing checksums to validate files transfer

# **SHA-1**
- SHA stands for `Secure Hash Algorithm`
- generates `160-bit` hash value
- it was found to have vulnerabilities also, it is no longer considered to be any less resistant to attack than `MD5`

# **SHA-2**
- returns hash values of `256-bits`
- while not quite perfect, research discovers that it is considerably more secure than either `MD5` or `SHA-1`