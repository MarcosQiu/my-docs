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
## Object Encryption
## S3 Object Storage Class
## S3 Lifecycle Configuration
## S3 Replication
## S3 Presigned URLs
## S3 Select and Glacier Select
## S3 Events
## S3 Access Logs