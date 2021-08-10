## S3 Security (Resource Policies & ACLs)
## S3 Static Hosting
## Object Versioning & MFA Delete
## S3 Performance Optimization
## Encryption
### Encryption Approaches

#### Encryption At Rest
 - one entity involved
 - e.g. encrypt data before writing to disk

#### Encryption In Transit
 - Multiple individuals or systems involved
 - e.g. encrypted data before sending to others

### Encryption Concepts
- plaintext: unencrypted data, can be document, iamge, app, etc
- algorithm: methods that used to generate encrypted data from plaintext and key
- key: a token that is used to encrypt/decrypt data
- cyphertext: encrypted data

### Symmetric Encryption
Encrypt & decrypt with the same key, however, distributing keys can be really tricky.

### Asymmetric Encryption
Receiver distributes the public key, sender encrypts the plaintext with the public key. Only reciever can decrypt the cypher with its private key.

### Signing
Encrypt the message with own private key and others can decrypt the message with corresponding public key. Normally used for identity verification.

### Steganography
Steganography is the practice of concealing a message within another message or a physical object. In computing contexts, a computer file, message, image is consealed within another file, message, image.

## Key Management Service (KMS)
 - Regional & public service
 - Create, store and manage keys
 - AWS managed/customer managed CMKs
 - Support symmetric & asymmetric keys
 - Cryptographic opertions (encrypt, decrypt and more)
 - **Keys never leaves KMS** - It provides [FIPS](https://en.wikipedia.org/wiki/Federal_Information_Processing_Standards) 140 - 2 (L2)
 - Support aliases, which are also isolated to regions

### CMK - Customer Master Key
 - CMK is logical, has ID, date, policy, desc & state
 - backed by phsical key material
 - generated or imported
 - CMKs can be used for up to 4KB of data

### KMS and CMKs
![image](https://i.ibb.co/kmQy30w/IMG-0545.jpg)

### Data Encryption Keys (DEKs)
DEKs are generated from CMK, used to decrypt/encrypt on data > 4KB. However, this is not part of the KMS, you or the other service need to do this. This is how it works,

1. Generate plaintext version of DEK and cyphertext version of DEK.
2. Encrypt the data using plaintext key & discard it.
3. Store the encrypted key with the data.
4. When decrypt, first decrypt the DEK with KMS.
5. Decrypt the cypher text with the decrypted DEK, and discard the DEK afterwards.

S3 basically generate a DEK for each object that needs to be encrypted.

## Object Encryption

We are talking about encrypting objects, buckets aren't encrypted. There are two types of encryptions,

 - Client-side encryption: Objects are encrypted on users side, users are responsible for managing the keys, performing encryption/decryption. AWS is not involved in the encryption.
 - Server-side encryption: The user send the plaintext (to the other parties, it's still encrypted in transit, but s3 endpoint will receive plaintext) and the encryption happens on the server side.

We mainly focus on server-side encryption.

### SSE-C

 - Server-side encryption with customer provided keys.
 - Users are responsible for managing keys.
 - Users send object and key to s3 endpoint, on the server side, object is encrypted and a hash of the key is generated, then, the server writes the key hash and cyphertext to the storage, and discard the key.
 - When fetch object, users provide the key to decrypt objects they want to fetch, the server will generate the hash and compare with the key hash stored in storage.


## S3 Object Storage Class
## S3 Lifecycle Configuration
## S3 Replication
## S3 Presigned URLs
## S3 Select and Glacier Select
## S3 Events
## S3 Access Logs