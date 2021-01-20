# API

**Authors:  Jubin Jose**


Some API requests are marked to be cryptographically signed before making into Aquila Hub. Below are the generic steps for making API requests.

1. Prepare a JSON message as it is specified under each API below.
2. If required, sign the JSON message as specified in [asymmetric key signing](https://github.com/Aquila-Network/specs/blob/main/adb/Asymmetric%20key%20signing.md#pseudo-code-for-generating-signature-of-a-json-request) section.
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

**1. Get Aquila Hub node status:** 

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
**1. Prepare a model:**

[POST]  /prepare [Sign message]

request:

```python
{ 
    "databaseName": <String>,
    "schema": <JSON schema definition> 
}
```

response:

```python
{
    "success": <Boolean>,
    "databaseName": <String>
}
```


**2. Compress data:**

[POST]  /compress

request:

```python
{ 
    "databaseName": <String>, 
    "text": <String array>
}
```

response:

```python
{
    "success": <Boolean>,
    "vectors": <2D Floating point array>
}
```