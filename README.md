# Aquila Network Specifications

This repository contains the technical specification for Aquila Network component protocols. Follow this specification to implement core components of Aquila Network Ecosystem and to connect to the network. If you prefer to use implementations by Aquila Network team please visit our [Github Repository](https://github.com/Aquila-Network).



## Index

#### **[Aquila Network overview](https://github.com/Aquila-Network/specs/blob/main/Aquila%20Network.md)**
#### **[Aquila DB](https://github.com/Aquila-Network/specs/blob/main/adb/Aquila%20DB.md)**
- [Content Addressing](https://github.com/Aquila-Network/specs/blob/main/adb/Content%20Addressing.md)
- Authentication & Ownership
	- Asymmetric key signing
		- RSA
		- ECDSA
	- Notion of a wallet
- [Database (search index)](https://github.com/Aquila-Network/specs/blob/main/adb/Database.md)
	- Schema
    - [Schema definition](https://github.com/Aquila-Network/specs/blob/main/adb/Schema.md)
    - Metadata
    - Schema validation
	- Creating a database
- Document
	- Document lifecycle
		- Creating a document
		- Deleting a document
		- Updating a document
- Vector search
	- Vector indexing
		- Full search
		- Bucket search
		- k-NN search
		- Radius search
		- Notion of error
- API
#### Aquila **Port**
- Eventual consistency of events
	- Version managing a document
		- Version ID convention
	- Conflict resolution
		- Timestamp
		- Block-height
- Couch replication protocol
- Ceramic protocol
- IPFS storage
- API
#### Aquila **Hub**
- Dynamic loading a model
- Serving a model
- API
#### Aquila **X**
- API
