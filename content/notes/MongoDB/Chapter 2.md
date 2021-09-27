---
title: 2. Importing, Exporting, and Querying Data
linktitle: 2. Importing, Exporting, and Querying Data
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  example:
    parent: MongoDB
    weight: 2

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 2
---

### Data Storing
MongoDB can work with JSON or BSON data files, what's the difference?

* MongoDB stores data in BSON, internally and over network
* JSON can natively be stored and retrieved in MongoDB
* BSON provides additional features like speed and flexibility

**JSON**: JavaScript Standard Object Notation.
* Human and Machine Readability
* Start and ends with curly braces {}
* Separate each key and value with a comma, "keys" must be surrounded by quotation marks "" - also called "fields"

**BSON** : Term comes from Binary JSON - Bridges the gap between binary representation and JSON format.
* Machine Only Readability
* Obtimized for: speed, space and flexibility
* High performance and General-purpose focus


--------------------------------------------------------------------------

**Commands:**

* View collections in the active db: `show collections`

* Switch the active db to training: `use training`

* View all available databases: `show dbs`

syntax : `db.{collection}.{query}`

**FIND:** Find the documents with _id: 1

`db.inspections.findOne({ "_id": 1 })`

`db.zips.find({"state": "NY", "city": "ALBANY"}).pretty()` -> returns data in user readable JSON format


--------------------------------------------------------------------------

## Code Instances
Connect to Atlas cluster

        mongo "mongodb+srv://sandbox.v16f0.mongodb.net/admin" --username m001-student

### Export and Import data

Export data in BSON format

        mongodump --uri "mongodb+srv://sandbox.v16f0.mongodb.net/sample_supplies"

Export data in JSON format

        mongodump --uri "mongodb+srv://sandbox.v16f0.mongodb.net/sample_supplies" --collection sales --out sales.json

Import data from BSON dump

        mongorestore --uri "mongodb+srv://sandbox.v16f0.mongodb.net/sample_supplies" --drop dump

Import data from JSON file

        mongoimport --uri "mongodb+srv://sandbox.v16f0.mongodb.net/sample_supplies" --collection sales --drop=sales.json

### Start working with Mongo Shell

Show all databses

        show dbs;

Connect to database (create unless exist)

        use sample_training;

Show database collections

        show collections;

Query all zip codes from NY state (type "it" for iterate through resulting cursor)

        db.zips.find({ "state": "NY" })

How many zip codes in NY state

        db.zips.find({ "state": "NY" }).count()

How many zip codes in NY state AND Albany city

        db.zips.find({ "state": "NY", "city": "ALBANY" }).count()

Format resulting JSON

        db.zips.find({ "state": "NY", "city": "ALBANY" }).pretty()