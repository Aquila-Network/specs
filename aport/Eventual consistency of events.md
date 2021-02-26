# Eventual consistency of events

**Authors:  *Jubin Jose*, *Nibin Peter***



Aquila Network is eventually consistent. Aquila Replication Protocol is the real reason behind it. Any independent Aquila DB node could accept any version of a document. These documents are then replicated through the network to eventually reach a common state with deterministic agreement on dictating versions. Aquila Network tades off consistancy for scalability and decentralization. 

## Version managing a document

Encounter of conflicting documents during replication is very common in eventual consistent networks. Conflicts are managed based on a resolution algorithm tailored for specific networks. In Aquila Network, its a simple and straight forward algorithm. The document with highest version number dictates its rival and survives in the network.

### Version ID convention

Because Aquila Network simply accepts the highest version number during conflict resoluthin, a version ID of a document should reflect the order in which each transaction has occurred. To establish this criteria, Aquila DB takes in account the following parameters to determine the version ID of a document. 

- Anchor block number (string)
- UNIX timestamp of the transaction (integer)
- Has the document deleted? (boolean)

Below is the pseudocode to generate version id of a document during a `create` or `delete` transaction:

**Create a document:**

```python
version_id = anchor_document(JSON_document) + str(get_current_timestamp()) + str(0)
```

**Delete a document:**

```python
version_id = anchor_document(JSON_document) + str(get_current_timestamp()) + str(1)
```

**Helper functions:**

```python
def anchor_document (JSON_document) -> str:
  blockchain_id, block_number, anchor_proof = service_make_anchor_transaction(JSON_document)
  # Note: anchor proof is ignored in this version of specification, 
  # assuming replication happens between trusted parties
  return str(blockchain_id+block_number)

def get_current_timestamp() -> int:
  return get_current_13_digit_UNIX_timestamp_in_milliseconds()
```

## Conflict resolution

Aquila Network is fully decentralized. It assumes a database to be created in any possible subgraph in a network. It can be a standalone offline node, nodes in a restricted network or it can be a public node.  With this setting, database collisions between nodes across the network is highly probable. So, in general a node is assumed to be dynamic in a sense that it can join or leave the network dynamically. So, from a random node's perspective, it can synchronize with any other node in the network at anytime as long as they are interested the same database, while manipulating its contents independently. In addition scalability, flexibility, redundancy, and reliability with load balancing are some other advantages that this architecture could offer by design.



The advantages we have stated above comes with an expense of conflicts in transactions. There might exist atleast two conflicting transactions that happened independently. These conflicts need to be resolved within a node acroos the network as they join and replicate local changes into the network. With a `deterministic` algorithm which favour a `set of properties` of transactions over other would eventually settle the entire network to a global state. 



Aquila Network resolves conflicts based on `version ID` of transactions (documents). The `highest version ID survives`. For more details on version ID generation, please refer the section - [Version managing a document](#Version managing a document). In below sections, each property which contributes to a version number is discussed in detail.

### Block-height

*To be done soon*

> Note: Taking Block height into account involves breaking changes in some parts of Aquila Network specification. 
>
> In this version block height is fixed to "0". Discussions on proposed chanes are currently in progress.

### Timestamp

A timestamp is 13 digit [UNIX timestamp](https://en.wikipedia.org/wiki/Unix_time) - which is the adjusted number of milliseconds elapsed since Unix epoch.

### Delete status

In Aquila DB, there are two types of transactions related to a document - create and delete. Aquila DB documents are immutable. Which means there is no update operation. Logically, a delete operation should be considered as an update. However, Aquila Network eliminates a need for this by setting a `delete flag`  to the version id without making any modfications to the original document.