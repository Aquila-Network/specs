# API

**Authors:  *Jubin Jose*, *Nibin Peter***



All API requests should be cryptographically signed before making into Aquila DB. Below are the generic steps for making API requests.

1. Prepare a JSON message as it is specified under each API below.
2. Sign the JSON message as specified in [asymmetric key signing](https://github.com/Aquila-Network/specs/blob/main/adb/Asymmetric%20key%20signing.md#pseudo-code-for-generating-signature-of-a-json-request) section.
3. Wrap JSON message and signature in the following request format: 

```python
data = {
    "data": <JSON message>,
    "signature": signature
}
```

4. Make API request with header `headers["Content-Type"] = "application/json"`.



## API definitions

### Transparency APIs

**1. Get Aquila DB node status:** 

[GET]  /

request:  

```python
{}
```

response:

```python
{
    "success": <Boolean>,
    "message": <String>
}
```



### Transaction APIs

**1. Create a database:**

[POST]  /db/create

request:

```python
{ 
    "schema": <JSON schema definition> 
}
```

response:

```python
{
    "success": <Boolean>,
    "database_name": <String>
}
```

### 

**2. Insert documents:**

[POST]  /db/doc/insert

request:

```python
{ 
    "docs": <JSON documents array>, 
    "database_name": <database name>
}
```

response:

```python
{
    "success": <Boolean>,
    "ids": <String array>
}
```

### 

**3. Delete documents:**

[POST]  /db/doc/delete

request:

```python
{ 
    "ids": <Document id array>, 
    "database_name": <database name> 
}
```

response:

```python
{
    "success": <Boolean>,
    "ids": <String array>
}
```

### 

**4. Search k documents:**

[GET]  /db/search

request:

```python
{ 
    "matrix": <2D array for batch search>, 
    "k": <number k>, # Optional
    "r": <number k>, # Optional
    "database_name": <database name> 
}
```

response:

```python
{
    "success": <Boolean>,
    "docs": <2D JSON array>,
    "dists": <2D Floating-point array>
}
```

