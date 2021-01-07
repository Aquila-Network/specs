# Schema

**Authors:  *Jubin Jose*, *Nibin Peter***



A schema is a [JSON Schema](https://json-schema.org/) object which takes the following form. The ordering of keys should be maintained the same way as seen below: 

```json
{ 
        "$schema": "http://json-schema.org/schema#", 
        "$id": "//aquilanetwork/schema/id/v1", 
        "title": "Schema", 
        "description": "<collected from the user API>",
        "encoder": "<collected from the user API>",
        "unique": "<collected from the user API>",
        "type": "object",
        "properties": {
            "code": {
                "description": "Encoded data",
                "type": "array",
                "items": {
                    "type": "number"
                },
             "maxItems": "<collected from the user API>"
            },
            "metadata": {
                "$ref": "#/definitions/metadata"
            }
        },
        "definitions": {
            "metadata": {
                "description": "User defined metadata",
                "type": "object",
                "properties": {
                    "<collected metadata key1 from the user API>": {
                        "type": "<collected type1 from the user API>"
                    },
                    "<...>": {...}
                },
                "required": ["<collected key1 from the user API>", <...>]
            }
        },
        "required": ["code", "metadata"]
    }
```

> Metadata is organised in such a way to preserve the alphabetical order of keys.



### Schema definition

Above JSON object is auto-generated within Aquila DB (system level) and is the original schema over which CID is generated. Aquila DB should also accept a different JSON schema definition at the API (user level) which is intended to collect all the necessary information from the user to generate the original system level schema. Here is an example schema definition:

```json
{
    "description": "Database description",
    "unique": "random",
    "encoder": "example.com/autoencoder.model",
    "codelen": 300,
    "metadata": {
        "name": "string",
        "age": "number"
    }
}
```

