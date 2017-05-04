## Problem

You want to add a new index to MongoDB, so that you can query over that field quickly.

## Solution

Add the index to the server Schema, and then get a CoCo Engineer to add the index to the production MongoDB manually. (Manually adding it ahead of time is preferable to doing it during deploy)

## Details

In `server/models/(your model).schema`, add the index. (Note: Mongoose makes indexes `background: true` by default here)

Eg: ```PrepaidSchema.index({'joiners.userID': 1}, {sparse: true})```


Then, before deploying this code, ask a CodeCombat engineer to add the index. Make sure to add `background: true` to the options here.
```db.prepaids.createIndex({'joiners.userID': 1}, {sparse: true, background: true})```

## Resources

* [MongoDB Index Options](https://docs.mongodb.com/manual/reference/method/db.collection.createIndex/#db.collection.createIndex)