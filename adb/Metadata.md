# Metadata

**Authors:  *Jubin Jose*, *Nibin Peter***



Aquila DB is vector + document database. The reasons for choosing this combination are the following:



Vectors are abstract (lossy / lossless compression) information. It represents something meaningful in the real world. However, the vector representation itself is not self explanatory. It should be accompanied by a global transformation (as defined by the probability distribution) function and an associated metadata. All three components above are needed together to represent a real world meaning. Missing / misalignment of at least one component would result in chaos.



In Aquila DB, metadata should always be associated with the vector. It is the least amount of data, which is needed to unravel the entire information outside of Aquila DB. For example, it can simply be an `id` towards information stored in some other databases such as MySQL or MongoDB. It can also be URLs, ContentIDs, Link to other Aquila DB documents etc. Metadata in Aquila DB is a `JSON` object. JSON objects are the most friendly data structure to most of the [agents](https://en.wikipedia.org/wiki/Agent_(economics)) we know.



For convenience, Aquila DB requires the expected `keys` in `metadata` object to be defined early on as part of [schema definition](https://github.com/Aquila-Network/specs/blob/main/adb/Schema.md#schema-definition) along with the data types. And when vectors are inserted, the documents are checked for metadata (all keys are mandatory) and validated. 



Currently, accepted types of metadata values are `string` and `number`.



> **Important**: Aquila DB will accept any extra information added to the document. This information will be treated as payload, will be moved to a secondary storage, will not be replicated through Aquila Network but the secondary storage network and is ignored in querying and filtering operations.

> Aquila DB users must maintain external storage networks and second level filtering mechanisms outside of Aquila DB.

