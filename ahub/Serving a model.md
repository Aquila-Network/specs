# Serving a model

**Authors:  Jubin Jose**



Aquila Hub serves multiple models. It dynamically switches to corresponding model for the database specified in the query.

- An Aquila Hub node should load models from disk on `"compress query"` if not loaded previously (this might happen on failure recovery of a node).
- If a model is not available on disk, it should fail a `"compress query"`.
- A `"Compression Model"` should accept batched inputs for compression.
