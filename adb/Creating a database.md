# Creating a database

**Authors:  *Jubin Jose*, *Nibin Peter***



A database creation process starts from [schema definition](https://github.com/Aquila-Network/specs/blob/main/adb/Schema.md#schema-definition). Below is the pseudo-code to generate a database from given schema:

> Note: content inside angle brackets `<>` should be replaced accordingly based on the programming language used.



### At the user / client side

```python
user_defined_schema = {
    "description": "Database description",
    "unique": "random string",
    "encoder": "example.com/autoencoder.model",
    "codelen": <vector length integer>,
    "metadata": {
        "key 1": "type",
        "key 2": "type",
        ...
    }
}

def sign_message (JSON_object):
    return <Refer Aquila DB API specification to see modified JSON which is returned>

# call Aquila DB API to create a database and get database name in return
database_name = AquilaDB_DB_create_API(sign_message(user_defined_schema))
```



### At the server / Aquila DB side

```python
def AquilaDB_DB_create_API (user_defined_schema):
    # predefine metadata to be used in schema
    metadata_pre = {}
    for each `key` in sorted(user_defined_schema.metadata.list_keys()):
        metadata_pre[`key`] = {
            "type": <user_defined_schema.metadata[key]>
        }
    
    # generate actual schema from user defined schema
    generated_schema = { 
        "$schema": "http://json-schema.org/schema#", 
        "$id": "//aquilanetwork/schema/id/v1", 
        "title": "Schema", 
        "description": <user_defined_schema.description>,
        "encoder": <user_defined_schema.encoder>,
        "unique": <user_defined_schema.unique>,
        "type": "object",
        "properties": {
            "code": {
                "description": "Encoded data",
                "type": "array",
                "maxItems": <user_defined_schema.codelen>
                "items": {
                    "type": "number"
                }
            },
            "metadata": {
                "$ref": "#/definitions/metadata"
            }
        },
        "definitions": {
            "metadata": {
                "description": "User defined metadata",
                "type": "object",
                "properties": <metadata_pre>,
                "required": [<user_defined_schema.metadata.list_keys()>]
            }
        },
        "required": ["code", "metadata"]
    }
    
    # generate database name from content ID of schema
    # refer schema specification for pseudo-code
    database_name = CID(generated_schema)
    # create <AquilaDB data>/<database name> directory inside host file system 
    # & keep a copy of schema, empty key-value storage & empty vector storage
    status = init_database(database_name, generated_schema)
    # return database name with status
    return status, database_name
```

