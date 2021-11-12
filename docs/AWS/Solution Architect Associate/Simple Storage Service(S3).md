## S3 Security (Resource Policies & ACLs)



## S3 Static Hosting

 - Normal access is via AWS APIs.
 - This feature allows access via HTTP.
 - Index and error documents are set (HTML file).
 - Website endpoint is created.
 - Custom domain via Route53, bucket name matters.

### Usage

 - Offloading: put static media in S3.
 - Out-of-band pages: have a static page to show some maintenance info.

### Pricing

 - Data storage, per GB per month.
 - Data transfer fee.
 - Certain costs per 1000 operations.


## Object Versioning & MFA Delete

Versioning lets you store multiple versions of objects within a bucket. Operations which would modified objects generate a new version.

### Enable/Disable/Suspend Versioning

 - Versioning is on bucket level, it's turned off by default.
 - Once versioning is turned on, it can't be turned off.
 - After the versioning is turned on, you can suspend the versioning and turn it back to enabled later.

### Without Versioning

Objects are identified by key (name), their id are set to null.

### With Versioning

Ids are allocated to objects. When retrieving, latest version are returned by default. But can get specific version individually as well.

When delete without giving version id, it just creates a new special version (delete marker) on top.

To actually remove a version, you just specify the version id that you want to remove.

### MFA Delete

 - Enabled in versioning configuration.
 - MFA is required to change bucket versioning state.
 - MFA is required to delete versions.
 - Serial number (MFA) + Code passed with API calls.

## S3 Performance Optimization

#### Upload objects with single PUT request

 - Single data stream to S3
 - If the stream fails, the upload fails and requires full restart
 - Speed & reliability is limited because there is only one stream
 - Maximum object size of 5GB

#### Upload objects with multiple PUT requests

 - Objects are broken up into smaller pieces
 - Minimum object size of 100MB to be able to turn on this feature
 - The object can be split into a maximum of 10000 pieces, for each piece, it can range in size between 5MB and 5GB
 - The last piece can be less than 5MB
 - The whole upload can partially fail, just need to restart for that part
 - Transfer rate equals to the sum of the speed of all parts

### S3 accelerated transfer

S3 is public regional service, **using the public Internet for data transfer is never an optimal solution**. To improve the performance, we can use the network of AWS edge locations. Data get transferred to the edge locations first, and then send to the bucket via AWS network. This feature is off by default, to turn it on,

 1. bucket name cannot contain periods,
 2. it needs to be DNS compatiable in its naming.

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

### SSE-S3

 - S3 endpoints handles encryption/decryption processes and key management, so there is no admin overhead.
 - For each object, s3 generates an unqie key to encrypt the object, and encrypts the key with a master key, the encrypted object & key pair is kept in storage.
 - It's not suitable if: 
    1. you need to control & get access to keys 
    2. you need to take control of key rotation 
    3. you need role separation (different roles have different set of permissions)

### SSE-KMS

 - Different from SSE-S3, an AWS managed CMK is generated in KMS to encrypt the keys.
 - S3 is provided with a pair of DEKs, a plaintext and an encrypted versions, to encrypt the object.
 - Instead of using AMS managed CMK, can also use customer CMK.
 - It gives control ono the key management & key rotation.
 - It makes role separation possible (S3 admin that has no access to KMS cannot see the content of the objects in S3).

### Bucket Default Encryption

When uploading, can hae the header `x-amz-server-side-encryption` in request, to specify the encryption type, e.g.

 - `AMS256` -> `SSE-S3`
 - `aws:kms` -> `SSE-KMS`

## S3 Object Storage Class
## S3 Lifecycle Configuration
## S3 Replication
## S3 Presigned URLs
## S3 Select and Glacier Select
## S3 Events
## S3 Access Logs