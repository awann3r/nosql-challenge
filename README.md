# NoSQL Challenge
## Background
For this challenge, I'm acting as a contracted analyst for a food magazine, *Eat Safe, Love*, to evaluate some of the
ratings data conducted by the UK Food Standards. The data analyzed will help journalists and food critics decide where
to focus future articles.

## Challenge Deliverables
Two python scripts 
- `NoSQL_setup.ipynb` -- this will setup and update the database using json file provided
- `NoSQL_analysis.ipynb` -- this will analyze the data from above that's been updated

## Instructions/Requirements
### Part 1 & 2: Jupyter Notebook Set Up and Update the Database
First part will be to import the data provided in `establishments.json`. Create a database named `uk_food` and collection 
`establishments`. Ensure that the data is uploaded properly.

Once confirmed database is ready, add the *Penang Flavours* as a new restaurant:
```
establishments.insert_one(new_restaurant)
```

Update the new restaurant with the `BusinessTypeID`:
```
establishments.update_one(new_restaurant, {'$set': {'BusinessTypeID': 1}})
```

Drop establishments that are in Dover:
```
establishments.delete_many({'LocalAuthorityName':'Dover'})
```

Convert `latitude` and `longitude` to decimal, and `RatingValues` to integer:
```
establishments.update_many({}, [{'$set': {'geocode.longitude': {'$toDecimal': '$geocode.longitude'},
                                'geocode.latitude': {'$toDecimal': '$geocode.latitude'}}}])
 establishments.update_many({}, [{'$set': {'RatingValue': {'$toInt': '$RatingValue'}}}])
 ```

### Part 3: Exploratory Analysis
1. Which establishments have a hygiene score equal to 20?

There are 41 establishments with a hygiene score of 20.

2. Which establishments in London have a RatingValue greater than or equal to 4?

There are 33 establishments with London as the Local Authority and has a RatingValue greater than or equal to 4.

3. What are the top 5 establishments with a RatingValue of 5, sorted by lowest hygiene score, nearest to the new restaurant added, "Penang Flavours"?

 "Volunteer", "Plumstead Manor Nursery", "Atlantic Fish Bar", "Iceland", and "Howe and Co Fish and Chips - Van 17" 

4. How many establishments in each Local Authority area have a hygiene score of 0? Sort the results from highest to lowest?

Number of documents in results: 55. This is a preview of the first 10 rows:
    | _id | count |
    |-----|-------|
    |Thanet|1130|
    |Greenwich|882|
    |Maidstone|713|
    |Newham|711|
    |Swale|686|
    |Chelmsford|680|
    |Medway|672|
    |Bexley|607|
    |Southend-On-Sea|586|
    |Tendring|542|


