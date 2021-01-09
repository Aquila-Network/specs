# Document

**Authors:  *Jubin Jose*, *Nibin Peter***



Just like we define a [database](https://github.com/Aquila-Network/specs/blob/main/adb/Creating%20a%20database.md) as a JSON object, a document in Aquila DB is another JSON object which complies to the database schema. A document ID is deterministic and is generated based on the [content address](https://github.com/Aquila-Network/specs/blob/main/adb/Content%20Addressing.md) (CID) of the document itself.



## Document life-cycle

In Aquila DB a document can have any of the following two states - `created` and `deleted`. The documents are immutable. Meaning, once a document is created, it cannot be modified (updated). This is because, once the content of a document is changed, the content ID should also be changed. Which thus becomes a new independent document that contradicts with the concept of update.



> Note: Just like any other API, a document creation / deletion API expects the request to be signed by appropriate key from the wallet. This is to future proof data ownership and authorization wherever this document goes across Aquila Network. Please refer API section for more information.



### Creating a document

To create a document, construct a valid JSON object which follows the schema definition of database we are interested in. Document ID is deterministic (generated from the document content itself) thus is already known to both user and Aquila Network modules. So, the document ID is not required to be specified in the document itself. However for convenience, an Aquila DB instance should return the document ID upon successful creation.



```python
document_id = create_document_API(sign_message(JSON_document, database_name))
```



### Deleting a document

Since a document is immutable, delete operation doesn't really delete a document from the database. Instead a document is `"flagged"` as `deleted` or `not deleted`. This simple concept has the following advantages:

- A document can be created and deleted at independent instances / geolocation across the network.

- Maintains a reproducible state history for every document. This allows anyone ask questions such as "what was the snapshot of a specific database at a specific time?" without actually worrying about maintaining database snapshots.

  

```python
document_id = delete_document_API(sign_message(document_id, database_name))
```

**Flag operation**

```python
def delete_document_API (document_id, database_name):
    document_reference = get_reference_to_document(document_id, database_name)
    document_reference[__deleted__] = True
```





> Note: Independent, conflicting operations over document states are resolved `eventually`, through [`"eventual consistency"`](https://en.wikipedia.org/wiki/Eventual_consistency) strategies. It is important to note that, Aquila DB is not a real time database but an eventually consistent one with guaranteed state convergence.



### Updating a document

As mentioned earlier, there is no update operation available in Aquila DB to keep things very simple. An update operation is considered to be done at the user managed high-level layer by abstracting a sequence of a `delete` followed by a `create` operations. The user is supposed to map newly returned document ID to the old one accordingly at the higher level.



> Reasoning behind decision: Since, Aquila Network will most probably be used with an already existing system which already use other mutable databases, this immutability strategy wouldn't make much issues to the large population with a better trade-off for simplicity and scalability.