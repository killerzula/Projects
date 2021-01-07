# Data Scientist Role Play: Profiling and Analyzing the Yelp Dataset Coursera Worksheet

This is a 2-part assignment. In the first part, you are asked a series of questions that will help you profile and understand the data just like a data scientist would. For this first part of the assignment, you will be assessed both on the correctness of your findings, as well as the code you used to arrive at your answer. You will be graded on how easy your code is to read, so remember to use proper formatting and comments where necessary.

In the second part of the assignment, you are asked to come up with your own inferences and analysis of the data for a particular research question you want to answer. You will be required to prepare the dataset for the analysis you choose to do. As with the first part, you will be graded, in part, on how easy your code is to read, so use proper formatting and comments to illustrate and communicate your intent as required.

For both parts of this assignment, use this "worksheet." It provides all the questions you are being asked, and your job will be to transfer your answers and SQL coding where indicated into this worksheet so that your peers can review your work. You should be able to use any Text Editor (Windows Notepad, Apple TextEdit, Notepad ++, Sublime Text, etc.) to copy and paste your answers. If you are going to use Word or some other page layout application, just be careful to make sure your answers and code are lined appropriately.
In this case, you may want to save as a PDF to ensure your formatting remains intact for you reviewer.



## Part 1: Yelp Dataset Profiling and Understanding

1. Profile the data by finding the total number of records for each of the tables below:
	
	i. Attribute table = 10000

	ii. Business table = 10000

	iii. Category table = 10000

	iv. Checkin table = 10000

	v. elite_years table = 10000

	vi. friend table = 10000

	vii. hours table = 10000

	viii. photo table = 10000

	ix. review table = 10000

	x. tip table = 10000

	xi. user table = 10000
	


2. Find the total distinct records by either the foreign key or primary key for each table. If two foreign keys are listed in the table, please specify which foreign key.


	i.	Business = id: 10000

	ii. 	Hours = business_id: 1562

	iii. 	Category = business_id: 2643

	iv. 	Attribute = business_id: 1115

	v. 	Review = id:10000, business_id: 8090, user_id: 9581

	vi. 	Checkin = business_id: 493

	vii. 	Photo = id: 10000, business_id: 6493

	viii. 	Tip = user_id: 537, business_id: 3979

	ix. 	User = id: 10000

	x. 	Friend = user_id: 11

	xi. 	Elite_years = user_id: 2780

Note: Primary Keys are denoted in the ER-Diagram with a yellow key icon.	



3. Are there any columns with null values in the Users table? Indicate "yes," or "no."

	Answer: 
	```
	No
	```
	
	SQL code used to arrive at answer:
	```sql
	SELECT COUNT(*)
	FROM user
	WHERE id IS NULL OR 
		name IS NULL OR 
		review_count IS NULL OR 
		yelping_since IS NULL OR
		useful IS NULL OR 
		funny IS NULL OR 
		cool IS NULL OR 
		fans IS NULL OR 
		average_stars IS NULL OR 
		compliment_hot IS NULL OR 
		compliment_more IS NULL OR 
		compliment_profile IS NULL OR 
		compliment_cute IS NULL OR 
		compliment_list IS NULL OR 
		compliment_note IS NULL OR 
		compliment_plain IS NULL OR 
		compliment_cool IS NULL OR 
		compliment_funny IS NULL OR 
		compliment_writer IS NULL OR 
		compliment_photos IS NULL 
	```

	
4. For each table and column listed below, display the smallest (minimum), largest (maximum), and average (mean) value for the following fields:

	i. Table: Review, Column: Stars
	
		min: 1		max: 5		avg: 3.7082
		
	
	ii. Table: Business, Column: Stars
	
		min: 1 	max: 5		avg: 3.6549
		
	
	iii. Table: Tip, Column: Likes
	
		min: 0		max: 2		avg: 0.0144
		
	
	iv. Table: Checkin, Column: Count
	
		min: 1		max: 53		avg: 1.9414
		
	
	v. Table: User, Column: Review_count
	
		min: 0		max: 2000	avg: 24.2995
		


