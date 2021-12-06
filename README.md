# weratedogs
Udacity Data Wrangling course final project

# Wrangling Report

In this report, I will explain the wrangling process for wrangle_data.ipynb. There were three sets of data in use in this file.
1. The twitter archive provided by the WeRateDogs twitter account. This archive was read into the dataframe 'twitter_archive' and is later copied to 'archive_clean' in order to perform cleaning.
2. The image predictions file downloaded from cloudfront.net. This archive was read into the dataframe image_predictions and is later copied to 'images_clean' in order to perform cleaning. 
3. The twitter data that was scraped from Twitter with the Tweepy API. This data was read into the dataframe 'twitter_df' and is later copied to 'counts_clean' in order to perform cleaning.

Each dataframe had both quality and tidiness issues. Each issue was addressed as follows.

### Quality

1. The 'tweet_id' columns in twitter_archive and image_predictions were changed to object types using the astype function.

2. The 'timestamp' column in twitter_archive was changed to datetime type using the Pandas function to_datetime and disabling the UTC function to drop timezones.

3. The 'id' column in counts_clean was renamed to 'tweet_id' to match the other two dataframes using the Pandas rename function.  

4. The 'id' column was changed to object type using the astype function.

5. Some of the tweets were replies or retweeted from other users. This data should represent only tweets from WeRateDogs with ratings so they needed to be removed. To do this, I saved 'archive_clean' containing only the rows in which 'retweeted_status_id' and 'in_reply_to_status_id' were both null. I then dropped all columns with retweet or reply statuses.

6. Tweets with IDs 682808988178739200 and 686035780142297088 were identified as not containing ratings when the tweets with rating denominators not equal to 10 were asessed. They were then dropped.

7. Tweets with IDs 775096608509886464, 716439118184652801, 682962037429899265, 722974582966214656 have incorrectly extracted ratings. As it is such a small number, these wer dropped.

8. There were 14 rows with dogs in multiple stages of development. These rows were identified using a for loop and then dropped.






### Tidiness

*Tidy data should have the following characteristics:*
* *Each variable forms a column*
* *Each observation forms a row*
* *Each type of observational unit forms a table*

Tidiness issues to be fixed:
1.  All data should be in one single table of observations because they each contain observation data about individual tweets. This by merging dataframes on the 'tweet_id' column. Outer merges were performed so all data would be transferred.

2. Dog stages (doggo, floofer, pupper, or puppo) should be stored in a single column 'dog_stages'. This was accomplished by combining all four rows into a single row called 'stages' and dropping the original rows.
