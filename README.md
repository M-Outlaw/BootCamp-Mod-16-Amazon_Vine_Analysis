# BootCamp-Mod-16-Amazon_Vine_Analysis
Performing analysis on Amazon reviews using PySpark.


## Overview of Project

### Purpose
The purpose of this analysis is to use PySpark to analyze a large amount of Amazon reviews written by members of the Amazon Vine program and add the data to SQL tables.


## Analysis and Results
### Data
- The data chosen to analyze was Amazon reviews of pet products via [https://s3.amazonaws.com/amazon-reviews-pds/tsv/amazon_reviews_us_Pet_Products_v1_00.tsv.gz](https://s3.amazonaws.com/amazon-reviews-pds/tsv/amazon_reviews_us_Pet_Products_v1_00.tsv.gz).
- The data was first imported to PySpark.
- Then, separated into 4 dataframes:
  * customers_df                           
  * <p align="center"><img src="https://github.com/M-Outlaw/BootCamp-Mod-16-Amazon_Vine_Analysis/blob/main/Graphics/PySpark_customers_df.png"width="253" height="184"/></p>
  * products_df
  * <p align="center"><img src="https://github.com/M-Outlaw/BootCamp-Mod-16-Amazon_Vine_Analysis/blob/main/Graphics/PySpark_products_df.png"width="291" height="178"/></p>
  * review_id_df
  * <p align="center"><img src="https://github.com/M-Outlaw/BootCamp-Mod-16-Amazon_Vine_Analysis/blob/main/Graphics/PySpark_review_id_df.png"width="572" height="178"/></p>
  * vine_df
  * <p align="center"><img src="https://github.com/M-Outlaw/BootCamp-Mod-16-Amazon_Vine_Analysis/blob/main/Graphics/PySpark_vine_df.png"width="671" height="184"/></p>

- PySpark was then connected to pgAdmin and the data in these dataframes were imported into the SQL tables.
<p align="center"><img src="https://github.com/M-Outlaw/BootCamp-Mod-16-Amazon_Vine_Analysis/blob/main/Graphics/SQL_customers_table.png"width="336" height="249"/></p>
<p align="center"><img src="https://github.com/M-Outlaw/BootCamp-Mod-16-Amazon_Vine_Analysis/blob/main/Graphics/SQL_products_table.png"width="582" height="252"/></p>
<p align="center"><img src="https://github.com/M-Outlaw/BootCamp-Mod-16-Amazon_Vine_Analysis/blob/main/Graphics/SQL_review_id_table.png"width="563" height="268"/></p>
<p align="center"><img src="https://github.com/M-Outlaw/BootCamp-Mod-16-Amazon_Vine_Analysis/blob/main/Graphics/SQL_vine_table.png"width="605" height="254"/></p>


### Vine Bias Analysis
- The vine dataframe then underwent further analysis in PySpark to see if there was any bias towards reviews that were written as part of the Vine program.
  * A new Colab file was created to perform the analysis.
  * The pet product Amazon reviews were uploaded again and the exact vine dataframe was created.
<p align="center"><img src="https://github.com/M-Outlaw/BootCamp-Mod-16-Amazon_Vine_Analysis/blob/main/Graphics/Vine_PySpark_redo.png"width="928" height="260"/></p>

- The vine dataframe was then filtered to include only the top reviews to reduce the amount of data to sift through and better aid in analysis. The filters included:
  * reviews that had 20 votes or higher.
  * <p align="center"><img src="https://github.com/M-Outlaw/BootCamp-Mod-16-Amazon_Vine_Analysis/blob/main/Graphics/Vine_filter_total.png"width="713" height="270"/></p>
  * reviews that had a percentage of helpful votes to total votes that was 50% or higher.
  * <p align="center"><img src="https://github.com/M-Outlaw/BootCamp-Mod-16-Amazon_Vine_Analysis/blob/main/Graphics/Vine_filter_helpful.png"width="1010" height="273"/></p>

- The data was then split into two categories, those that were part of the Vine program and those that were not.
<p align="center"><img src="https://github.com/M-Outlaw/BootCamp-Mod-16-Amazon_Vine_Analysis/blob/main/Graphics/Vine_filter_Vine.png"width="723" height="279"/></p>
<p align="center"><img src="https://github.com/M-Outlaw/BootCamp-Mod-16-Amazon_Vine_Analysis/blob/main/Graphics/Vine_filter_nonVine.png"width="714" height="273"/></p>

## Vine Bias Results
- The total number of non-Vine reviews far exceeded the total number of Vine reviews: 37,840 to 170.
- With such a large difference, it is obvious that the total number of non-Vine 5-star reviews would be much larger than the total number of Vine 5-star reviews: 20,612 to 65. However, this information doesn't tell us much because of the large differences in total reviews.
- Therefore, a percentage of 5-star reviews to total reviews was created for each category, Vine and non-Vine reviews.
  * Non-Vine reviews had a higher 5-star to total review percentage than Vine reviews: 54.5% to 38.2%:
<p align="center"><img src="https://github.com/M-Outlaw/BootCamp-Mod-16-Amazon_Vine_Analysis/blob/main/Graphics/Vine_stats_Vine.png"width="622" height="242"/></p>
<p align="center"><img src="https://github.com/M-Outlaw/BootCamp-Mod-16-Amazon_Vine_Analysis/blob/main/Graphics/Vine_stats_nonVine.png"width="620" height="249"/></p>


## Summary
- There does not seem to be any positive bias toward reviews in the Vine program.
  * Positive bias is when there is a tendency for people to judge a group more favorably than another. Therefore, for this to have positive bias for reviews in the Vine program, we would expect to see a much higher percentage of 5-star reviews for the Vine reviews than for the non-Vine reviews, since the 5-star rating is given to the reviews after they are submitted and the 5-star rating is the highest positive rating. Since non-Vine reviews had a higher 5-star percentage, this shows that there was not bias toward the Vine reviews group.
  * Furthermore, during the filtering process, only reviews that had a 50% or higher percentage of helpful_votes to total votes were kept in the data. If there was positive bias toward the Vine reviews, we would expect to see more total votes for the Vine reviews than the non-Vine reviews.

- Another analysis that could be performed to further support the fact that there was not positive bias toward the Vine group would be to see if verified purchase played a role in the number of 5-star reviews.
  * Each category of reviews (Vine and non-Vine) could be split into two groups of when verified purchase equals Y and when verified purchase equals N and then calculate the same 3 statistics of total reviews, total 5-star reviews, and percentage of 5-star reviews for all 4 categories.
  * Also, filtering the data after the helpful votes filter into the two categories of verified purchase instead of whether they are Vine or non-Vine reviews and then comparing the 5-star percentage of those to the 4 categories above could give some insight as to if this was a factor in giving the review 5-stars or not.





