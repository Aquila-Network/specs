# Asymmetric key signing

**Authors:  *Jubin Jose*, *Nibin Peter***



Aquila DB currently supports wallets that use private-public key pairs to sign messages. The wallets that support public key cryptography optionally, DIDs thus becomes compatible by default. An asymmetric key pair enables independent signing of messages (to claim ownership) with a private key at the client (user) side and validation of the claim at the server (Aquila DB and others) side. The biggest advantages this independency can offer are the following:

- Aquila Network APIs can be configured to Authenticate and Authorize requests based on their DID signatures.
- Aquila DB is an eventually consistent database. This means the document operations can wait and be validated at any point of time without maintaining a session with the client.
- Eventual consistency is applicable to replication of documents through the network. Any node in the Aquila Network could validate the replicated document of its ownership.
- A node in the Aquila Network can be configured to accept / reject certain documents based on their signatures or owners. 
- Any document in the Aquila Network is by default associated with a DID, which brings in trust from the real / virtual world over time.
- In later times, DIDs can be rewarded for their value addition as data / information to the network or as a node executor.



#### Pseudo-code for generating signature of a JSON request

```python
def sign_message (JSON_request)
    bson_request = bson(JSON_request)
    hash = SHA384(bson_request)
    
    # Sign with pvt key
    signature = pkcs1_15(hash, priv_key)
    signature = base58(signature).decode("utf-8")
```

> JSON_request formats depends upon the type of operation. Please refer API specifications for each module for more information

### RSA

##### RSASSA-PKCS1-v1_5 (PKCS#1)

Currently Aquila DB supports the following PKCS#1 configuration to validate signatures:

```
RSA Private-Key: (2048 bit, 2 primes)

Hashing algorithm: RSA-SHA384
```

##### RSASSA-PSS 

`coming soon`

### ECDSA

`coming soon`