# Exploring Establishment Data with NoSQL Analysis

## Overview ##

The UK Food Standards Agency assesses establishments across the United Kingdom, assigning food hygiene ratings to these establishments. This project, undertaken as part of a collaboration with Eat Safe, Love magazine, examines a subset of the ratings data to assist their journalists and food critics in prioritizing future article topics.

---

## Database and Jupyter Notebook Set Up ##

### Process ###

A) Import Dataset:
  1. Import the dataset with:
     - `mongoimport --type json -d uk_food -c establishments --drop --jsonArray establishments.json`
  2. Importation of dependencies (PyMongo and Prettyprint)
  3. Create an instance of MongoClient
  4. Confirm that the new Database was created
  5. Assign the uk_food Database to a variable name
  6. Review the Collections in the new Database
  7. Assign the Collection of interest ('establishments') to a variable, to prepare the collection for use
  8. Review a document in the establishments Collection

---

## Update The Database ##

### Process ###

The magazine editors have some requested modifications for the database before any queries or analysis can be performed for them.

A) An exciting new halal restaurant just opened in Greenwich, but hasn't been rated yet. The magazine wants it included in the analysis:
  1. Create a dictionary for the new restaurant data
  2. Insert the new restaurant into the Collection
  3. Check that the new restaurant was inserted
  4. Find BusinessTypeID for "Restaurant/Cafe/Canteen", return only BusinessTypeID and BusinessType fields
  5. Find Document matching query and project only the specified fields
     - Print result 
  6. Update the new restaurant with the correct BusinessTypeID
  7. Confirm that the new restaurant was updated 

B) The magazine is not interested in any establishments in Dover. Remove any establishments within the Dover Local Authority from the database:
  1. Find how many Documents have LocalAuthorityName as "Dover"
  2. Delete all Documents where LocalAuthorityName is "Dover"
  3. Check if any remaining Documents include Dover
  4. Check that other Documents remain with 'find_one'

C) Some of the number values are stored as strings. These values should be stored as numbers:
  1. Change the data type from string to decimal for Longitude and Latitude
  2. Set Non 1-5 Rating Values To Null
  3. Change the data type from string to integer for RatingValue
  4. Update all Documents in the Collection
  5. Check that the Coordinates and Rating Value are now numbers

---

## Exploratory Analysis ##

### Process ###

Eat Safe, Love has specific questions they want answered, which will help them find the locations they wish to visit and avoid.
   - RatingValue refers to the overall rating decided by the Food Authority and ranges from 1-5.
      - The higher the value, the better the rating.
   - The scores for Hygiene, Structural, and ConfidenceInManagement work in reverse.
      - The higher the value, the worse the establishment is in these areas.

A) Notebook Setup:
  1. Importation of dependencies (PyMongo, Pandas, and Prettyprint)
  2. Create an instance of MongoClient
  3. Assign the uk_food Database to a variable name
  4. Review the Collections in the new Database
  5. Assign the Collection of interest ('establishments') to a variable, to prepare the collection for use

B) Which establishments have a hygiene score equal to 20?
  1. Find the Establishments with a Hygiene score of 20
  2. Use count_documents to display the number of Documents in the result
  3. Display the first Document in the results using pprint
  4. Convert the result to a Pandas DataFrame
  5. Display the number of rows in the DataFrame
  6. Display the first 10 rows of the DataFrame

C) Which establishments in London have a `RatingValue` greater than or equal to 4?
  1. Find Establishments with London as the Local Authority and RatingValue >= 4
  2. Use count_documents to display number of Documents in the result
  3. Display first Document in the results using pprint
  4. Convert the result to a Pandas DataFrame
  5. Display the number of rows in the DataFrame
  6. Display the first 10 rows of the DataFrame

D) What are the top 5 establishments with a `RatingValue` rating value of 5, sorted by lowest hygiene score, nearest to the new restaurant added, "Penang Flavours"?
  1. Set Latitude and Longitude of "Penang Flavours" restaurant 
  2. Construct Latitude and Longitude range for the search
  3. Construct query to find Establishments
  4. Define sort criteria (ascending Hygiene score)
  5. Limit results to top 5 Establishments
  6. Find top 5 Establishments matching the query
  7. Print the results
  8. Convert Result To Pandas DataFrame

E) How many establishments in each Local Authority area have a hygiene score of 0?
  1. Create a pipeline
     - Matches Establishments with Hygiene score of 0
     - Groups matches by Local Authority
     - Sorts matches from highest to lowest
  2. Execute the pipeline
  3. Print print first 10 results
  4. Convert the result to a Pandas DataFrame
  5. Display the number of rows in the DataFrame
  6. Display the first 10 rows of the DataFrame

  
