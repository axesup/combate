## Problem

You want to define how a collection of data is structured.

## Solution

Add a JSON schema file to `/app/schemas/models`.

## Details

We use JSON schema both on the client and on the server to enforce data integrity, document intended structure, validate forms, and generate some interfaces. Though the file is located in `/app`, the server will also load the file and should use it whenever changes are made to a document. These are not hard and fast schemas, though, there is nothing preventing the server logic from making changes without checking the schema, or changing the schema in such a way that existing data becomes 'invalid'.

Make sure to read through the [JSON Schema website](http://json-schema.org/) for how schemas are structured, in particular the [JSON Schema Validation Specification](http://json-schema.org/latest/json-schema-validation.html).

We us a [schemas module](https://github.com/codecombat/codecombat/blob/master/app/schemas/schemas.coffee) to generate many of our schemas, rather than write them all from scratch.