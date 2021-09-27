---
title: 1. What is MongoDB
linktitle: 1. What is MongoDB
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  example:
    parent: MongoDB
    weight: 1

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 1
---

### What is MongoDB

* **A database**: structured way to store and access data
* **A NoSQL database**: related tables of data
* **NoSQL documentsDB**: data in MongoDB is stored as documents
* **Stored in Collections**: documents are stored in collection of documents

### MongoDB Atlas
MongoDB Atlas is a fully-managed cloud database developed by the same people that build MongoDB. Atlas handles all the complexity of deploying, managing, and healing your deployments on the cloud service provider of your choice (AWS, Azure, and GCP).

* Atlas: https://cloud.mongodb.com/v2/5fbe56b9cd3fab68c99facc1#clusters
* username: m001-student
* password: m001-mongodb-basics

Atlas users can deploy **clusters** (groups of servers that store your data), configured in **replica sets** ( a few connected MongoDB instances that store the same data)

--------------------------------------------------------------------------

### Code Instances

 Select the database to use.

        use('sample_training');

        db.trips.createIndex({ "start station id": 1, "birth year": 1 })

 Trips starting west of -74 Latitude

        db.trips.find({'start station location.coordinates.0': {'$lt': -74}})

 All Ceos named Mark

        db.companies.find({'relationships.0.person.first_name': 'Mark', 'relationships.0.title': {'$regex': 'CEO'}},
        {'name': 1}).pretty()

 Return names only

        db.companies.find({'funding_rounds': {'$size': 8}},
        {'name': 1, "_id": 0}
        )