# BUDT 703 DBMS Project - Home Too Realty
> This project focuses on providing Home Too with prospecting and operational business solutions. The new database management system will help customers to save time and find the perfect rental options that fit their requirements. The real estate business involves maintaining a lot of data and involves a lot of information exchange. Out DBMS allows faster search, customer match and deal closure.

## Table of Contents
* [General Info](#general-information)
* [Technologies Used](#technologies-used)
* [Features](#features)
* [Screenshots](#screenshots)
* [Setup](#setup)
* [Usage](#usage)
* [References](#references)




## General Information
- The purpose of the new DBMS is to help Home Too agency keep track of all the prospects’,   customers’, listings’ data and manage the transactions efficiently. This system will help students/users look for properties to rent depending on their needs. This system covers all the functionality related to tenancy management, marketing, managing all the transactional information, legal documents and reports. 
- The scope of the project contains following features:
Offered database management system focused on computerizing and automating the business processes of Home Too
It provides a platform for efficient data management, maintenance and access
It is simple to learn  and includes user friendly graphical interface
It is a networked DBMS, therefore it allows an access to large amount of data (useful for information sharing between realtors)
Allows search requirements to meet the needs of prospective customers
Allows filtering data and sorting depending on a potential client’s requirements




## Technologies Used
- Microsoft SQL Server Management Studio
- Lucidchart


## Features
- The scope of the project contains following features:
- Offered database management system focused on computerizing and automating the business processes of Home Too
- It provides a platform for efficient data management, maintenance and access
- It is simple to learn  and includes user friendly graphical interface
- It is a networked DBMS, therefore it allows an access to large amount of data (useful for information sharing between realtors)
- Allows search requirements to meet the needs of prospective customers
- Allows filtering data and sorting depending on a potential client’s requirements
- Business Description:

- The following describes “Home Too”  organization:

- The real estate agency lists properties for lease and provides the reviews from the previous tenants. Each property may have several reviews or not have at all (if it was recently listed).
- The reviewers (previous or current customers of Home Too) could leave at least one review per property. Each property includes the property details such as unique property ID, square footage, number of bedrooms, number of bathrooms and the availability of parking options. Each property details should list the accessibility features such as the nearest hospital, restaurant, and the nearest metro station.



## Screenshots
![Example screenshot](./img/screenshot.png)
<!-- If you have screenshots you'd like to share, include them here. -->


## Setup
You'll need Microsoft SQL Server Management Studio to make changes to the data or draw outcomes from the given information. All the sql files, presentation and erd are in the same folder as this file. 


## Usage
- I've added a few cases how you can use the data to acquire some particular information.
--What are the cheapest available units in the College Park area?
CREATE VIEW propertyLowestPrice AS(
SELECT propertyId, propertyType, propertyPrice
FROM Property p
WHERE zip IN ('20740')
ORDER BY propertyPrice)

--What are the properties, their zip, review comments, rating and review date
with all the properties more than 3.5 rating. Sort them by date
CREATE VIEW allDetails AS(
SELECT p.propertyId, p. propertyPrice, p.zip, r. reviewComments, r. rating, r. 
reviewDate
FROM Property p, Review r
WHERE p. propertyId = r. reviewPropertyId AND r. rating >= 3.5
ORDER BY r. reviewDate)

-- Which properties have 2 bedrooms and a parking space unavailable?
CREATE VIEW specificProperty AS(
SELECT propertyDetailsId, propertyId, noOfbedrooms, parkingSpaceAvailable
FROM propertyDetails
WHERE noOfbedrooms = 2 AND parkingSpaceAvailable = 'Y'
ORDER BY propertyId)

-- What are the properties that can access to a near metro station
CREATE VIEW metroAccessibility AS(
SELECT a.accessibilityId, a.propertyId
FROM Accessibility a
WHERE a.nearestMetroStation is NOT NULL
ORDER BY accessibilityId)

-- What are the maximum and minimum proce of properties in Zip 20740?
CREATE VIEW minMaxPrice AS(
SELECT p. propertyId, p. propertyPrice, p. propertyType, 'Highest Price' AS MonthlyRent
FROM Property p
WHERE zip IN ('20740') 
	AND  p. propertyType = 'townhouse' 
	AND p.propertyPrice = (
	SELECT MIN (p. propertyPrice)
	FROM Property p)
ORDER BY 1

UNION 
SELECT p. propertyId, p. propertyPrice, p. propertyType, 'Lowest Price' 
FROM Property p
WHERE  zip IN ('20740') 
	AND  p. propertyType = 'townhouse' 
	AND p.propertyPrice = (
	SELECT MAX(p. propertyPrice)
	FROM Property p)
ORDER BY p.propertyPrice ASC)


## References
- https://www.apartments.com/
- https://www.zillow.com/


