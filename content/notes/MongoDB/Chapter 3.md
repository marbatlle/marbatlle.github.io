---
title: 3. Creating and Manipulating Documents
linktitle: 3. Creating and Manipulating Documents
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  example:
    parent: MongoDB
    weight: 3

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 3
---
--------------------------------------------------------------------------

**INSERT:**

Insert three test documents:

`db.inspections.insert([ { "test": 1 }, { "test": 2 }, { "test": 3 } ])`

Insert three test documents but specify the _id values:

`db.inspections.insert([{ "_id": 1, "test": 1 },{ "_id": 1, "test": 2 }, { "_id": 3, "test": 3 }])`

Insert multiple documents specifying the _id values, and using the "ordered": false option.

`db.inspections.insert([{ "_id": 1, "test": 1 },{ "_id": 1, "test": 2 }, { "_id": 3, "test": 3 }],{ "ordered": false })`

Insert multiple documents with _id: 1 with the default "ordered": true setting

`db.inspection.insert([{ "_id": 1, "test": 1 },{ "_id": 3, "test": 3 }])`

**UPDATE:**

Update all documents in the zips collection where the city field is equal to "HUDSON" by adding 10 to the current value of the "pop" field.

`db.zips.updateMany({ "city": "HUDSON" }, { "$inc": { "pop": 10 } })`

$inc is used to increment the value.

Update a single document in the zips collection where the zip field is equal to "12534" by setting the value of the "pop" field to 17630.

`db.zips.updateOne({ "zip": "12534" }, { "$set": { "pop": 17630 } })`

$set is used to update the value to particular value.

Update a single document in the zips collection where the zip field is equal to "12534" by setting the value of the "popupation" field to 17630.

`db.zips.updateOne({ "zip": "12534" }, { "$set": { "population": 17630 } })`

Update one document in the grades collection where the student_id is 250 *, and the class_id field is 339 , by adding a document element to the "scores" array.

`db.grades.updateOne({ "student_id": 250, "class_id": 339 }, { "$push": { "scores": { "type": "extra credit", "score": 100 } } })`

$push is used to add a new value to already existing object.

**DELETE:**
Delete all the documents that have test field equal to 1.

`db.inspections.deleteMany({ "test": 1 })`

Delete one document that has test field equal to 3.

`db.inspections.deleteOne({ "test": 3 })`

Drop the inspection collection.

`db.inspection.drop()`

--------------------------------------------------------------------------

## Code Instances
Connect to database (create unless exist)

        use sample_training;

Get a random document (for querying an example document or exact ObjectId)

        db.inspections.findOne();

Insert new document (must receive a duplicate error)

        db.inspections.insert({
                "_id" : ObjectId("56d61033a378eccde8a8354f"),
                "id" : "10021-2015-ENFO",
                "certificate_number" : 9278806,
                "business_name" : "ATLIXCO DELI GROCERY INC.",
                "date" : "Feb 20 2015",
                "result" : "No Violation Issued",
                "sector" : "Cigarette Retail Dealer - 127",
                "address" : {
                "city" : "RIDGEWOOD",
                "zip" : 11385,
                "street" : "MENAHAN ST",
                "number" : 1712
                }
        }
        );

Insert new document, removing ObjectId field - success, returns WriteResult({ "nInserted" : 1 })

        db.inspections.insert({
        "id" : "10021-2015-ENFO",
        "certificate_number" : 9278806,
        "business_name" : "ATLIXCO DELI GROCERY INC.",
        "date" : "Feb 20 2015",
        "result" : "No Violation Issued",
        "sector" : "Cigarette Retail Dealer - 127",
        "address" : {
                "city" : "RIDGEWOOD",
                "zip" : 11385,
                "street" : "MENAHAN ST",
                "number" : 1712
        }
        }
        );

Find inserted and source documents (2 documents)

        db.inspections.find( {
        "id": "10021-2015-ENFO"
        } ).pretty();

Insert array of documents - return BulkWriteResult({ "writeErrors" : [ ], "nInserted" : 3...})

        db.inspections.insert( [
        { "test": 1 }, 
        { "test": 2 }, 
        { "test": 2 }
        ] );

Change ObjectId key with int, and generate duplicate key error

First document { "_id": 1, "test": 1 } inserted, but { "_id": 3, "test": 2 } does not

        db.inspections.insert( [
        { "_id": 1, "test": 1 }, 
        { "_id": 1, "test": 2 }, 
        { "_id": 3, "test": 2 }
        ] );

Default insert befavior insert in provided order until error

We can overwrite this behavior by providing property { "ordered": false }
Now { "_id": 3, "test": 2 } inserted despite of 2 duplicate key errors

        db.inspections.insert( [
        { "_id": 1, "test": 1 }, 
        { "_id": 1, "test": 2 }, 
        { "_id": 3, "test": 2 }
        ], { "ordered": false } );

Find the documents with _id: 1

Unlike findOne(), returns the cursor with all documents

        db.inspections.find({ "_id": 1 });
        db.zips.find().pretty();

Get all zip codes from Hudson city

        db.zips.find( {"city": "HUDSON"} ).pretty();

Count == 16

        db.zips.find( {"city": "HUDSON"} ).count();

Update all documents which math the query updateMany(query, action)
This operation makes pop += 10 (population growth 10 people)
It returns update summary { "acknowledged" : true, "matchedCount" : 16, "modifiedCount" : 16 }

        db.zips.updateMany( 
        {"city": "HUDSON"}, 
        { "$inc": {"pop": 10} } 
        );

Check the result

        db.zips.find( {"city": "HUDSON"} ).pretty();

Update only one documents, first which found
Update this record with pop (population) = 17630

Returns { "acknowledged" : true, "matchedCount" : 1, "modifiedCount" : 1 } "$inc" and "$set" allow to update multiple fields

        db.zips.updateOne( 
        { "zip": "12534" }, 
        { "$set": { "pop": 17630 } } 
        );

Find student 250, class 339 for the example

        db.grades.find( {"student_id": 250, "class_id": 339 } ).pretty();

Update it with pushing element to an array updateOne(query, {$push: { arrayName: (element(s)) } } )

        db.grades.updateOne( 
        { "student_id": 250, "class_id": 339 },
        { "$push": {"scores": { "type": "extra credit", "score": 100.00 }} }
        );

Deleting one document - only good for querying by "_id: field
Find test documents created earlier

        db.inspections.find( {"test": 1} );
        db.inspections.find( {"test": 2} );

Delete it

        db.inspections.deleteMany( {"test": 1} );
        db.inspections.deleteMany( {"test": 2} );

This one does not delete, no such document

        db.inspections.deleteMany( {"test": 3} );

db.collection.drop() deletes whole collection

Chapter 3 Assessment
People often confuse New York City as the capital of New York state, when in
reality the capital of New York state is Albany. Add a boolean field "capital?" to all documents pertaining to Albany NY, and New York, NY. The value of the field should be true for all Albany documents
and false for all New York documents.

Update Albany as NY capital

        db.zips.updateMany( 
        { "state": "NY", "city": "ALBANY"}, 
        { "$set": {"capital?": true} } 
        );

Update all other cities in NY as not capital

        db.zips.updateMany( 
        { "state": "NY", "city": { "$not": { "$eq": "ALBANY" } } },
        { "$set": {"capital?": false} } 
        );
