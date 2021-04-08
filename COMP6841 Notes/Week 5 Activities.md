# Community

## Recharge

To avoid burnouts, I play musical instruments to destress myself between coding or study sessions, especially when I'm stuck on a problem. I find this very effective in taking my mind off things and allowing me to regain focus for many long hours of work at a time. 



# Security Engineering

## Password hash cracking

- Avalanche effect - small changes in the input lead to large changes in the hash output
- Deterministic - hashing the same input always produces the same hash output
- Preimage resistance - given a hash output, it should be hard to find an input which would produce it
- Second preimage resistance - given a hash input, it should be hard to find a different input that has the same hash
- Collision resistance - it should be hard to find two different inputs which produce the same hash output

- Dictionary attack - form of brute force attack by trying dictionary words as likely possibilities
- Rainbow/lookup tables - lookup table for hashed outputs mapped to inputs
- Birthday attack - specialised form of brute force assault used to find collisions in a cryptographic hash function. The attacks exploit the underlying probability theory and mathematics of the Birthday Paradox situation to help reduce the number of data samples and iterations on a target required to find matching pairs. (1st vs 3rd person)
  - Repeated attempts to locate two inputs that hash to the same value, rather than trying to find something that collides with a specific hash value
  - Defence
    - Large output length of the hash function - typically about twice as many bits compared to countering an ordinary brute force attack
    - Altering original copy to be passed as input without changing the overall form of the message, keeping personal record of these alterations
  - [Birthday Paradox | When Mathematical Theory is Used in Cyber Attacks (finjan.com)](https://blog.finjan.com/birthday-paradox-when-mathematical-theory-is-used-in-cyber-attacks/)
- Chosen-plaintext attack - trying to learn more about encryption system by analysing generated ciphertext for plaintext data to be encrypted

Crack an MD5 password hash using crackstation.net

Securing Stream Ciphers using HMAC

- Message authentication code (MAC)
- Stream ciphers usually used for video stream encryption - XOR for a pseudo-random key stream (flip bits)
- Message can be intercepted and bits flipped for interference - banks etc. follow a pattern
- Add checksum to end of message m: h(k|m) hash of a key k appended to message - although hash functions used based on Merkle-Damgard construction, whose internal states can be resumed and append to the message (append to message and calculate a new hash)
- HMAC (key hashed authentication code) - two hashes involved for two keys k1 and k2
  - h(k2|h(k1|m))
  - Immune to length extension attacks - don't know internal state for inner hash

Length extension attacks

- If you have a message that is concatenated with a secret and the resulting hash of the concatenated value (the MAC) – and you know only the length of that secret – you can add your own data to the message and calculate a value that will pass the MAC check without knowing the secret itself.
- Registers updated with hashes of message + padding, broken into 512 bit blocks - returned as hash
- key + message + padding + extension
- Extension must be in its own block so key + message + padding must be a multiple of 512 bits
- [Hash Length Extension Attacks | WhiteHat Security](https://www.whitehatsec.com/blog/hash-length-extension-attacks/)
- https://youtu.be/3R_q5XD-RJU

Database dump



# Extension

YmFzZTY0X2lzX25vdF9lbmNyeXB0aW9u





