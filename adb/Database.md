# Database (Search Index)

A database in Aquila DB is a collection of documents that conforms to a schema definition. It can also be considered as a search index since one of its main function is to serve nearest neighbour queries from within the indexed documents. A database name is universal and is deterministically generated from it's [schema](https://github.com/Aquila-Network/specs/blob/main/adb/Schema.md) definition's [content address](https://github.com/Aquila-Network/specs/blob/main/adb/Content%20Addressing.md).



##### Life cycle of a database

A database is not owned by anyone, but a document is, - owned by a wallet. Databases can neither be created nor be destroyed. It exists forever in the realm of possible combinations constrained by the set of symbols and string length (base-58, 44 characters). A new database can be discovered by making changes to the schema definition ([refer the algorithm for database naming](https://github.com/Aquila-Network/specs/blob/main/adb/Content%20Addressing.md#cid-in-aquila-db)). A database can only be transformed from one another, by making changes to schema definition, followed an application of a `transformation function` over each and every document entries. 

