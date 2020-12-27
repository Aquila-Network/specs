# Aquila DB

Aquila DB is at the core of everything in the Aquila Network ecosystem. It is a standalone latent vector search engine. Aquila DB allows the following, very basic operations:

- Create database

  Aquila DB accepts a schema definition and based on that schema, a database is created. Apart from other common databases, database name in Aquila DB is not decided by the user but Aquila DB itself. Database name is generated from the content id of schema definition to ensure a predictable name for anyone who use the same schema, anywhere around the globe. Here's the magic: when a user connect their existing Aquila DB instance to participate in Aquila Network, this simple idea of content ID (hence database name) allows replication and synchronization of available documents in a database that anyone has created, automatically across the network. Not to worry of bad actors, it is possible to control what data is replicated to/from your Aquila DB instance, Aquila Network provides special control mechanisms for this.

- Insert documents to a database

  Once a database is created, a user is able to add JSON documents along with its vector embedding. Aquila DB validates the documents against database schema definition. If the validation succeeds, the JSON document and corresponding vector will be indexed inside `doc store` and `vec store` respectively. Similar to database name generation, a document id is auto generated from its content id and it will be returned back to the user. This is to ensure that the same documents created independently across the globe will have same document id. A replication process will then be able to ignore already existing documents through Aquila Network.

- Pseudo delete a document from a database

  Aquila DB is an append only, eventually consistent database. All insert / delete operations are kept inside it as append only logs. When a delete operation is performed, it doesn't actually delete the documents instead marks the document as deleted. The deleted documents will never participate in any of the retrieval operations.

- Search for nearest neighbours

  Nearest neighbour search operation accepts vector encoding and number of documents (**k**) to be retrieved as inputs. Aquila DB will perform cosine similarity search on the indexed documents and will return **k** nearest documents to the query vector.

  >  Note: It is an on going discussion whether to enable filtering on documents based on their JSON values. Since Aquila DB to be a part of already existing software infrastructure and databases, that is dedicated to provide complex filtering options anyway, we thought it might become an over engineered solution which contradicts with Aquila Network's simplicity mission. Also, Aquila X could still filter out Aquila DB's results. We're looking forward to see how community reacts to it.

  