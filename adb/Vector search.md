# Vector search

**Authors:  *Jubin Jose*, *Nibin Peter***



It is mentioned in other part of the specification that, Aquila DB keeps document and vector indices separately. Any operation on document keys or vectors are separately done. Aquila DB internally maintains a mapping between vectors and documents to keep consistency between them.



### Vector indexing

Vector indexes are long matrices having dimension **d**x**n**. **d** is a fixed number for a database and is computed as **min(**[**schema.maxItems**](https://github.com/Aquila-Network/specs/blob/main/adb/Creating%20a%20database.md#at-the-server--aquila-db-side),  [**config.docs.vd**](https://github.com/Aquila-Network/AquilaDB/blob/master/src/DB_config.yml)**)**. **n** is the number of vectors inserted to the database (and not deleted) so far. Maintaining a single long matrix is just a concept. An implementation of Aquila DB is expected to keep the index as small chunks to enable distributed scaling and data redundancy (reliability). 



There is a set of methods to do chunking called bucketization. These methods try to come up with a hashing (central point) algorithm which clusters vectors based on their distance from one another. Popular examples include pre-trained [k-means clustering](https://en.wikipedia.org/wiki/K-means_clustering), [locality sensitive hashing](https://en.wikipedia.org/wiki/Locality-sensitive_hashing), special [rolling hashes](https://en.wikipedia.org/wiki/Rolling_hash) etc. 



> Note: Official Aquila DB implementation currently uses k-means clustering to generate buckets.



## Domain constraints in search

### Full search

Full search allows anyone to search the entire matrix chunks without any constraints. This should be done when in need for 100% accuracy with a trade-off of increased latency. Aquila DB implementations should do an exhaustive search over all distributed instances at once.

### Bucket search

Bucket searches are limited to a pre-configured / dynamically specified number of closest buckets. This improves search performance with a trade-off of reduced accuracy. Scale of accuracy drops purely depends upon the bucketization algorithm used by implementations. Please refer [Notion of error](https://github.com/Aquila-Network/specs/blob/main/adb/Vector%20search.md#notion-of-error) section below for more information on measuring accuracy of implementations.



## Content constraints in search

### k-NN search

### Radius search



### Notion of error