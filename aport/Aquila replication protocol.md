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

The Replicator MUST ensure that Target exist and node ID is valid by using `GET /{db}` request.

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
'                                     v                            '
'                         +------------------------+               '
'                         | Get Target Information |               '
'                         +------------------------+               '
'                         |     GET /targetDB      |               '
'                         +------------------------+               '
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