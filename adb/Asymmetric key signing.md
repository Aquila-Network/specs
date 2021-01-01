# Asymmetric key signing

**Authors:  *Jubin Jose*, *Nibin Peter***



Aquila DB currently supports wallets that use private-public key pairs to sign messages. The wallets that support public key cryptography optionally, DIDs thus becomes compatible by default. An asymmetric key pair enables independent signing of messages (to claim ownership) with a private key at the client (user) side and validation of the claim at the server (Aquila DB and others) side. The biggest advantages this independency can offer are the following:

- Aquila Network APIs can be configured to Authenticate and Authorize requests based on their DID signatures.
- Aquila DB is an eventually consistent database. This means the document operations can wait and be validated at any point of time without maintaining a session with the client.
- Eventual consistency is applicable to replication of documents through the network. Any node in the Aquila Network could validate the replicated document of its ownership.
- A node in the Aquila Network can be configured to accept / reject certain documents based on their signatures or owners. 
- Any document in the Aquila Network is by default associated with a DID, which brings in trust from the real / virtual world over time.
- In later times, DIDs can be rewarded for their value addition as data / information to the network or as a node executor.

### RSA

### ECDSA

