# Data structures

## Entity

At the core of the DataHub are `datasets`.
Each dataset contains `entities`.
An `entity` is a single data object that has an identifier, properties, and references to other entities.

The JSON data format, along with some special keys, is used when serialising an `entity`.

```json
{
    "id": "a uri identifier",
    "deleted": "flag indicating if the entity is deleted",
    "props": {},
    "refs": {}
}
```

The following is an example `entity`:

```json
{
    "id": "http://data.mimiro.io/people/homer",
    "deleted": "false",
    "props": {
        "http://data.mimiro.io/schema/person/fullname": "homer simpson"
    },
    "refs": {
        "http://data.mimiro.io/schema/person/worksfor": "http://data.mimiro.io/companies/mimiro",
        "http://www.w3.org/1999/02/22-rdf-syntax-ns#type": "http://data.mimiro.io/schema/person"
    }
}
```

Note the use of URIs for property names and entity identifiers.
Entities are mostly returned from the DataHub in an array.

## Context

To make the payload more concise, a context can be added as the first JSON object.
The context defines URI prefixes and corresponding expansions.

```json
[
    {
        "id": "@context",
        "namespaces": {
            "schema": "http://data.mimiro.io/schema/",
            "rdf": "http://www.w3.org/1999/02/22-rdf-syntax-ns#",
            "person": "http://data.mimiro.io/schema/person/",
            "people": "http://data.mimiro.io/people/",
            "companies": "http://data.mimiro.io/companies/"
        }
    },

    {
        "id": "people:homer",
        "deleted": "false",
        "props": {
            "person:fullname": "Homer Simpson"
        },
        "refs": {
            "person:worksfor": "companies:mimiro",
            "rdf:type": "schema:person"
        }
    }
]
```

## Continuation Tokens

DataHub may return partial datasets. In this case payloads end with a `continuation token` as last array entry.
Continuation tokens point to the next entity, and can be used to page through larger datasets.

```json
[
    {
        "id": "http://data.mimiro.io/people/homer",
        "deleted": "false",
        "props": {
            "http://data.mimiro.io/schema/person/fullname": "homer simpson"
        },
        "refs": {}
    },
    {
        "id": "@continuation",
        "token": "ef25a4"
    }
]
```

Refer to the entity graph datamodel section of the
[UDA specification](https://open.mimiro.io/specifications/uda/latest.html#the-entity-graph-data-model)
for more details on the `props` and `refs` data sections, or the data format in general.
