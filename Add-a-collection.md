## Problem

You want to add a new collection of data to the site.

## Solution

Define the model's schema, construct REST endpoints on the server, and create a Backbone Model and Collection on the client side to interface with the server for the collection.

## Details

Here are the key things you need to add a collection to the website:

1. [[JSON schema file in `/app/schemas/models`|add-a-collection-schema]]. This defines what properties of documents in the collection, and is used by both server and client.
1. [[Mongoose Model in `/server/models`|add-a-mongoose-model]]. This is the server's active record interface with MongoDB for the collection.
1. [[Node/Express REST endpoints in `/server/routes/index.coffee`|add-basic-rest-endpoints-for-a-collection]]. Typically need POST, PUT, GET one and GET many, although each collection's may need more or less.
1. [[Backbone Model and Collection in `/app/models` and `/app/collections`, respectively|connect-backbone-to-new-collection]]. These are the client's active record interface for a document or set of documents in the collection.

See linked recipes for details and examples.

## Resources

* [JSON Schema](http://json-schema.org/)
* [Mongoose](http://mongoosejs.com/docs/guide.html)
* [Express](http://expressjs.com/en/3x/api.html)
* [Backbone](http://backbonejs.org/)