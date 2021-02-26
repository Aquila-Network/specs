# Aquila Port 

**Authors:  *Jubin Jose*, *Nibin Peter***



Aquila Port is the data transport layer for Aquila Network. Its prime function is to handle continuous replication of data between Aquila DB nodes in a network. Aquila Port is also capable of discovering databases and documents across the network automatically.



## Aquila Replication Protocol

Aquila Replication Protocol is not built from scratch. It is a modified version of infamous [Couch Replication Protocol](https://docs.couchdb.org/en/stable/replication/protocol.html) adopted for content addressing and custom conflict resolution. 

> Current version of Aquila Replication Protocol is minimal and experimental as a proof of concept.  Breaking changes may apply in future versions to incorporate authentication, authorization and content addressed redundancy control.

