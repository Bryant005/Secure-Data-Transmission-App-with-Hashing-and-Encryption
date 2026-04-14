# Secure-Data-Transmission-App-with-Hashing-and-Encryption
1. Upholding the CIA Triad (Outcome 1.1)
This application addresses the three core pillars of information security, known as the CIA Triad, through the following methods:

Confidentiality: This principle ensures that sensitive information is only accessible to authorized individuals. In the script, this is upheld in two ways. First, Role-Based Access Control (RBAC) ensures only users with the admin role can access the transmission feature. Second, the data payload is encrypted using symmetric encryption (AES via Fernet), ensuring that even if the data is intercepted during transmission, an attacker cannot read the plaintext without the secret key.

Integrity: This principle guarantees that data remains accurate and unaltered during storage or transmission. The application upholds integrity by utilizing the SHA-256 hashing algorithm. A hash is generated before encryption and again after decryption. If a single bit of the message were altered by a malicious actor or network error, the resulting hash would change drastically (the avalanche effect), alerting the system to the tampering.

Availability: This principle ensures that systems and data are available to authorized users when needed. By implementing structured authentication and clear error handling, the application ensures that legitimate users (like alice) can reliably access the system's functions without the system crashing due to unauthorized inputs or missing keys.

2. The Role of Entropy and Key Generation (Outcome 3.1)
In cryptography, entropy refers to the measure of randomness or unpredictability in a system. High entropy is essential for the strength of cryptographic algorithms because it prevents attackers from guessing keys through brute force or pattern recognition.

In this implementation, the generate_aes_key() function relies on the cryptography library, which utilizes the operating system's cryptographically secure pseudorandom number generator (CSPRNG) to create an AES key. Because the entropy of this generated key is incredibly high, an attacker cannot predict the sequence of bits that make up the key.

If we used low entropy (like a human-created password without proper key stretching, or a simple substitution cipher like the one demonstrated in Outcome 4.1), the encryption would be easily broken through frequency analysis or dictionary attacks. High-entropy key generation ensures that the symmetric encryption remains mathematically secure.

3. Digital Signatures (Outcome 4.3)
The application includes a demonstration of digital signatures using Asymmetric (Public Key) Cryptography. In this process:

The sender generates a mathematical key pair: a Private Key (kept secret) and a Public Key (shared openly).

The sender creates a hash of the message and encrypts that hash using their Private Key. This encrypted hash is the Digital Signature.

The receiver decrypts the signature using the sender's Public Key to reveal the original hash, and then compares it to their own hash of the message.

If they match, it proves two things: the message was not altered (Integrity), and it definitively came from the sender who holds the private key (Non-repudiation).
