---
title: 4. Advanced CRUD Operations
linktitle: 4. Advanced CRUD Operations
toc: true
type: docs
date: "2019-05-05T00:00:00+01:00"
draft: false
menu:
  example:
    parent: MongoDB
    weight: 4

# Prev/next pager order (if `docs_section_pager` enabled in `params.toml`)
weight: 4
---

## Comparision Operators

- $__eq__   - Equal to
- $__ne__   - Not Equal to
- $__gt__   - Greater Than
- $__lt__   - Less Than
- $__gte__  - Greater Than Equal to
- $__lte__  - Less Than Equal to

`{ <field>: { <operator> : <value> }}`
   
Problem: Find all documents where the tripduration was less than or equal to 70 seconds and the usertype was not Subscriber.<br>
`db.trips.find({ "tripduration": { "$lte" : 70 },
                "usertype": { "$ne": "Subscriber" } }).pretty()`


## Logical Operators

- $__and__  - Match all of the specified query clauses.
- $__or__   - Atleast one of the query clauses is matched.
- $__nor__  - Fail to match both given clauses.
- $__not__  - Negate the query requirement.

##### Implicit $and
$and is used as the default operator when an operator is not specified.

        {sector: 'Mobile Food Vendor - 881', result: 'Warning'}

is same as

        {"$and": [
        {sector: 'Mobile Food Vendor - 881'}, 
        {result: 'Warning'}
        ]}

------------------------------------------------------------------------------------------

Connect to database for examples

        use sample_training;

Find trips <= 70 seconds

        db.trips.find( { 
        "tripduration": { "$lte": 70 } 
        } ).pretty();

Find trips <= 70 seconds, user type != "Subscriber"

        db.trips.find( { 
        "tripduration": { "$lte": 70 },
        "usertype": { "$ne": "Subscriber" }
        } ).pretty();

How many documents in the sample_training.zips collection have fewer than 1000 people listed in the pop field?

        db.zips.find( {
        "pop": { "$lt": 1000 }
        } ).count();

What is the difference between the number of people born in 1998 and the number of people born after 1998 in the sample_training.trips collection? (18-12)

        db.trips.find( {
        "birth year": 1998
        } ).count();

        db.trips.find( {
        "birth year": { "$gt": 1998 }
        } ).count();

Find all inspections, that result neither "No Violation Issued" nor "Violation Issued"

        db.inspections.find( {
        "$nor": [ { "result": "No Violation Issued" }, { "result": "Violation Issued" } ]
        } );

$and is implicit and could be omitted


        db.inspections.find( {
        "sector": "Mobile Food Vendor - 881" ,  "result": "Warning"
        } );

same as

        db.inspections.find( {
        "$and": [ {"sector": "Mobile Food Vendor - 881"},  {"result": "Warning"} ]
        } );

Student IDs between (25, 100)

        db.grades.find( {
        "$and": [ {"student_id": { "$gt": 25 }},  {"student_id": { "$lt": 100 }} ]
        } );

one more form

        db.grades.find( {
        "student_id": { "$gt": 25, "$lt": 100 }
        } );

Using explicit $and required when you include same operator more than once (A||B) && (C||D). Find all documents where airplanes CR2 or A81 left or landed in the KZN airpor

        db.routes.find( {
        "$and": [ 
                { "$or": [ { "dst_airport": "KZN" }, { "src_airport": "KZN" } ] },
                { "$or": [{ "airplane": "CR2"}, {"airplane": "A81" }] }
        ]
        } );

How many businesses in the sample_training.inspections dataset have the inspection result "Out of Business" and belong to the "Home Improvement Contractor - 100" sector?

        db.inspections.find( {
        "result": "Out of Business", "sector": "Home Improvement Contractor - 100"
        } ).count();

How many zips in the sample_training.zips dataset are neither over-populated nor under-populated? We consider population of more than 1,000,000 to be over-populated and less than 5,000 to be under-populated

        db.zips.find( {
        "pop": { "$gt": 5000, "$lt": 1000000 }
        } ).count();

