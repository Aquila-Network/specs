<div align="center">
  <a href="https://aquila.network">
    <img
      src="https://user-images.githubusercontent.com/19545678/133918727-5a37c6be-676f-427b-8c86-dd50f58d1287.png"
      alt="Aquila Network Logo"
      height="64"
    />
  </a>
  <br />
  <p>
    <h3>
      <b>
        Aquila Network Specifications 
      </b>
    </h3>
  </p>
  <p>
    <b>
      v0.1.0 (draft)
    </b>
  </p>
  <br/>
</div>

This repository contains the technical specification for Aquila Network component protocols. Follow this specification to implement core components of Aquila Network Ecosystem and to connect to the network. If you prefer to use implementations by Aquila Network team please visit our [Github Repository](https://github.com/Aquila-Network).



## Index

#### [Aquila Network overview](https://github.com/Aquila-Network/specs/blob/main/Aquila%20Network.md)
#### [Aquila DB](https://github.com/Aquila-Network/specs/blob/main/adb/Aquila%20DB.md)
- [Content Addressing](https://github.com/Aquila-Network/specs/blob/main/adb/Content%20Addressing.md)
- [Authentication & Ownership](https://github.com/Aquila-Network/specs/blob/main/adb/Authentication%20%26%20Ownership.md)
	- [Asymmetric key signing](https://github.com/Aquila-Network/specs/blob/main/adb/Asymmetric%20key%20signing.md)
		- [RSA](https://github.com/Aquila-Network/specs/blob/main/adb/Asymmetric%20key%20signing.md#ras)
		- [ECDSA](https://github.com/Aquila-Network/specs/blob/main/adb/Asymmetric%20key%20signing.md#ecdsa)
	- [Notion of a wallet](https://github.com/Aquila-Network/specs/blob/main/adb/Notion%20of%20a%20wallet.md)
- [Database (search index)](https://github.com/Aquila-Network/specs/blob/main/adb/Database.md)
	- [Schema](https://github.com/Aquila-Network/specs/blob/main/adb/Schema.md)
		- [Schema definition](https://github.com/Aquila-Network/specs/blob/main/adb/Schema.md#schema-definition)
		- [Metadata](https://github.com/Aquila-Network/specs/blob/main/adb/Metadata.md)
		- [Schema validation](https://github.com/Aquila-Network/specs/blob/main/adb/Schema%20validation.md)
	- [Creating a database](https://github.com/Aquila-Network/specs/blob/main/adb/Creating%20a%20database.md)
- [Document](https://github.com/Aquila-Network/specs/blob/main/adb/Document.md)
	- [Document life-cycle](https://github.com/Aquila-Network/specs/blob/main/adb/Document.md#document-life-cycle)
		- [Creating a document](https://github.com/Aquila-Network/specs/blob/main/adb/Document.md#creating-a-document)
		- [Deleting a document](https://github.com/Aquila-Network/specs/blob/main/adb/Document.md#deleting-a-document)
		- [Updating a document](https://github.com/Aquila-Network/specs/blob/main/adb/Document.md#updating-a-document)
- [Vector search](https://github.com/Aquila-Network/specs/blob/main/adb/Vector%20search.md)
	- [Vector indexing](https://github.com/Aquila-Network/specs/blob/main/adb/Vector%20search.md#vector-indexing)
		- [Full search](https://github.com/Aquila-Network/specs/blob/main/adb/Vector%20search.md#full-search)
		- [Bucket search](https://github.com/Aquila-Network/specs/blob/main/adb/Vector%20search.md#bucket-search)
		- [k-NN search](https://github.com/Aquila-Network/specs/blob/main/adb/Vector%20search.md#k-nn-search)
		- [Radius search](https://github.com/Aquila-Network/specs/blob/main/adb/Vector%20search.md#radius-search)
		- [Notion of error](https://github.com/Aquila-Network/specs/blob/main/adb/Vector%20search.md#notion-of-error)
- [API](https://github.com/Aquila-Network/specs/blob/main/adb/API.md)
#### [Aquila Port](https://github.com/Aquila-Network/specs/blob/main/aport/Aquila%20Port.md)
- [Eventual consistency of events](https://github.com/Aquila-Network/specs/blob/main/aport/Eventual%20consistency%20of%20events.md)
	- [Version managing a document](https://github.com/Aquila-Network/specs/blob/main/aport/Eventual%20consistency%20of%20events.md#version-managing-a-document)
		- [Version ID convention](https://github.com/Aquila-Network/specs/blob/main/aport/Eventual%20consistency%20of%20events.md#version-id-convention)
	- [Conflict resolution](https://github.com/Aquila-Network/specs/blob/main/aport/Eventual%20consistency%20of%20events.md#conflict-resolution)
		- [Block-height](https://github.com/Aquila-Network/specs/blob/main/aport/Eventual%20consistency%20of%20events.md#block-height)
		- [Timestamp](https://github.com/Aquila-Network/specs/blob/main/aport/Eventual%20consistency%20of%20events.md#timestamp)
		- [Delete status](https://github.com/Aquila-Network/specs/blob/main/aport/Eventual%20consistency%20of%20events.md#delete-status)
- [Aquila Replication Protocol](https://github.com/Aquila-Network/specs/blob/main/aport/Aquila%20replication%20protocol.md)
- [API](https://github.com/Aquila-Network/specs/blob/main/aport/API.md)
#### [Aquila Hub](https://github.com/Aquila-Network/specs/blob/main/ax/Aquila%20Hub.md)
- [Dynamic loading a model](https://github.com/Aquila-Network/specs/blob/main/ahub/Dynamic%20loading%20a%20model.md)
- [Serving a model](https://github.com/Aquila-Network/specs/blob/main/ahub/Serving%20a%20model.md)
- [API](https://github.com/Aquila-Network/specs/blob/main/ahub/API.md)
#### [Aquila X](https://github.com/Aquila-Network/specs/blob/main/ax/Aquila%20X.md#aquila-x)
- [UI](https://github.com/Aquila-Network/specs/blob/main/ax/Aquila%20X.md#ui)
- [Functionalities](https://github.com/Aquila-Network/specs/blob/main/ax/Aquila%20X.md#aquila-x-functionalities)
- [API](https://github.com/Aquila-Network/specs/blob/main/ax/Aquila%20X.md#x-api)
