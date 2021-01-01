# Aquila Network Specifications

This repository contains the technical specification for Aquila Network component protocols. Follow this specification to implement core components of Aquila Network Ecosystem and to connect to the network. If you prefer to use implementations by Aquila Network team please visit our [Github Repository](https://github.com/Aquila-Network).



## Index

#### **[Aquila Network overview](https://github.com/Aquila-Network/specs/blob/main/Aquila%20Network.md)**
#### **[Aquila DB](https://github.com/Aquila-Network/specs/blob/main/adb/Aquila%20DB.md)**
- [Content Addressing](https://github.com/Aquila-Network/specs/blob/main/adb/Content%20Addressing.md)
- [Authentication & Ownership](https://github.com/Aquila-Network/specs/blob/main/adb/Authentication%20%26%20Ownership.md)
	- [Asymmetric key signing](https://github.com/Aquila-Network/specs/blob/main/adb/Asymmetric%20key%20signing.md)
		- [RSA](https://github.com/Aquila-Network/specs/blob/main/adb/Asymmetric%20key%20signing.md#ras)
		- [ECDSA](https://github.com/Aquila-Network/specs/blob/main/adb/Asymmetric%20key%20signing.md#ecdsa)
	- [Notion of a wallet](https://github.com/Aquila-Network/specs/blob/main/adb/Notion%20of%20a%20wallet.md)
- [Database (search index)](https://github.com/Aquila-Network/specs/blob/main/adb/Database.md)
	- [Schema](https://github.com/Aquila-Network/specs/blob/main/adb/Schema.md)
		- [Schema definition](https://github.com/Aquila-Network/specs/blob/main/adb/Schema.md#schema-definition)
		- Metadata
		- Schema validation
	- Creating a database
- Document
	- Document life-cycle
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