How many companies in the sample_training.companies dataset were either founded in 2004, or in the month of October and either have the social category_code or web category_code?

        db.companies.find( {
        "$and": [ 
                { "$or": [ { "founded_year": 2004 }, { "founded_month": 10 } ] },
                { "$or": [{ "category_code": "social"}, {"category_code": "web" }] }
        ]
        } ).count();

How many sample_training.trips have same source and destination station

        db.trips.find( {
        "$expr": { "$eq": ["$start station id", "$end station id"] }
        }).count();

How many of them used bike long enough (> than 1200 seconds)?

        db.trips.find( {
        "$expr": {
                "$and": [
                { "$gt": [ "$tripduration", 1200 ] },
                { "$eq": ["$start station id", "$end station id"] }  
        ]
        }
        }).count();

How many companies in the sample_training.companies collection have the same permalink as their twitter_username?

        db.companies.find( {
        "$expr": { "$eq": ["$permalink", "$twitter_username"] }
        } ).count();

Connect to database for following examples

        use sample_airbnb;

Find all documents in sample_airbnb.listingsAndReviews, where "amenities" contains "Shampoo" value

        db.listingsAndReviews.find( {
        "amenities": { "$all": ["Shampoo"] }
        } ).pretty();

Same results, but with exactly 20 amenities

        db.listingsAndReviews.find( {
        "amenities": { "$size": 20, "$all": ["Shampoo"] }
        } ).count();

What is the name of the listing in the sample_airbnb.listingsAndReviews dataset that accommodates more than 6 people and has exactly 50 reviews?

        db.listingsAndReviews.find( {
        "accommodates": { "$gt": 6 },
        "reviews": { "$size": 50}
        } ).pretty();

Using the sample_airbnb.listingsAndReviews collection find out how many documents have the "property_type" "House", and include "Changing table" as one of the "amenities"?

        db.listingsAndReviews.find( {
        "property_type": "House",
        "amenities": { "$all": ["Changing table"] }
        } ).count();

Find all documents with exactly 20 amenities which include "Shampoo", and display only their price and address

        db.listingsAndReviews.find( {
        "amenities": { "$all": ["Shampoo"] }
        }, {
        "price": 1, "address": 1
        }
        ).pretty();

Same but exclude _id field

        db.listingsAndReviews.find( {
        "amenities": { "$all": ["Shampoo"] }
        }, {
        "price": 1, "address": 1, "_id": 0
        }
        ).pretty();

Connect again

        use sample_training;

Find all documents where the student in class 431 received a grade higher than 85 for any type of assignment (projection prints the field if "$elemMatch" return one )

        db.grades.find( 
        { "class_id": 431 },
        { "scores": { "$elemMatch": { "score": { "$gt": 85 } } } }
        ).pretty();

Find all students who has extra credit

        db.grades.find( 
        { "scores": { "$elemMatch": { "type": "extra credit" } } }
        ).pretty();

How many companies in the sample_training.companies collection have offices in the city of Seattle

        db.companies.find( {
        "offices": { "$elemMatch": { "city": "Seattle" } }
        } ).count();

Example of accessing subdocument - pick one sample_training.trips with start station type "Point"

        db.trips.findOne({ "start station location.type": "Point" });

CEO named "Mark" listed first in sample_training.companies "relationships" array

        db.companies.find( {
        "relationships.0.person.first_name": "Mark",
        "relationships.0.title": { "$regex": "CEO" }
        }, {
        "name": 1
        } ).pretty();

All senior executives named "Mark" and no longer working in the company ("is_past": true)

        db.companies.find( {
        "relationships": { "$elemMatch": { "is_past": true, "person.first_name": "Mark" } }
        }, {
        "name": 1
        } ).pretty();

How many trips in the sample_training.trips collection started at stations that are to the west of the -74 latitude coordinate

        db.trips.find({
        "start station location.coordinates.0": { "$lt": -74.0 }
        }).count();

How many inspections from the sample_training.inspections collection were conducted in the city of NEW YORK?

        db.inspections.find({
        "address.city": "NEW YORK"
        }).count();

How many documents in the sample_training.zips collection have fewer than 1000 people listed in the pop field?

        db.zips.find({
        "address.city": "NEW YORK"
        }).count();