5. List the cities with the most reviews in descending order:

	SQL code used to arrive at answer:
	```sql
	SELECT city,
	   SUM(review_count) AS reviews
	FROM business
	GROUP BY city
	ORDER BY reviews DESC
	```
	Copy and Paste the Result Below:
	```
	+-----------------+---------+
	| city            | reviews |
	+-----------------+---------+
	| Las Vegas       |   82854 |
	| Phoenix         |   34503 |
	| Toronto         |   24113 |
	| Scottsdale      |   20614 |
	| Charlotte       |   12523 |
	| Henderson       |   10871 |
	| Tempe           |   10504 |
	| Pittsburgh      |    9798 |
	| Montréal        |    9448 |
	| Chandler        |    8112 |
	| Mesa            |    6875 |
	| Gilbert         |    6380 |
	| Cleveland       |    5593 |
	| Madison         |    5265 |
	| Glendale        |    4406 |
	| Mississauga     |    3814 |
	| Edinburgh       |    2792 |
	| Peoria          |    2624 |
	| North Las Vegas |    2438 |
	| Markham         |    2352 |
	| Champaign       |    2029 |
	| Stuttgart       |    1849 |
	| Surprise        |    1520 |
	| Lakewood        |    1465 |
	| Goodyear        |    1155 |
	+-----------------+---------+
	```
	
6. Find the distribution of star ratings to the business in the following cities:

	i. Avon
	
	SQL code used to arrive at answer:
		
		```sql
		SELECT stars,
			   SUM(review_count) AS count
		FROM business
		WHERE city == 'Avon'
		GROUP BY stars		
		```
		
		Copy and Paste the Resulting Table Below (2 columns - star rating and count):
```	
+-------+-------+
| stars | count |
+-------+-------+
|   1.5 |    10 |
|   2.5 |     6 |
|   3.5 |    88 |
|   4.0 |    21 |
|   4.5 |    31 |
|   5.0 |     3 |
+-------+-------+	
```	
	
	ii. Beachwood

		SQL code used to arrive at answer:
```sql	
SELECT stars,
	   SUM(review_count) AS count
FROM business
WHERE city == 'Beachwood'
GROUP BY stars
```
		Copy and Paste the Resulting Table Below (2 columns - star rating and count):
```sql
+-------+-------+
| stars | count |
+-------+-------+
|   2.0 |     8 |
|   2.5 |     3 |
|   3.0 |    11 |
|   3.5 |     6 |
|   4.0 |    69 |
|   4.5 |    17 |
|   5.0 |    23 |
+-------+-------+
```

7. Find the top 3 users based on their total number of reviews:
	
	SQL code used to arrive at answer:
```sql
SELECT id,
	   name,
	   review_count
FROM user
ORDER BY review_count DESC
LIMIT 3
```
		
	Copy and Paste the Result Below:
```	
+------------------------+--------+--------------+
| id                     | name   | review_count |
+------------------------+--------+--------------+
| -G7Zkl1wIWBBmD0KRy_sCw | Gerald |         2000 |
| -3s52C4zL_DHRK0ULG6qtg | Sara   |         1629 |
| -8lbUNlXVSoXqaRRiHiSNg | Yuri   |         1339 |
+------------------------+--------+--------------+
```
8. Does posing more reviews correlate with more fans?
```sql
SELECT id,
	   name,
	   review_count,
	   fans,
	   yelping_since
FROM user
ORDER BY fans + review_count DESC
```
	Please explain your findings and interpretation of the results:
		To a certain extent, posing more reviews doescorrelate with more fans. However, it is important to notice that the time spent yelping is also a confounding variable in the current scenario. The longer a user has been yelping the more reviews they would have posted and the more people they have associated with and hence acquired more fans.

	
9. Are there more reviews with the word "love" or with the word "hate" in them?

	Answer:
	```
		There are more reviews with the word 'love'
	```
	SQL code used to arrive at answer:
```sql
SELECT count(text)
FROM review
where text like '%love%'
	--1780
```
```sql
SELECT count(text)		
FROM review
where text like '%hate'
	--232
```	
	
10. Find the top 10 users with the most fans:

	SQL code used to arrive at answer:
		SELECT id, name, fans
		FROM user
		ORDER BY FANS DESC
		LIMIT 10		
	
	Copy and Paste the Result Below:
		+------------------------+-----------+------+
		| id                     | name      | fans |
		+------------------------+-----------+------+
		| -9I98YbNQnLdAmcYfb324Q | Amy       |  503 |
		| -8EnCioUmDygAbsYZmTeRQ | Mimi      |  497 |
		| --2vR0DIsmQ6WfcSzKWigw | Harald    |  311 |
		| -G7Zkl1wIWBBmD0KRy_sCw | Gerald    |  253 |
		| -0IiMAZI2SsQ7VmyzJjokQ | Christine |  173 |
		| -g3XIcCb2b-BD0QBCcq2Sw | Lisa      |  159 |
		| -9bbDysuiWeo2VShFJJtcw | Cat       |  133 |
		| -FZBTkAZEXoP7CYvRV2ZwQ | William   |  126 |
		| -9da1xk7zgnnfO1uTVYGkA | Fran      |  124 |
		| -lh59ko3dxChBSZ9U7LfUw | Lissa     |  120 |
		+------------------------+-----------+------+
	
		

