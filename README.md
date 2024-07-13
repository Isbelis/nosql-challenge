# nosql-challenge

Welcome to this repository, which showcases the analysis of a database of establishments across the United Kingdom from the UK Food Standards Agency, providing them with a hygiene score. The analysis has three parts, as outlined below:

## Part 1:  Database and Jupyter Notebook Set Up
1. Imported the data provided in the `establishments.json` file from your Terminal. Named the database `uk_food` and the collection `establishments`. Copied the text used to import the data from your Terminal to a markdown cell in your notebook.
2. Within the notebook, imported the necessary libraries: PyMongo and Pretty Print (`pprint`).
3. Created an instance of the Mongo Client.
4. Confirmed the creation of the database and successful loading of the data:
 - Listed the databases in MongoDB to verify uk_food is listed.
 - Confirmed the presence of the establishments collection in the database.
 - Retrieved and displayed one document from the establishments collection using find_one and printed it with pprint.
5. Assigned the establishments collection to a variable for further use.


## Part 2: Update the Database

The magazine editors requested specific modifications to the database before proceeding with any queries or analysis. The following changes were made to the `establishments` collection:

1. Added predetermined information to the database for an exciting new halal restaurant in Greenwich that hasn't been rated yet.
2. Identified the `BusinessTypeID` for "Restaurant/Cafe/Canteen" and returned only the `BusinessTypeID` and `BusinessType` fields.
3. Updated the new restaurant entry with the found `BusinessTypeID`.
4. Excluded any establishments within the Dover Local Authority from the database, ensuring deletion confirmation.
5. Corrected numeric data stored as strings:
  - Used `update_many` to convert latitude and longitude to decimal numbers.
  - Used `update_many` to convert `RatingValue` to integer numbers.

## Part 3: Exploratory Analysis

Eat Safe, Love has specific questions to guide their visits and avoidances, addressed using `NoSQL_analysis_starter.ipynb` for this section. Key considerations while exploring the dataset include:
- `RatingValue` represents the overall rating assigned by the Food Authority, ranging from 1-5 (higher values indicate better ratings)
    -Note: Non-numeric values such as 'Pass' denote passing inspections without a numeric rating, coerced to nulls during database setup.
- Scores for Hygiene, Structural, and ConfidenceInManagement are inversely related (higher values indicate poorer conditions).

The following questions were explored to provide answers for the magazine editors:
1. Identified establishments with a hygiene score equal to 20.
2. Located establishments in London with a `RatingValue` greater than or equal to 4, using `$regex` for extended matching.
3. Determined the top 5 establishments with a `RatingValue` of 5, sorted by the lowest hygiene score, nearest to the new restaurant "Penang Flavours".
  - Geocode comparison within ±0.01 degree latitude and longitude.
4. Calculated the number of establishments with a hygiene score of 0 in each Local Authority area, sorted in descending order, and presented the top ten.

##  Files 
  - `NoSQL_setup_starter-final.ipynb`: Analysis for part 1 and part 2.
  - `NoSQL_analysis_starter-final.ipynb`: Analsysis for part 3.

    
## References

 - UK Food Standards Agency (https://www.food.gov.uk/) (2022). UK food hygiene rating data API. https://ratings.food.gov.uk/open-data/en-GB (https://ratings.food.gov.uk/opendata/en-GB) . Contains public sector information licensed under the Open Government Licence v3.0 (https://www.nationalarchives.gov.uk/doc/open-government-licence/version/3/)
Accessed Sept 9, 2022 and Sept 12, 2022 with the establishment settings as follows: longitude=51.5072, latitude=-0.1276, maxdistancelimit=4567, pagesize=10000,
 - Bootcamp Spot. https://bootcampspot.instructure.com/courses/6446/assignments/78956?module_item_id=1248997
