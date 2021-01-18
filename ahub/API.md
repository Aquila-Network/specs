# API

**Authors:  Jubin Jose**



Make API request with header `headers["Content-Type"] = "application/json"`.



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

[POST]  /prepare

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