Part 2: Inferences and Analysis

1. Pick one city and category of your choice and group the businesses in that city or category by their overall star rating. Compare the businesses with 2-3 stars to the businesses with 4-5 stars and answer the following questions. Include your code.
	City: Las Vegas
	Business: Shopping
	
i. Do the two groups you chose to analyze have a different distribution of hours?
	From the output it can be observed that the two groups have different distribution of hours. The 4-5 stars businesses seem to have shorter hours however, only three businesses are returned by the query. Therefore this observation may not be conclusive given the small sample size.

ii. Do the two groups you chose to analyze have a different number of reviews?
    Once again, the number of reviews are different for one business named 'Red Rock Canyon Visitor Center'. However this may simply be an outlier, as the other 4-5 star business 'Desert Medical Equipment' has almost equal number of reviews to the 2-3 stars business.
         
iii. Are you able to infer anything from the location data provided between these two groups? Explain.
	From the postal address all the locations seem to be different as such nothing can be inferred from the location data.


SQL code used for analysis:
	SELECT 
		B.name
		,CASE
			WHEN B.stars BETWEEN 2 AND 3 THEN '2-3 stars'
			WHEN B.stars BETWEEN 4 AND 5 THEN '4-5 stars'
		END AS star_rating
		,H.hours
		,B.review_count
		,address
		,CASE
			WHEN hours LIKE "%monday%" THEN 1
			WHEN hours LIKE "%tuesday%" THEN 2
			WHEN hours LIKE "%wednesday%" THEN 3
			WHEN hours LIKE "%thursday%" THEN 4
			WHEN hours LIKE "%friday%" THEN 5
			WHEN hours LIKE "%saturday%" THEN 6
			WHEN hours LIKE "%sunday%" THEN 7
		END AS cat
	FROM business B 
	
	INNER JOIN hours H
	ON B.id = H.business_id
	
	INNER JOIN category C
	ON C.business_id = B.id
	
	WHERE (B.city == 'Las Vegas'
	AND
	C.category LIKE 'shopping')
	AND
	(B.stars BETWEEN 2 AND 3
	OR
	B.stars BETWEEN 4 AND 5)
	
	GROUP BY stars,cat
	ORDER BY cat,star_rating ASC
		

OUTPUT:
	+--------------------------------+-------------+----------------------+--------------+------------------------+-----+
	| name                           | star_rating | hours                | review_count | address                | cat |
	+--------------------------------+-------------+----------------------+--------------+------------------------+-----+
	| Walgreens                      | 2-3 stars   | Monday|8:00-22:00    |            6 | 3808 E Tropicana Ave   |   1 |
	| Red Rock Canyon Visitor Center | 4-5 stars   | Monday|8:00-16:30    |           32 | 1000 Scenic Loop Dr    |   1 |
	| Desert Medical Equipment       | 4-5 stars   | Monday|8:00-17:00    |            4 | 3555 W Reno Ave, Ste F |   1 |
	| Walgreens                      | 2-3 stars   | Tuesday|8:00-22:00   |            6 | 3808 E Tropicana Ave   |   2 |
	| Red Rock Canyon Visitor Center | 4-5 stars   | Tuesday|8:00-16:30   |           32 | 1000 Scenic Loop Dr    |   2 |
	| Desert Medical Equipment       | 4-5 stars   | Tuesday|8:00-17:00   |            4 | 3555 W Reno Ave, Ste F |   2 |
	| Walgreens                      | 2-3 stars   | Wednesday|8:00-22:00 |            6 | 3808 E Tropicana Ave   |   3 |
	| Red Rock Canyon Visitor Center | 4-5 stars   | Wednesday|8:00-16:30 |           32 | 1000 Scenic Loop Dr    |   3 |
	| Desert Medical Equipment       | 4-5 stars   | Wednesday|8:00-17:00 |            4 | 3555 W Reno Ave, Ste F |   3 |
	| Walgreens                      | 2-3 stars   | Thursday|8:00-22:00  |            6 | 3808 E Tropicana Ave   |   4 |
	| Red Rock Canyon Visitor Center | 4-5 stars   | Thursday|8:00-16:30  |           32 | 1000 Scenic Loop Dr    |   4 |
	| Desert Medical Equipment       | 4-5 stars   | Thursday|8:00-17:00  |            4 | 3555 W Reno Ave, Ste F |   4 |
	| Walgreens                      | 2-3 stars   | Friday|8:00-22:00    |            6 | 3808 E Tropicana Ave   |   5 |
	| Red Rock Canyon Visitor Center | 4-5 stars   | Friday|8:00-16:30    |           32 | 1000 Scenic Loop Dr    |   5 |
	| Desert Medical Equipment       | 4-5 stars   | Friday|8:00-17:00    |            4 | 3555 W Reno Ave, Ste F |   5 |
	| Walgreens                      | 2-3 stars   | Saturday|8:00-22:00  |            6 | 3808 E Tropicana Ave   |   6 |
	| Red Rock Canyon Visitor Center | 4-5 stars   | Saturday|8:00-16:30  |           32 | 1000 Scenic Loop Dr    |   6 |
	| Walgreens                      | 2-3 stars   | Sunday|8:00-22:00    |            6 | 3808 E Tropicana Ave   |   7 |
	| Red Rock Canyon Visitor Center | 4-5 stars   | Sunday|8:00-16:30    |           32 | 1000 Scenic Loop Dr    |   7 |
	+--------------------------------+-------------+----------------------+--------------+------------------------+-----+	

