# Aquila Replication Protocol

**Authors:  *Jubin Jose*, *Nibin Peter***



Aquila Replication Protocol is adopted from the original [Couch Replication Protocol](https://docs.couchdb.org/en/stable/replication/protocol.html). Below sections describe Aquila Replication Protocol in detail as a sequence of steps.



## Replication Protocol Algorithm

The Aquila Replication Protocol is not *magical*, but an agreement on usage of the public [Aquila Port HTTP REST API]() to enable Documents to be replicated from Source to Target.

### Verify peers

```
+ - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - +
' Verify Peers:                                                             '
'                                                                           '
'                404 Not Found   +--------------------------------+         '
'       +----------------------- |     Check Target Existence     |         '
'       |                        +--------------------------------+         '
'       |                        |             GET /              |         '
'       |                        +--------------------------------+         '
'       |                          |                                        '
'       |                          | 200 OK                                 '
'       |                          v                                        '
'       |                        +--------------------------------+         '
'       |                        |     Check Target ID Changed    | ----+   '
'       |                        +--------------------------------+     |   '
'       |                        |      Compare local storage     |     |   '
'       |                        +--------------------------------+     |   '
'       |                          |                                    |   '
'       |                          | Target ID Not Found                |   '
'       v                          v                                    |   '
'   +-------+                    +--------------------------------+     |   '
'   | Abort | <----------------- |      Set Status "inactive"     |     |   '
'   +-------+                    +--------------------------------+     |   '
'                                                                       |   '
'                                                       Target ID Found |   '
'                                                                       |   '
+ - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - | - +
                                                                        |
+ - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - | - +
' Verify Database:                                                      |   '
'                                  +------------------------------------+   '
'                                  |                                        '
'                                  v                                        '
'                                +--------------------------------+         '
'                                |        Verify Databases        |         '
'                                +--------------------------------+         '
'                                                                           '
+ - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - +
```

The Replicator MUST ensure that Target exist and node ID is valid by using `GET /` request.

### Verify Databases

```
+ - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - +
' Verify Databases:                                                         '
'                                                                           '
'                  Not Found     +--------------------------------+         '
'       +----------------------- |    Check Source DB Existence   |         '
'       |                        +--------------------------------+         '
'       |                        |       Check local storage      |         '
'       |                        +--------------------------------+         '
'       |                          |                                        '
'       |                          | 200 OK                                 '
'       |                          v                                        '
'       |                        +--------------------------------+         '
'       |                        |    Check Target DB Existence   | ----+   '
'       |                        +--------------------------------+     |   '
'       |                        |         HEAD /targetDB         |     |   '
'       |                        +--------------------------------+     |   '
'       |                          |                                    |   '
'       |                          | 404 Not Found                      |   '
'       v                          v                                    |   '
'   +-------+    No              +--------------------------------+     |   '
'   | Abort | <----------------- |        Create Target DB?       |     |   '
'   +-------+                    +--------------------------------+     |   '
'       ^                          |                                    |   '
'       |                          | Yes                                |   '
'       |                          v                                    |   '
'       |        Failure         +--------------------------------+     |   '
'       +----------------------- |       Create Target DB         |     |   '
'                                +--------------------------------+     |   '
'                                |         PUT /targetDB          |     |   '
'                                +--------------------------------+     |   '
'                                  |                                    |   '
'                                  | 201 Created                 200 OK |   '
'                                  |                                    |   '
+ - - - - - - - - - - - - - - - -  | - - - - - - - - - - - - - - - - -  | - +
                                   |                                    |
+ - - - - - - - - - - - - - - - -  | - - - - - - - - - - - - - - - - -  | - +
' Get DB Information:              |                                    |   '
'                                  +------------------------------------+   '
'                                  |                                        '
'                                  v                                        '
'                                +--------------------------------+         '
'                                |    Get Target DB Information   |         '
'                                +--------------------------------+         '
'                                                                           '
+ - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - +
```

The Replicator MUST ensure that both Source and Target DBs exist by using `HEAD /{db}` requests.

### Get DB information

```
+ - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -+
' Get Target DB infromation:                                       '
'                         +---------------------------+            '
'                         | Check Target DB Existence |            '
'                         +---------------------------+            '
'                                     |                            '
'                                     | 200 OK                     '
'                                     |                            '
+ - - - - - - - - - - - - - - - - - - | - - - - - - - - - - - - - -+
                                      |
+ - - - - - - - - - - - - - - - - - - | - - - - - - - - - - - - - -+
' Get DB Information:                 |                            '
'                                     |                            '
'                 404                 v                            '
'   +-------+  Not Found  +------------------------+               '
'   | Abort | <-----------|     GET /targetDB      |               '
'   +-------+             +------------------------+               '
'                                     |                            '
'                                     | 200 OK                     '
'                                     |                            '
+ - - - - - - - - - - - - - - - - - - | - - - - - - - - - - - - - -+
                                      |
+ - - - - - - - - - - - - - - - - - - | - - - - - - - - - - - - - -+
' Find Common Ancestry:               |                            '
'                                     |                            '
'                                     v                            '
'                         +-------------------------+              '
'                         | Generate Replication ID |              '
'                         +-------------------------+              '
'                                                                  '
+ - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - -+
```

The Replicator retrieves basic information from Target using `GET /{db}` request. 

> Note: currently, any information about target DB that is retrieved is skipped without validation. 200 response is enough to verify that target peer is still up and running with healthy database.

### Find Common Ancestry

```
+ - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - +
' Get DB Information:                                                       '
'                                                                           '
'                             +-------------------------------------------+ '
'                             |           Get Target DB Information       | '
'                             +-------------------------------------------+ '
'                               |                                           '
+ - - - - - - - - - - - - - - - | - - - - - - - - - - - - - - - - - - - - - +
                                |
+ - - - - - - - - - - - - - - - | - - - - - - - - - - - - - - - - - - - - - +
' Find Common Ancestry:         v                                           '
'                             +-------------------------------------------+ '
'                             |          Generate Replication ID          | '
'                             +-------------------------------------------+ '
'                               |                                           '
'                               |                                           '
'                               v                                           '
'                             +-------------------------------------------+ '
'                             |      Get Replication Log from Source      | '
'                             +-------------------------------------------+ '
'                               |                                           '
'                               |                                           '
'                               v                                           '
'                             +-------------------------------------------+ '
'                             |      Get Replication Log from Target      | '
'                             +-------------------------------------------+ '
'                             |    GET /targetDB/_local/replication-id    | '
'                             +-------------------------------------------+ '
'                               |                                           '
'                               | 200 OK                                    '
'                               | 404 Not Found                             '
'                               v                                           '
'                             +-------------------------------------------+ '
'                             |          Compare Replication Logs         | '
'                             +-------------------------------------------+ '
'                               |                                           '
'                               | Use latest common revision as start point '
'                               |                                           '
+ - - - - - - - - - - - - - - - | - - - - - - - - - - - - - - - - - - - - - +
                                |
                                |
+ - - - - - - - - - - - - - - - | - - - - - - - - - - - - - - - - - - - - - +
' Locate Changed Documents:     |                                           '
'                               |                                           '
'                               v                                           '
'                             +-------------------------------------------+ '
'                             |        Listen Source Changes Feed         | '
'                             +-------------------------------------------+ '
'                                                                           '
+ - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - +
```

##### Generate Replication ID

The Replication ID generation algorithm is implementation specific. Whatever algorithm is used it MUST uniquely identify the Replication process. Aquila Port’s Replicator, for example, uses the following factors in generating a Replication ID:

- Source Aquila Port Node ID (already generated as UUID)
- Target Aquila Port Node ID (already generated as UUID)
- Database Name (unique for a specific schema)

```
replication_id = base64( sha( source_node_ID + target_node_ID + databaseName ) )
```

### Locate Changed Documents

```
+ - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - +
' Find Common Ancestry:                                                     '
'                                                                           '
'             +------------------------------+                              '
'             |   Compare Replication Logs   |                              '
'             +------------------------------+                              '
'                                          |                                '
'                                          |                                '
+ - - - - - - - - - - - - - - - - - - - -  |  - - - - - - - - - - - - - - - +
                                           |
+ - - - - - - - - - - - - - - - - - - - -  |  - - - - - - - - - - - - - - - +
' Locate Changed Documents:                |                                '
'                                          |                                '
'                                          |                                '
'                                          v                                '
'            +-------------------------------+                              '
'   +------> |     Listen to Changes Feed    |                              '
'   |        +-------------------------------+      +-------------+         '
'   |        |     Read Batch of Changes     | ---> | Replication |         '
'   |        +-------------------------------+      |  Completed  |         '
'   |                                      |        +-------------+         '
'   |                                      |                                '
'   | No                                   |                                '
'   |                                      v                                '
'   |        +-------------------------------+                              '
'   |        |  Compare Documents Revisions  |                              '
'   |        +-------------------------------+                              '
'   |        |   POST /targetDB/_revs_diff   |                              '
'   |        +-------------------------------+                              '
'   |                                      |                                '
'   |                               200 OK |                                '
'   |                                      v                                '
'   |        +-------------------------------+                              '
'   +------- |     Any Differences Found?    |                              '
'            +-------------------------------+                              '
'                                          |                                '
'                                      Yes |                                '
'                                          |                                '
+ - - - - - - - - - - - - - - - - - - - -  |  - - - - - - - - - - - - - - - +
                                           |
+ - - - - - - - - - - - - - - - - - - - -  |  - - - - - - - - - - - - - - - +
' Replicate Changes:                       |                                '
'                                          v                                '
'            +-------------------------------+                              '
'            |  Fetch Next Changed Document  |                              '
'            +-------------------------------+                              '
'                                                                           '
+ - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - +
```

### Replicate changes

```
+ - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - +
' Locate Changed Documents:                                                       '
'                                                                                 '
'               +-------------------------------------+                           '
'               |      Any Differences Found?         |                           '
'               +-------------------------------------+                           '
'                                                   |                             '
'                                                   |                             '
'                                                   |                             '
+ - - - - - - - - - - - - - - - - - - - - - - - - - | - - - - - - - - - - - - - - +
                                                    |
+ - - - - - - - - - - - - - - - - - - - - - - - - - | - - - - - - - - - - - - - - +
' Replicate Changes:                                |                             '
'                                                   v                             '
'               +-------------------------------------+                           '
'   +---------> |     Fetch Next Changed Document     |                           '
'   |           +-------------------------------------+                           '
'   |             |                                                               '
'   |             |                                                               '
'   |             v                                                               '
'   |           +-------------------------------------+                           '
'   |           |     Put Document Into the Stack     |                           '
'   |           +-------------------------------------+                           '
'   |             |                                                               '
'   |             |                                                               '
'   |             v                                                               '
'   |     No    +-------------------------------------+                           '
'   +---------- |           Stack is Full?            |                           '
'   |           +-------------------------------------+                           '
'   |             |                                                               '
'   |             | Yes                                                           '
'   |             |                                                               '
'   |             v                                                               '
'   |           +-------------------------------------+                           '
'   |           | Upload Stack of Documents to Target |                           '
'   |           +-------------------------------------+                           '
'   |           |      POST /targetDB/_bulk_docs      |                           '
'   |           +-------------------------------------+                           '
'   |             |                                                               '
'   |             | 201 Created                                                   '
'   |             v                                                               '
'   |           +-------------------------------------+                           '
'   |           |          Ensure in Commit           |                           '
'   |           +-------------------------------------+                           '
'   |           |  POST /target/_ensure_full_commit   |                           '
'   |           +-------------------------------------+                           '
'   |             |                                                               '
'   |             | 201 Created                                                   '
'   |             v                                                               '
'   |           +--------------------------------------+                           '
'   |           |     Record Replication Checkpoint    |                           '
'   |           +--------------------------------------+                           '
'   |           | Update source Replication Checkpoint |                           '
'   |           | PUT /targetDB/_local/replication-id  |                           '
'   |           +--------------------------------------+                           '
'   |             |                                                               '
'   |             | 201 Created                                                   '
'   |             v                                                               '
'   |     No    +-------------------------------------+                           '
'   +---------- | All Documents from Batch Processed? |                           '
'               +-------------------------------------+                           '
'                                                   |                             '
'                                               Yes |                             '
'                                                   |                             '
+ - - - - - - - - - - - - - - - - - - - - - - - - - | - - - - - - - - - - - - - - +
                                                    |
+ - - - - - - - - - - - - - - - - - - - - - - - - - | - - - - - - - - - - - - - - +
' Locate Changed Documents:                         |                             '
'                                                   v                             '
'               +-------------------------------------+                           '
'               |               Sleep                 |                           '
'               +-------------------------------------+                           '
'               |       Listen to Changes Feed        |                           '
'               +-------------------------------------+                           '
'                                                                                 '
+ - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - - +
```

### Notes

Below are some noteworthy comments that will come in handy if you are familiar with Couch Replication Protocol.

- Couch Replication Protocol assumes the replication agent to be an independent daemon. In Aquila Port, replication daemon is part of the node itself. This replaces every source API calls in the original Couch Replication Protocol with local database calls as seen above in the Aquila Replication Protocol.
- Aquila Port doesn't implement two way replication (sync). Replication will only happen from source to target (push replication only). To simulate sync, each Aquila Port should perform push replication from both ends.
- Aquila Replication Protocol doesn't support document attachments (out of the scope).
- Aquila Replication Protocol is not compatible with Couch Replication Protocol (as of now atleast).

