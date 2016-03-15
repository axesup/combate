## Problem

You want to explore the dev environment database.

## Solution

Explore the `coco` db with the MongoDB client of your choice.

## Details

Having set up MongoDB on your machine, you should have the command line client set up. To use that:

1. Make sure your db is running. See [Dev Setup](https://github.com/codecombat/codecombat/wiki/Dev-Setup:-General-Information#running-the-environment)
1. Run `mongo` in your terminal. This will start the client, and connect to your local mongodb instance by default.
1. Run `use coco`. This will switch to the dev environment's database.

That's it! You can now use any MongoDB commands. To see what collections there are, run `show collections`. To, for example, display users, run `db.users.find()`.

## Resources

* [Mongo shell commands](https://docs.mongodb.org/manual/reference/method/)