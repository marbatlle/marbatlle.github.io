---
title: 5. Indexing and Aggregation Pipeline
linktitle: 5. Indexing and Aggregation Pipeline
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  example:
    parent: MongoDB
    weight: 5

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 5
---

 Connect to database for examples

        use sample_airbnb;

 Find sample_airbnb.listingsAndReviews including Wifi as an aminity, and print only price and address

 MQL approach

        db.listingsAndReviews.find( {
        "amenities": { "$all": ["Wifi"] }
        }, {
        "price": 1, "address": 1, "_id": 0
        }
        ).pretty();

 Aggregation approach

        db.listingsAndReviews.aggregate([
        { "$match": {"amenities": "Wifi" } },
        { "$project": {"price": 1, "address": 1, "_id": 0} }
        ]);

 Aggregate by countries (list all countries present)

        db.listingsAndReviews.aggregate([
        { "$project": { "address": 1, "_id": 0 } },
        { "$group": { "_id": "$address.country" } }
        ]);

 Take previous aggregation and add counting all countries

        db.listingsAndReviews.aggregate([
        { "$project": { "address": 1, "_id": 0 } },
        { "$group": { "_id": "$address.country" } },
        { "count": { "$sum": 1 } }
        ]);

 What room types are present in the sample_airbnb.listingsAndReviews collection?

        db.listingsAndReviews.aggregate([
        { "$project": { "room_type": 1, "_id": 0 } },
        { "$group": { "_id": "$room_type" } }
        ]);

 Change database

        use sample_training;

 Get least populated city in sample_training.zips

        db.zips.find().sort({ "pop": 1 }).limit(1).pretty();

 Get 10 most populated now

        db.zips.find().sort({ "pop": -1 }).limit(10).pretty();

 Sort it in increasing order by population, and then in decreasing by city name

        db.zips.find().sort({ "pop": 1, "city": -1 }).limit(10).pretty();

 Return the name and founding year for the 5 oldest companies in the sample_training.companies collection?

        db.companies.find({ 
        "founded_year": { "$ne": null } 
        }, { 
        "name": 1, "founded_year": 1 
        } ).sort({ "founded_year": 1 }).limit(5);

 In what year was the youngest bike rider from the sample_training.trips collection born?

        db.trips.find({ 
        "$and": [{ "birth year": {"$ne": ""} }, { "birth year": {"$ne": null}}]
        }, { 
        "birth year": 1 
        } ).sort({ "birth year": -1 }).limit(1);

 Create index by field

        db.trips.createIndex({ "birth year": 1 })

 Create compound index

        db.trips.createIndex({ "start station id": 476, "birth year": 1 })