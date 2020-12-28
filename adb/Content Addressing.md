# Content Addressing

**Authors:  *Jubin Jose*, *Nibin Peter***



### Introduction

Content addressing (**CID**) is at the core of everything in Aquila Network ecosystem. It is becoming new standard in the peer-to-peer web technologies. Any data being served over a network can be addressed uniquely by what bits it contains. This ensures a deterministic, unique address that is associated with the signature of the data at its entirety. In the past, any content over the web is addressed by the directory (location) it is stored in. For example, a file hosted in an FTP server is addressed in the following format: `<IP address (location of the server)>/<root directory>/<level 1 directory>/.../<level n directory/<file name>`. 



The biggest caveat of this location based addressing mechanism is that, the same file served at multiple places should be addressed with entirely different addresses (**redundancy** is good but most of the times, presence of redundant data is unknown, so everybody adds their own redundant data). This introduces overheads in associating mutually independent location address and the original content and management of this relationship becomes complicated as the data creation process explodes (content **discoverability** meets scaling issues). Adding to this complexity, since the server can replace the content at any location at anytime without leaving any traces of such activity, data **consistency** is a nightmare. Today, we are trying to solve these issues through explicit tools. However it will become infeasible as we face the ever exploding data that grows exponentially. 



Content addressing solves all three issues by design. It solves a lot of problems that got introduces as a side effect of location based addressing. It frees up a lot of compute resources and makes the management tools that tries very hard to meet scalability requirements obsolete. It brings in nice redundancy, discoverability and consistancy of data for free by design.



### CID in Aquila DB

In Aquila DB, A database name and a document id are content addressed. 

**Database Name**:

`database_name = CID(JSON_schema_definition)`

More detail on schema definition can be found at [schema specification](https://github.com/Aquila-Network/specs/blob/main/adb/Schema.md).

**Document id:**

`document_id = CID(JSON_document)`



### Pseudo-code for `CID(JSON_input)` function

Encode `JSON` input to corresponding `BSON` format

`bson_code = bson(JSON_input)`

Perform `SHA-256` double hashing on `bson_code`

`hash_code = sha256(sha256(bson_code))`

Convert `hash_code` to `Base-58` string

`b58_string = b58encode(hash_code)`

Convert `b58_string` to `utf-8` string

`utf-8_string = utf-8(b58_string)`