2. Group business based on the ones that are open and the ones that are closed. What differences can you find between the ones that are still open and the ones that are closed? List at least two differences and the SQL code you used to arrive at your answer.
		
i. Difference 1:
	The businesses that are open tend to have more reviews than ones that
	are closed on average.
	
		Open:   AVG(review_count) = 31.757
		Closed: AVG(review_count0 = 23.198

         
ii. Difference 2:
	The average star rating is higher for businesses that are open than
	businesses that are closed.

		Open:   AVG(stars) = 3.679
		Closed: AVG(stars) = 3.520

SQL code used for analysis:
	SELECT COUNT(DISTINCT(id)),
		   AVG(review_count),
		   SUM(review_count),
		   AVG(stars),
		   is_open
	FROM business
	GROUP BY is_open
	
	
3. For this last part of your analysis, you are going to choose the type of analysis you want to conduct on the Yelp dataset and are going to prepare the data for analysis.

Ideas for analysis include: Parsing out keywords and business attributes for sentiment analysis, clustering businesses to find commonalities or anomalies between them, predicting the overall star rating for a business, predicting the number of fans a user will have, and so on. These are just a few examples to get you started, so feel free to be creative and come up with your own problem you want to solve. Provide answers, in-line, to all of the following:
	
i. Indicate the type of analysis you chose to do:
	I would like to do a predictive analysis on whether the business will stay ongoing or will it close in the near future based on the data provided by the yelp database such as location, category, reviews, and ratings. I would also like to analyze whether some variables are more important than others when it comes to decide the success or failure of an ongoing business.
         
ii. Write 1-2 brief paragraphs on the type of data you will need for your analysis and why you chose that data:
	For this analysis I would need the id, name, location, hours distribution, reviews, stars, category and other attributes assigned to the business. This sort of predictive analysis would help us analyze which factors matter the most when it comes to user satisfaction and will also help businesses improve the quality of their services.
                  
iii. Output of your finished dataset:
	+------------------------+--------------------------------+-----------------------------+-------+---------------+-------+-------------+--------------+--------------+---------------+-----------------+----------------+--------------+----------------+--------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------+
	| id                     | name                           | address                     | state | city          | stars | postal_code | review_count | hours_monday | hours_tuesday | hours_wednesday | hours_thursday | hours_friday | hours_saturday | hours_sunday | categories                                                                                                                                                                                                 | attributes                                                                                                                                                                                                                                                                                                                          | is_open |
	+------------------------+--------------------------------+-----------------------------+-------+---------------+-------+-------------+--------------+--------------+---------------+-----------------+----------------+--------------+----------------+--------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------+
	| -0DET7VdEQOJVJ_v6klEug | Flaming Kitchen                | 3235 York Regional Road 7   | ON    | Markham       |   3.0 | L3R 3P9     |           25 | 12:00-23:00  | 12:00-23:00   | 12:00-23:00     | 12:00-23:00    | 12:00-23:00  | 12:00-23:00    | 12:00-23:00  | Asian Fusion,Restaurants                                                                                                                                                                                   | RestaurantsTableService,GoodForMeal,Alcohol,Caters,HasTV,RestaurantsGoodForGroups,NoiseLevel,WiFi,RestaurantsAttire,RestaurantsReservations,OutdoorSeating,RestaurantsPriceRange2,BikeParking,RestaurantsDelivery,Ambience,RestaurantsTakeOut,GoodForKids,BusinessParking                                                           |       1 |
	| -2HjuT4yjLZ3b5f_abD87Q | Freeman's Car Stereo           | 4821 South Blvd             | NC    | Charlotte     |   3.5 | 28217       |            8 | 9:00-19:00   | 9:00-19:00    | 9:00-19:00      | 9:00-19:00     | 9:00-19:00   | 9:00-17:00     | None         | Electronics,Shopping,Automotive,Car Stereo Installation                                                                                                                                                    | BusinessAcceptsCreditCards,RestaurantsPriceRange2,BusinessParking,WheelchairAccessible                                                                                                                                                                                                                                              |       1 |
	| -CdstAUdEvci8GeJG8owpQ | Motors & More                  | 2315 Highland Dr            | NV    | Las Vegas     |   5.0 | 89102       |            7 | 7:00-17:00   | 7:00-17:00    | 7:00-17:00      | 7:00-17:00     | 7:00-17:00   | 8:00-12:00     | None         | Home Services,Solar Installation,Heating & Air Conditioning/HVAC                                                                                                                                           | BusinessAcceptsCreditCards,BusinessAcceptsBitcoin,ByAppointmentOnly                                                                                                                                                                                                                                                                 |       1 |
	| -K4gAv8_vjx8-2BxkVeRkA | Baby Cakes                     | 4145 Erie St                | OH    | Willoughby    |   3.5 | 44094       |            5 | None         | 11:00-17:00   | 11:00-17:00     | 11:00-20:00    | 11:00-17:00  | 10:00-17:00    | None         | Bakeries,Food                                                                                                                                                                                              | BusinessAcceptsCreditCards,RestaurantsTakeOut,WheelchairAccessible,RestaurantsDelivery                                                                                                                                                                                                                                              |       1 |
	| -PtTGvWsckUL8tTutHr6Ew | Snip-its Rocky River           | 21609 Center Ridge Rd       | OH    | Rocky River   |   2.5 | 44116       |           18 | 10:00-19:00  | 10:00-19:00   | 10:00-19:00     | 10:00-19:00    | 10:00-19:00  | 9:00-17:30     | 10:00-16:00  | Beauty & Spas,Hair Salons                                                                                                                                                                                  | BusinessAcceptsCreditCards,RestaurantsPriceRange2,GoodForKids,BusinessParking,ByAppointmentOnly                                                                                                                                                                                                                                     |       1 |
	| -ayZoW_iNDsunYXX_0x1YQ | Standard Restaurant Supply     | 2922 E McDowell Rd          | AZ    | Phoenix       |   3.5 | 85008       |           15 | 8:00-18:00   | 8:00-18:00    | 8:00-18:00      | 8:00-18:00     | 8:00-18:00   | 9:00-17:00     | None         | Shopping,Wholesalers,Restaurant Supplies,Professional Services,Wholesale Stores                                                                                                                            | BusinessAcceptsCreditCards,RestaurantsPriceRange2,BusinessParking,BikeParking,WheelchairAccessible                                                                                                                                                                                                                                  |       1 |
	| -d9qyfNhLMQwVVg_raBKeg | What A Bagel                   | 973 Eglinton Avenue W       | ON    | York          |   3.0 | M6C 2C4     |            8 | 6:00-15:30   | 6:00-15:30    | 6:00-15:30      | 6:00-15:30     | 6:00-15:30   | 6:00-15:30     | None         | Restaurants,Bagels,Breakfast & Brunch,Food                                                                                                                                                                 | NoiseLevel,RestaurantsAttire,RestaurantsTableService,OutdoorSeating                                                                                                                                                                                                                                                                 |       1 |
	| -hjbcaxaU9yYXY2iI-49sw | Pinnacle Fencing Solutions     |                             | AZ    | Phoenix       |   4.0 | 85060       |           13 | 8:00-16:00   | 8:00-16:00    | 8:00-16:00      | 8:00-16:00     | 8:00-16:00   | None           | None         | Home Services,Contractors,Fences & Gates                                                                                                                                                                   | BusinessAcceptsCreditCards,ByAppointmentOnly                                                                                                                                                                                                                                                                                        |       1 |
	| -iu4FxdfxN4rU4Fu9BjiFw | Alterations Express            | 17240 Royalton Rd           | OH    | Strongsville  |   4.0 | 44136       |            3 | 8:00-19:00   | 8:00-19:00    | 8:00-19:00      | 8:00-19:00     | 8:00-19:00   | 8:00-18:00     | None         | Shopping,Bridal,Dry Cleaning & Laundry,Local Services,Sewing & Alterations                                                                                                                                 | BusinessParking,BusinessAcceptsCreditCards,RestaurantsPriceRange2,BusinessAcceptsBitcoin,BikeParking,ByAppointmentOnly,WheelchairAccessible                                                                                                                                                                                         |       1 |
	| -j4NsiRzSMrMk2N_bGH_SA | Extra Space Storage            | 2880 W Elliot Rd            | AZ    | Chandler      |   4.0 | 85224       |            5 | 8:00-17:30   | 8:00-17:30    | 8:00-17:30      | 8:00-17:30     | 8:00-17:30   | 8:00-17:30     | 10:00-14:00  | Home Services,Self Storage,Movers,Shopping,Local Services,Home Decor,Home & Garden                                                                                                                         | BusinessAcceptsCreditCards                                                                                                                                                                                                                                                                                                          |       1 |
	| -uiBBVWI6tMDm2JFbZFrOw | Gussied Up                     | 1090 Bathurst St            | ON    | Toronto       |   4.5 | M5R 1W5     |            6 | None         | 11:00-19:00   | 11:00-19:00     | 11:00-19:00    | 11:00-19:00  | 11:00-17:00    | 12:00-16:00  | Women's Clothing,Shopping,Fashion                                                                                                                                                                          | BusinessAcceptsCreditCards,RestaurantsPriceRange2,BusinessParking,BikeParking                                                                                                                                                                                                                                                       |       1 |
	| 0-aPEeNc2zVb5Gp-i7Ckqg | Buddy's Muffler & Exhaust      | 1509 Hickory Grove Rd       | NC    | Gastonia      |   5.0 | 28056       |            4 | 8:30-17:00   | 8:30-17:00    | 8:30-17:00      | 8:30-17:00     | 8:30-17:00   | 9:00-15:00     | None         | Automotive,Auto Repair                                                                                                                                                                                     | BusinessAcceptsCreditCards                                                                                                                                                                                                                                                                                                          |       1 |
	| 01xXe2m_z048W5gcBFpoJA | Five Guys                      | 2641 N 44th St, Ste 100     | AZ    | Phoenix       |   3.5 | 85008       |           63 | 10:00-22:00  | 10:00-22:00   | 10:00-22:00     | 10:00-22:00    | 10:00-22:00  | 10:00-22:00    | 10:00-22:00  | American (New),Burgers,Fast Food,Restaurants                                                                                                                                                               | RestaurantsTableService,GoodForMeal,Alcohol,Caters,HasTV,RestaurantsGoodForGroups,NoiseLevel,WiFi,RestaurantsAttire,RestaurantsReservations,OutdoorSeating,BusinessAcceptsCreditCards,RestaurantsPriceRange2,BikeParking,RestaurantsDelivery,Ambience,RestaurantsTakeOut,GoodForKids,DriveThru,BusinessParking                      |       1 |
	| 06I2r8S3tHP_LwGnnkk6Uw | All Storage - Anthem           | 2620 W Horizon Ridge Pkwy   | NV    | Henderson     |   3.5 | 89052       |            3 | 9:00-16:30   | 9:00-16:30    | 9:00-16:30      | 9:00-16:30     | 9:00-16:30   | 9:00-16:30     | None         | Truck Rental,Local Services,Self Storage,Parking,Automotive                                                                                                                                                | BusinessAcceptsCreditCards,BusinessAcceptsBitcoin                                                                                                                                                                                                                                                                                   |       1 |
	| 07h3mGtTovPJE660nX6E-A | Mood                           | 1 Greenside Place           | EDH   | Edinburgh     |   2.0 | EH1 3AA     |           11 | None         | None          | None            | 22:30-3:00     | 22:00-3:00   | 22:00-3:00     | 22:30-3:00   | Dance Clubs,Nightlife                                                                                                                                                                                      | Alcohol,OutdoorSeating,BusinessAcceptsCreditCards,RestaurantsPriceRange2,AgesAllowed,Music,Smoking,RestaurantsGoodForGroups,WheelchairAccessible                                                                                                                                                                                    |       0 |
	| 0AJF-USLN6K5T4caooDdjw | Starbucks                      | 4605 E Chandler Blvd, Ste A | AZ    | Phoenix       |   3.0 | 85048       |           52 | 5:00-20:00   | 5:00-20:00    | 5:00-20:00      | 5:00-20:30     | 5:00-20:00   | 5:00-20:00     | 5:00-20:00   | Coffee & Tea,Food                                                                                                                                                                                          | BusinessParking,Caters,WiFi,OutdoorSeating,BusinessAcceptsCreditCards,RestaurantsPriceRange2,BikeParking,RestaurantsTakeOut                                                                                                                                                                                                         |       1 |
	| 0B3W6KxkD3o4W4l6cq735w | Big Smoke Burger               | 260 Yonge Street            | ON    | Toronto       |   3.0 | M4B 2L9     |           47 | 10:30-21:00  | 10:30-21:00   | 10:30-21:00     | 10:30-21:00    | 10:30-21:00  | 10:30-21:00    | 11:00-19:00  | Poutineries,Burgers,Restaurants                                                                                                                                                                            | RestaurantsTableService,GoodForMeal,Alcohol,Caters,HasTV,RestaurantsGoodForGroups,NoiseLevel,WiFi,RestaurantsAttire,RestaurantsReservations,OutdoorSeating,BusinessAcceptsCreditCards,RestaurantsPriceRange2,WheelchairAccessible,BikeParking,RestaurantsDelivery,Ambience,RestaurantsTakeOut,GoodForKids,DriveThru,BusinessParking |       1 |
	| 0IySwcfqwJjpHPsYwjpAkg | Subway                         | 2904 Yorkmont Rd            | NC    | Charlotte     |   3.5 | 28208       |            7 | 6:00-22:00   | 6:00-22:00    | 6:00-22:00      | 6:00-22:00     | 6:00-22:00   | 10:00-21:00    | None         | Fast Food,Restaurants,Sandwiches                                                                                                                                                                           | Ambience,RestaurantsPriceRange2,GoodForKids                                                                                                                                                                                                                                                                                         |       1 |
	| 0K2rKvqdBmiOAUTebcUohQ | Red Rock Canyon Visitor Center | 1000 Scenic Loop Dr         | NV    | Las Vegas     |   4.5 | 89161       |           32 | 8:00-16:30   | 8:00-16:30    | 8:00-16:30      | 8:00-16:30     | 8:00-16:30   | 8:00-16:30     | 8:00-16:30   | Education,Visitor Centers,Professional Services,Special Education,Local Services,Community Service/Non-Profit,Hotels & Travel,Travel Services,Gift Shops,Shopping,Parks,Hiking,Flowers & Gifts,Active Life | BusinessAcceptsCreditCards,GoodForKids                                                                                                                                                                                                                                                                                              |       1 |
	| 0Ni7Stqt4RFWDGjOYRi2Bw | Scent From Above Company       | 2501 W Behrend Dr, Ste 67   | AZ    | Scottsdale    |   4.5 | 85027       |           14 | 6:00-16:00   | 6:00-16:00    | 6:00-16:00      | 6:00-16:00     | 6:00-16:00   | None           | None         | Home Cleaning,Local Services,Professional Services,Carpet Cleaning,Home Services,Office Cleaning,Window Washing                                                                                            | BusinessAcceptsCreditCards,ByAppointmentOnly                                                                                                                                                                                                                                                                                        |       1 |
	| 0WBMEfqXQnEOAIkV-uCW6w | The Charlotte Room             | 19 Charlotte Street         | ON    | Toronto       |   3.5 | M5V 2H5     |           10 | 15:00-1:00   | 15:00-1:00    | 15:00-1:00      | 15:00-1:00     | 15:00-2:00   | 18:00-2:00     | None         | Event Planning & Services,Bars,Nightlife,Lounges,Pool Halls,Venues & Event Spaces                                                                                                                          | BusinessParking,HasTV,CoatCheck,NoiseLevel,OutdoorSeating,BusinessAcceptsCreditCards,RestaurantsPriceRange2,Music,WheelchairAccessible,Smoking,Ambience,BestNights,RestaurantsGoodForGroups,HappyHour,GoodForDancing,Alcohol                                                                                                        |       0 |
	| 0Y3lHyqRHfWOBuQlS1bM0g | PC Savants                     | 11966 W Candelaria Ct       | AZ    | Sun City      |   5.0 | 85373       |           11 | 10:00-19:00  | 10:00-19:00   | 10:00-19:00     | 10:00-19:00    | 10:00-19:00  | 11:00-18:00    | 11:00-18:00  | IT Services & Computer Repair,Electronics Repair,Local Services,Mobile Phone Repair                                                                                                                        | BusinessAcceptsCreditCards,BusinessAcceptsBitcoin                                                                                                                                                                                                                                                                                   |       1 |
	| 0aKsGxx7XP2TMs_fn_9xVw | Sweet Ruby Jane Confections    | 8975 S Eastern Ave, Ste 3-B | NV    | Las Vegas     |   4.0 | 89123       |           30 | 10:00-19:00  | 10:00-19:00   | 10:00-19:00     | 10:00-19:00    | 10:00-19:00  | 10:00-19:00    | None         | Food,Chocolatiers & Shops,Bakeries,Specialty Food,Desserts                                                                                                                                                 | BusinessAcceptsCreditCards,RestaurantsPriceRange2,BusinessParking,WheelchairAccessible                                                                                                                                                                                                                                              |       0 |
	| 0cxO1Lx2Pi7u6ftWX3Wksg | Oinky's Pork Chop Heaven       | 22483 Emery Rd              | OH    | North Randall |   3.0 | 44128       |            3 | 6:00-23:00   | 6:00-23:00    | 6:00-23:00      | 6:00-23:00     | 6:00-23:00   | 6:00-23:00     | 6:00-23:00   | Soul Food,Restaurants                                                                                                                                                                                      | RestaurantsAttire,RestaurantsGoodForGroups,GoodForKids,RestaurantsReservations,RestaurantsTakeOut                                                                                                                                                                                                                                   |       1 |
	| 0e-j5VcEn54EZT-FKCUZdw | Sushi Osaka                    | 5084 Dundas Street W        | ON    | Toronto       |   4.5 | M9A 1C2     |            8 | 11:00-23:00  | 11:00-23:00   | 11:00-23:00     | 11:00-23:00    | 11:00-23:00  | 11:00-23:00    | 14:00-23:00  | Sushi Bars,Restaurants,Japanese,Korean                                                                                                                                                                     | RestaurantsTakeOut,WiFi,RestaurantsGoodForGroups,RestaurantsReservations                                                                                                                                                                                                                                                            |       1 |
	+------------------------+--------------------------------+-----------------------------+-------+---------------+-------+-------------+--------------+--------------+---------------+-----------------+----------------+--------------+----------------+--------------+------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------+---------+
	(Output limit exceeded, 25 of 70 total rows shown)
         
iv. Provide the SQL code you used to create your final dataset:
	SELECT B.id
			,B.name
			,B.address
			,B.state
			,B.city
			,B.stars
			,B.postal_code
			,B.review_count
			,MAX(CASE
			WHEN H.hours LIKE "%monday%" THEN TRIM(H.hours,'%MondayTuesWednesThursFriSatSun|%') 
			END) AS hours_monday
			,MAX(CASE
			WHEN H.hours LIKE "%tuesday%" THEN TRIM(H.hours,'%MondayTuesWednesThursFriSatSun|%') 
			END) AS hours_tuesday
			,MAX(CASE
			WHEN H.hours LIKE "%wednesday%" THEN TRIM(H.hours,'%MondayTuesWednesThursFriSatSun|%') 
			END) AS hours_wednesday
			,MAX(CASE
			WHEN H.hours LIKE "%thursday%" THEN TRIM(H.hours,'%MondayTuesWednesThursFriSatSun|%') 
			END) AS hours_thursday
			,MAX(CASE
			WHEN H.hours LIKE "%friday%" THEN TRIM(H.hours,'%MondayTuesWednesThursFriSatSun|%') 
			END) AS hours_friday
			,MAX(CASE
			WHEN H.hours LIKE "%saturday%" THEN TRIM(H.hours,'%MondayTuesWednesThursFriSatSun|%') 
			END) AS hours_saturday
			,MAX(CASE
			WHEN H.hours LIKE "%sunday%" THEN TRIM(H.hours,'%MondayTuesWednesThursFriSatSun|%') 
			END) AS hours_sunday
			,GROUP_CONCAT(DISTINCT(C.category)) AS categories
			,GROUP_CONCAT(DISTINCT(A.name)) AS attributes
			,B.is_open
	FROM business B
	INNER JOIN hours H
	ON B.id = H.business_id
	INNER JOIN category C
	ON B.id = C.business_id
	INNER JOIN attribute A
	ON B.id = A.business_id
	GROUP BY B.id
