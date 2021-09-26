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
Connect to Atlas cluster

        mongo "mongodb+srv://sandbox.v16f0.mongodb.net/admin" --username m001-student

Export and Import data

Export data in BSON format

        mongodump --uri "mongodb+srv://sandbox.v16f0.mongodb.net/sample_supplies"

Export data in JSON format

        mongodump --uri "mongodb+srv://sandbox.v16f0.mongodb.net/sample_supplies" --collection sales --out sales.json

Import data from BSON dump

        mongorestore --uri "mongodb+srv://sandbox.v16f0.mongodb.net/sample_supplies" --drop dump

Import data from JSON file

        mongoimport --uri "mongodb+srv://sandbox.v16f0.mongodb.net/sample_supplies" --collection sales --drop=sales.json

Start working with Mongo Shell

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