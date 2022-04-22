# Amazon_Vine_Analysis
This is a project on Big Data. This involves performing ETL (extract-transform-load) on Amazon product reviews and determine bias.

## Overview of the Analysis
This challenge includes analyzing Amazon reviews written by members of the paid Amazon Vine program. The Amazon Vine program is a service that allows manufacturers and publishers to receive reviews for their products. Companies like SellBy pay a small fee to Amazon and provide products to Amazon Vine members, who are then required to publish a review.

Our dataset includes reviews of furniture. We used PySpark to perform the ETL process to extract the dataset, transform the data, connect to an AWS RDS instance, and load the transformed data into pgAdmin. Next, we used PySpark to determine if there is any bias toward favorable reviews from Vine members in our dataset.

## Resources
- Data Source: [Amazon Review Datasets](https://s3.amazonaws.com/amazon-reviews-pds/tsv/index.txt), [Furniture Dataset](https://s3.amazonaws.com/amazon-reviews-pds/tsv/amazon_reviews_us_Furniture_v1_00.tsv.gz)
- Tools: AWS, Google Colab Notebook, Pyspark, PostgreSQL 12.9, pgAdmin 4

## Analysis and Results
### Analysis - Section 1
Using the cloud ETL process, created an AWS RDS database with tables in pgAdmin, selected a dataset of furniture reviews from the Amazon Review datasets ([Furniture Dataset](https://s3.amazonaws.com/amazon-reviews-pds/tsv/amazon_reviews_us_Furniture_v1_00.tsv.gz)), and extracted the dataset into a DataFrame. Then the DataFrame was transformed into four separate DataFrames that match the table schema in pgAdmin. Then the transformed data was uploaded into the appropriate tables. All steps are listed below:<br/>
1. Create a new database with Amazon RDS.
2. In pgAdmin, create a new database in the Amazon RDS server
3. In pgAdmin, run a new query to create the tables for our new database. Now four new tables are created: customers_table, products_table, review_id_table, and vine_table
4. Start a new Google Colab Notebook called 'Amazon_Reviews_ETL'. To use Pyspark, install spark and Java, set environment variables and start a spark session.
5. Extract the 'furniture dataset' and create a new dataframe. 
6. Transform the dataset into four DataFrames that will match the schema in the pgAdmin tables.
7. Create customers_table dataframe
![customer_table_colab.png](https://github.com/rmat112/Amazon_Vine_Analysis/blob/main/Images/customer_table_colab.png)
9. Create products_table dataframe
![products_colab.png](https://github.com/rmat112/Amazon_Vine_Analysis/blob/main/Images/products_colab.png)
11. Create review_id_table dataframe
![reviw_id_colab.png](https://github.com/rmat112/Amazon_Vine_Analysis/blob/main/Images/reviw_id_colab.png)
13. Create vine_table dataframe
![vine_df_colab.png](https://github.com/rmat112/Amazon_Vine_Analysis/blob/main/Images/vine_df_colab.png)
15. Load the dataframes to corresponding tables in pgAdmin 
16. Queries are run to check that the tables have been populated

![review_id_table.png](https://github.com/rmat112/Amazon_Vine_Analysis/blob/main/Images/review_id_table.png)

![customers_table.png](https://github.com/rmat112/Amazon_Vine_Analysis/blob/main/Images/customers_table.png)

![products_table.png](https://github.com/rmat112/Amazon_Vine_Analysis/blob/main/Images/products_table.png)

![vine_table.png](https://github.com/rmat112/Amazon_Vine_Analysis/blob/main/Images/vine_table.png)

17. 'Amazon_Reviews_ETL' Google Colab Notebook was exported as an ipynb file, and available for review here: [Amazon_Reviews_ETL.ipynb](https://github.com/rmat112/Amazon_Vine_Analysis/blob/main/Amazon_Reviews_ETL.ipynb)

### Analysis - Section 2
In this section we worked on determining if there is bias towards reviews that were written as part of the Vine program. This task was completed by using PySpark.
1. A Google Colab notebook called Vine_Review_Analysis was created and used to extract the furniture dataset
2. Vine_table (from section 1) was recreated
3. The data in Vine_table is filtered to create a DataFrame where there are 20 or more total votes
![del2-20ormore.png](https://github.com/rmat112/Amazon_Vine_Analysis/blob/main/Images/del2-20ormore.png)
5. The data is filtered again to create a DataFrame where the percentage of 'helpful_votes' is equal to or greater than 50% 
![del2-helpfulvotes.png](https://github.com/rmat112/Amazon_Vine_Analysis/blob/main/Images/del2-helpfulvotes.png)
7. The data is filtered to create a DataFrame where there is a Vine review (paid reviews)
![del2-paid-df.png](https://github.com/rmat112/Amazon_Vine_Analysis/blob/main/Images/del2-paid-df.png)
9. The data is filtered to create a DataFrame where there isn’t a Vine review (unpaid reviews)
![del2-unpaid-df.png](https://github.com/rmat112/Amazon_Vine_Analysis/blob/main/Images/del2-unpaid-df.png)
11. The total number of reviews, the number of 5-star reviews, and the percentage 5-star reviews are calculated for all Vine and non-Vine reviews
![del2-paidStats.png](https://github.com/rmat112/Amazon_Vine_Analysis/blob/main/Images/del2-paidStats.png)

![del2-unpaidStats.png](https://github.com/rmat112/Amazon_Vine_Analysis/blob/main/Images/del2-unpaidStats.png)

13. 'Vine_Review_Analysis' Google Colab Notebook was exported as an ipynb file, and is available for review here: [Vine_Review_Analysis.ipynb](https://github.com/rmat112/Amazon_Vine_Analysis/blob/main/Vine_Review_Analysis.ipynb)

### Results
This analysis reveals the following:<br/>
-There are 136 Vine reviews as copared to 18,019 non-Vine reviews.<br/>
-There are 74 Vine revuews that were 5-stars as compared to 8,482 non-Vine 5-star reviews.<br/>
-There are 54.41% 5-star Vine reviews as compared to 47.07% non-Vine 5-star reviews.

 
## Summary
- Since the 5-star percentage for Vine reviews is slightly greater than the non-Vine reviews, this analysis shows that there is slight bias toward favorable reviews from Vine members.
- I recommend that we should perfom the same analysis on 4-star ratings to see if there is a similar pattern because 4-star ratings contribute to positive reveiews as well.

