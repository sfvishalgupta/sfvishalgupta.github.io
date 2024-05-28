#### [Back](./README.md)

# Generating a JWT with RSA Keys

## RS256 Signature
RS256 is an RSA Digital Signature Algorithm with SHA-256. RSA256 is an Asymmetric Key Cryptography algorithm, which uses a pair of keys: a public key and a private key to encrypt and decrypt. In this case, the private key is used by the token issuer (authorization server), and the public key is used by the application receiving the token in order to validate it.

## Hashing
Hashing converts one value into a different value. A hash function uses a mathematical algorithm to generate a new value from an existing one.

* Hashing is irreversible. Once we have hashed an input, we cannot get back to the original input again.
* Hashing will always produce the same output for the same input.
* No two different hashing inputs will produce the same output.

## Encryption
Next we encrypt the hashed signing input. Unlike hashing, encryption is reversible: we can decrypt encrypted results (called ciphertext) to decipher the original input (plaintext).

To generate a JWT signed with the RS256 algorithm and RSA keys, you need to use openssl commands or the auth0 library.

A JWT consists of three parts separated by dots.
* Header
* Payload
* Signature

```bash
Y = Base64URLEncode(header) + '.' + Base64URLEncode(payload)
JWT token = Y + '.' + Base64URLEncode(RSASHA256(Y))
```

## Header
```json
{
    "alg": "RS256",
    "typ": "JWT"
}
```

To encode the header, you can use the following command:
```bash
echo -n '{"alg":"RS256","typ":"JWT"}' | base64 | sed s/\+/-/ | sed -E s/=+$//
```
Result is encoded header
```txt
eyJhbGciOiJFUzI1NiIsInR5cCI6IkpXVCJ9
```

## Payload
The second part of the token is the payload, which contains the claims. Claims are statements about an entity (typically, the user) and additional data. There are three types of claims: registered, public, and private claims.

* **Registered Claims** These are a set of predefined claims which are not mandatory but recommended, to provide a set of useful, interoperable claims.

1. **iss** (Issuer) Claim
2. **sub** (Subject) Claim
3. **aud** (Audience) Claim
4. **exp** (Expiration Time) Claim
5. **nbf** (Not Before) Claim
6. **iat** (Issued At) Claim
7. **jti** (JWT ID) Claim

* **Public Claims** These can be defined at will by those using JWTs. But to avoid collisions

* **Private Claims** These are the custom claims created to share information between parties that agree on using them and are neither registered or public claims.

```json
{
    "sub": "1234567890",
    "name": "John Doe",
    "admin": true
}
```
To encode the payload, use a command similar to this one:
```bash
echo -n '{"sub":"RS256inOTA","name":"John Doe"}' | base64 | sed s/\+/-/ | sed -E s/=+$//
```

The result is the encoded payload:
```text
eyJzdWIiOiJFUzI1NmluT1RBIiwibmFtZSI6IkpvaG4gRG9lIn0
```

## Signature
To create a signature with the an RSA private key, you can use a command similar to this one:
```bash
echo -n "eyJhbGciOiJFUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJFUzI1NmluT1RBIiwibmFtZSI6IkpvaG4gRG9lIn0" | openssl dgst -sha256 -binary -sign jwtRSA256-private.pem  | openssl enc -base64 | tr -d '\n=' | tr -- '+/' '-_'
```

The result is the encoded signature:
```text
ICV6gy7CDKPHMGJxV80nDZ7Vxe0ciqyzXD_Hr4mTDrdTyi6fNleYAyhEZq2J29HSI5bhWnJyOBzg2bssBUKMYlC2Sr8WFUas5MAKIr2Uh_tZHDsrCxggQuaHpF4aGCFZ1Qc0rrDXvKLuk1Kzrfw1bQbqH6xTmg2kWQuSGuTlbTbDhyhRfu1WDs-Ju9XnZV-FBRgHJDdTARq1b4kuONgBP430wJmJ6s9yl3POkHIdgV-Bwlo6aZluophoo5XWPEHQIpCCgDm3-kTN_uIZMOHs2KRdb6Px-VN19A5BYDXlUBFOo-GvkCBZCgmGGTlHF_cWlDnoA9XTWWcIYNyUI4PXNw
```

## A Complete JWT
```text
eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJSUzI1NmluT1RBIiwibmFtZSI6IkpvaG4gRG9lIn0.ICV6gy7CDKPHMGJxV80nDZ7Vxe0ciqyzXD_Hr4mTDrdTyi6fNleYAyhEZq2J29HSI5bhWnJyOBzg2bssBUKMYlC2Sr8WFUas5MAKIr2Uh_tZHDsrCxggQuaHpF4aGCFZ1Qc0rrDXvKLuk1Kzrfw1bQbqH6xTmg2kWQuSGuTlbTbDhyhRfu1WDs-Ju9XnZV-FBRgHJDdTARq1b4kuONgBP430wJmJ6s9yl3POkHIdgV-Bwlo6aZluophoo5XWPEHQIpCCgDm3-kTN_uIZMOHs2KRdb6Px-VN19A5BYDXlUBFOo-GvkCBZCgmGGTlHF_cWlDnoA9XTWWcIYNyUI4PXNw
```

## A Request with JWT Token
Having the JWT ready, you can make a request.
```bash
curl -ki -vvv https://demo1.ota-updates.com/example.zip \
     -H "X-Akamai-OTA-Uid: rs256" \
     -H "X-Akamai-JWT-Token:
eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiJSUzI1NmluT1RBIiwibmFtZSI6IkpvaG4gRG9lIn0.ICV6gy7CDKPHMGJxV80nDZ7Vxe0ciqyzXD_Hr4mTDrdTyi6fNleYAyhEZq2J29HSI5bhWnJyOBzg2bssBUKMYlC2Sr8WFUas5MAKIr2Uh_tZHDsrCxggQuaHpF4aGCFZ1Qc0rrDXvKLuk1Kzrfw1bQbqH6xTmg2kWQuSGuTlbTbDhyhRfu1WDs-Ju9XnZV-FBRgHJDdTARq1b4kuONgBP430wJmJ6s9yl3POkHIdgV-Bwlo6aZluophoo5XWPEHQIpCCgDm3-kTN_uIZMOHs2KRdb6Px-VN19A5BYDXlUBFOo-GvkCBZCgmGGTlHF_cWlDnoA9XTWWcIYNyUI4PXNw"
```

## Validating the Signature
1. Decode headers (to see what algo is used to sign the JWT)
2. Decode payload
3. Hashing
4. Decrypt the signature with public key.
5. Compare hash
6. Verify Claims
