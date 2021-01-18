# Dynamic loading a model

**Authors:  Jubin Jose**



Aquila Hub serves `compressor models` to generate latent vector for an input data. Deep Learning models are really good knowledge compressors - hence the name `"compressor model"`.

 

As seen in Aquila DB [Schema specification](https://github.com/Aquila-Network/specs/blob/main/adb/Schema.md), `"encoder"` key in a `shema definition` specified which model to be loaded and used to compress data for a particular database. 

- An Aquila Hub node should validate CID of the schema definition with corresponding database name. 
- On successful validation, an Aquila Hub node should parse value corresponding to the `"encoder"` key in the schema and validate it. 
- On successful validation, an Aquila Hub node should download `"compressor model"` from the URL and should keep in local storage.
- After ensuring safe storage of the model on disk, an Aquila Hub node should load the model to main memory as a service.

> a `URL` can be `location addressed` or `content addressed`.