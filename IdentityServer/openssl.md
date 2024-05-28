#### [Back](./README.md)

# Open SSL

1. ## Basic Component of OPEN SSL
* **SSL/TLS Protocol:** These are cryptographic protocols designed to provide secure communication over a computer network. SSL is the predecessor of TLS.
* **Cryptographic Algorithms:** OpenSSL includes implementations of many cryptographic algorithms such as RSA, DSA, AES, SHA, etc.     
* **Tools and Utilities:** OpenSSL comes with command-line tools for managing and using cryptographic keys and certificates.

2. ## Key Functions and Features
    * a. **Encryption and Decryption**
        * **Symmetric Encryption:** Uses the same key for both encryption and decryption (e.g., AES).
        * **Asymmetric Encryption:** Uses a pair of keys – a public key for encryption and a private key for decryption (e.g., RSA).
    * b. **Digital Certificates and PKI** 
        * **Certificates:** OpenSSL can generate and manage X.509 certificates, which are used in SSL/TLS to verify the identity of entities.
        * **Certificate Authorities (CAs):** OpenSSL can be used to act as a CA, issuing and signing certificates.
    * c. **Hash Functions**
        * Provides implementations of hash functions like SHA-1, SHA-256, MD5, etc., used for ensuring data integrity.
    * d. **Digital Signatures**
        * Enables creation and verification of digital signatures, ensuring data authenticity and integrity.

3. ## Common Use Cases
    * a. **Generating Keys and Certificates**
        * **Generate a Private Key:**
        ```bash
        openssl genpkey -algorithm RSA -out private_key.pem
        ```
        * **Generate a Certificate Signing Request (CSR):**
        ```bash
        openssl req -new -key private_key.pem -out csr.pem
        ```
        * **Self-Signed Certificate:**
        ```bash
        openssl req -x509 -key private_key.pem -in csr.pem -out cert.pem -days 365
        ```
        * **Create Private RSA** Create a private RSA keys that are between 1024 and 4096 bits long. You have a private key in PEM format.
        ```bash
        openssl genrsa -out jwtRSA256-private.pem 2048
        ```
        * **Extract Public Key from Private Key** 
        ```bash
        openssl rsa -in jwtRSA256-private.pem -pubout -outform PEM -out jwtRSA256-public.pem
        ```
        
    * b. **Encrypting and Decrypting Data**
        * **Encrypt a File:**
            ```bash
            openssl enc -aes-256-cbc -salt -in file.txt -out file.enc
            ```
        * **Decrypt a File:**
            ```bash
            openssl enc -aes-256-cbc -d -in file.enc -out file.txt
            ```
    * c. **Creating Digital Signatures**
        * **Sign a File:**
        ```bash
        openssl dgst -sha256 -sign private_key.pem -out signature.bin file.txt
        ```

        * **Verify a Signature:**
        ```bash
        openssl dgst -sha256 -verify public_key.pem -signature signature.bin file.txt
        ```


