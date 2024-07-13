# nosql-challenge

Welcome to this repository, which showcases the analysis of a database of establishments across the United Kingdom from the UK Food Standards Agency, providing them with a hygiene score. The analysis has three parts, as outlined below:

## Part 1:  Database and Jupyter Notebook Set Up

 1. Imported the data provided in the establishments.json file from your Terminal. Named the database uk_food and the collection establishments. Copied the text used to import the data from your Terminal to a markdown cell in your notebook.
2. Within the notebook, imported the libraries needed: PyMongo and Pretty Print (pprint).
3. Created an instance of the Mongo Client.
4. Confirmed that the database was created and the data was loaded properly:
5. Listed the databases in MongoDB to confirm that uk_food is listed.
6. Listed the collection(s) in the database to ensure that establishments is there.
7. Found and displayed one document in the establishments collection using find_one and displayed it with pprint.
8. Assigned the establishments collection to a variable to prepare it for use.



## Part 2: Update the Database

The magazine editors have requested some modifications to the database before I could perform any queries or analysis for them. Made the following changes to the establishments collection:

1. An exciting new halal restaurant just opened in Greenwich but hasn't been rated yet. The magazine has asked to include it in the analysis. Added the following information to the database:

    {
        "BusinessName": "Penang Flavours",
   
        "BusinessType": "Restaurant/Cafe/Canteen",
   
        "BusinessTypeID": "",
   
        "AddressLine1": "Penang Flavours",
   
        "AddressLine2": "146A Plumstead Rd",
   
        "AddressLine3": "London",
   
        "AddressLine4": "",
   
        "PostCode": "SE18 7DY",
   
        "Phone": "",
   
        "LocalAuthorityCode": "511",
   
        "LocalAuthorityName": "Greenwich",
   
        "LocalAuthorityWebSite": "http://www.royalgreenwich.gov.uk",
   
        "LocalAuthorityEmailAddress": "health@royalgreenwich.gov.uk",
   
        "scores": {
   
            "Hygiene": "",
   
            "Structural": "",
   
            "ConfidenceInManagement": ""
   
        },
   
        "SchemeType": "FHRS",
   
        "geocode": {
            "longitude": "0.08384000",
            "latitude": "51.49014200"
        },
        "RightToReply": "",
        "Distance": 4623.9723280747176,
        "NewRatingPending": true
    }

3. Found the BusinessTypeID for "Restaurant/Cafe/Canteen" and returned only the BusinessTypeID and BusinessType fields.
4. Updated the new restaurant with the BusinessTypeID found.
5. The magazine is not interested in any establishments in Dover, so checked how many documents contain the Dover Local Authority. Then, removed any establishments within the Dover Local Authority from the database and checked the number of documents to ensure they were deleted.
3. Some of the number values are stored as strings when they should be stored as numbers.
    - Used update_many to convert latitude and longitude to decimal numbers.
    - Used update_many to convert RatingValue to integer numbers.

## Part 3: Exploratory Analysis

Eat Safe, Love has specific questions they want answered to help them find the locations they wish to visit and avoid. Used NoSQL_analysis_starter.ipynb for this section of the challenge. 
Some notes to be aware of while exploring the dataset:

    `RatingValue` refers to the overall rating decided by the Food Authority and ranges from 1-5. The higher the value, the better the rating.
        Note: This field also includes non-numeric values such as 'Pass', where 'Pass' means that the establishment passed their inspection but isn't given a number rating. Non-numeric values will be coerced to nulls during the database setup before converting ratings to integers.
    The scores for Hygiene, Structural, and ConfidenceInManagement work in reverse. This means the higher the value, the worse the establishment is in these areas.

Used the following questions to explore the database and find the answers for the magazine editors. 
Unless otherwise stated, for each question:

    Used `count_documents` to display the number of documents contained in the result.
    Displayed the first document in the results using `pprint`.
    Converted the result to a Pandas DataFrame, printed the number of rows in the DataFrame, and displayed the first 10 rows.

1. Which establishments have a hygiene score equal to 20?

2. Which establishments in London have a RatingValue greater than or equal to 4?
    Hint: The London Local Authority has a longer name than "London" so you will need to use $regex as part of your search.

3. What are the top 5 establishments with a RatingValue of 5, sorted by the lowest hygiene score, nearest to the new restaurant added, "Penang Flavours"?
    Hint: You will need to compare the geocode to find the nearest locations. Search within 0.01 degree on either side of the latitude and longitude.
    
4. How many establishments in each Local Authority area have a hygiene score of 0? Sort the results from highest to lowest and print out the top ten local authority areas.
    Hint: You will need to use the aggregation method to answer this.

## References

UK Food Standards Agency (https://www.food.gov.uk/) (2022). UK food hygiene rating data API. https://ratings.food.gov.uk/open-data/en-GB (https://ratings.food.gov.uk/opendata/en-GB) . Contains public sector information licensed under the Open Government Licence v3.0 (https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/)
Accessed Sept 9, 2022 and Sept 12, 2022 with the establishment settings as follows: longitude=51.5072, latitude=-0.1276, maxdistancelimit=4567, pagesize=10000,

Bootcamp Spot. https://bootcampspot.instructure.com/courses/6446/assignments/78956?module_item_id=1248997
