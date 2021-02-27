# API

**Authors:  *Jubin Jose*, *Nibin Peter***



## API definitions

**1. Get Aquila Port node status:** 

[GET]  /

request:  

```python
{}
```

response:

```python
{
    {"nodeId":<UUID String>}
}
```

## 

**2. Database exists:** 

[HEAD]  /<database name>

request:  

```python
{}
```

response:

```python
{}
```

## 

**3. Create Database:** 

[PUT]  /<database name>

request:  

```python
{}
```

response:

```python
{
  "ok":<Status Boolean>
}
```

**4. Get Database Information:** 

[GET]  /<database name>

request:  

```python
{}
```

response:

```python
{
  "db_name":<Database name String>
}
```

**5. Bulk Insert Documents:** 

[POST]  /<database name>/_bulk_docs

request:  

```python
[{
    "id": <Document ID String>,
    "deleted": <Delete status Boolean>,
    "timestamp": <UNIX Timestamp String>,
    "payload": <Payload data String>,
    "signature": <Payload signature String>
},
  ...
]
```

response:

```python
[{
    "id": <Document ID String>,
    "deleted": <Delete status Boolean>,
    "timestamp": <UNIX Timestamp String>,
  	"version": <Version number String>,
    "payload": <Payload data String>,
    "signature": <Payload signature String>
},
  ...
]
```

**6. Bulk Get Documents:** 

[GET]  /<database name>/_all_docs

request:  

```python
{}
```

response:

```python
[{
    "id": <Document ID String>,
    "deleted": <Delete status Boolean>,
    "timestamp": <UNIX Timestamp String>,
  	"version": <Version number String>,
    "payload": <Payload data String>,
    "signature": <Payload signature String>
},
  ...
]
```

**7. Get Changes List:** 

[GET]  /<database name>/_changes

request:  

```python
{}
```

response:

```python
{
  "last_seq": <Last Sequence Integer>,
  "pending": <Pending results Integer>,
  "results": [
    {
      "changes": [
        {
          "rev": <Version number String>
        }
      ],
      "id": <Document ID String>,
      "seq": <Document sequence Integer>,
      "deleted": <Deleted status Boolean>
    },
    ...
  ]
}
```

**8. Send Revision Differences:** 

[POST]  /<database name>/_revs_diff

request:  

```python
{
    <Document ID String>: [
        <Version number String>
    ],
  	...
}
```

response:

```python
{
  <Document ID String>: [
    <Version number String>
  ],
  ...
}
```

**9. Commit Replicated Changes:** 

[POST]  /<database name>/_ensure_full_commit

request:  

```python
{}
```

response:

```python
{
  "ok":<Commit status Boolean>
}
```

**10. Update Replication Checkpoint:** 

[PUT]  /<database name>/_local

request:  

```python
{
    "id": <Replication ID String>,
    "ok": true,
    "rev": <Version number String>
}
```

response:

```python
{
    "id": <Replication ID String>,
    "ok": true,
    "rev": <Version number String>
}
```

**11. Enable Push Replication:** 

[POST]  /<database name>/replicate

request:  

```python
{
    "target": <Target node ex:"http://localhost:5007/" String>
}
```

response:

```python
{
    "target": <Target node ex:"http://localhost:5007/" String>
}
```

**12. Disable Push Replication:** 

[DELETE]  /<database name>/replicate

request:  

```python
{
    "target": <Target node ex:"http://localhost:5007/" String>
}
```

response:

```python
{
    "target": <Target node ex:"http://localhost:5007/" String>
}
```

