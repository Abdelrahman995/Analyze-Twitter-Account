# Analyze Twitter Account "We Rate Dogs" 

By Shimaa Elabd

Date: December 30, 2018


We Rate Dogs is a Twitter account (@WeRateDogs) rates people's dogs with a humorous
comment about the dog. These ratings almost always have a denominator of 10. The
numerators, though? Almost always greater than 10. 11/10, 12/10, 13/10, etc. Why? Because
"they're good dogs Brent." 

![labrador](https://user-images.githubusercontent.com/25883512/50638692-60b47c80-0f67-11e9-9338-91c79d8a380a.jpg)


## Project Overview

In This project I've wrangled the WeRateDogs Twitter data to create interesting and trustworthy analyses and visualizations.
WeRateDogs downloaded their Twitter archive and sent it to Udacity via email exclusively to use in this project.
This archive contains basic tweet data (tweet ID, timestamp, text, etc.) for all 5000+ of their tweets as they stood on August 1, 2017.
The challenge lies in the fact that the Twitter archive is great, but it only contains very basic tweet information that comes in JSONformat. For a successful project,
I needed to gather, asses and clean the Twitter data for a worthy analysis and visualization.

## What Software is Needed?

Using Jupyter Notebook for example, The following packages (libraries) need to be installed via conda or pip:

- pandas
- NumPy
- requests
- tweepy
- json

## Data Wrangling (Analyzing and Visualizing) process


## Table of Contents
- [Part I - Gathering Data](#Gathering)
- [Part II - Assessing Data](#Assessing)
- [Part III - Cleaning Data](#Cleaning)
- [Part IV - Analysis, and Visualization](#AV)




<a id='Gathering'></a>
#### Part I - Gathering Data

## Gathering data

1. **The WeRateDogs Twitter archive file**: I've download this file manually "twitter_archive_enhanced.csv"


2. **The tweet image predictions**, i.e., what breed of dog is present in each tweet according to a neural network. This file (image_predictions.tsv) is hosted on Udacity's servers and I've downloaded it programmatically using the Requests library and the following URL: https://d17h27t6h515a5.cloudfront.net/topher/2017/August/599fd2ad_image-predictions/image-predictions.tsv


3. **Twitter API and JSON**: Each tweet's retweet count and favorite ("like") count at minimum, and followers_count and favourites_count and the date time the tweet have been created Using the tweet IDs in the WeRateDogs Twitter archive, query the Twitter API for each tweet's JSON data using Python's Tweepy library and store each tweet's entire set of JSON data in a file called tweet_json.txt file. Each tweet's JSON data is written to its own line. Then read this .txt file line by line into a pandas DataFrame with (at minimum) tweet ID, retweet count, and favorite count. 

    - For the first time this was a little bit hard task somehow. So I get some help from:
    - Tweepy docs:
        - https://tweepy.readthedocs.io/en/v3.5.0/getting_started.html
    - StackOverFlow :
        - https://stackoverflow.com/questions/28384588/twitter-api-get-tweets-with-specific-id
        

<a id='Assessing'></a>
#### Part II - Assessing Data

## Assessing data

1. Assess the gathered data visually and programmatically for quality and tidiness issues.


2. Detect and document at least eight (8) quality issues and two (2) tidiness issues.
        
        
### Quality
##### `twitter_archive` table
- Erroneous datatypes (Timestamp and retweeted_status_timestamp) are objects (strings) not datetime.
- Erroneous datatypes (dogtionary, dog_breed, source), are objects not categories.
- Erroneous datatypes (In_reply_to_status_id, in_reply_to_user_id, retweeted_status_id, retweeted_status_user_id) are float not integers.
- Nulls represented as None in Columns (name, doggo, floofer, pupper, puppo) 
- Invalid names like 'None', 'a', 'an', 'the', 'my' in the Column (name)
- Missing values in the dataset,There's 2278 nulls in the Columns (in_reply_to_status_id, in_reply_to_user_id)
- Missing values in the dataset,There's 2175 nulls in the Columns (retweeted_status_id, retweeted_status_user_id, retweeted_status_timestamp)
- Missing values in the dataset,There's 59 nulls in the Column (expanded_urls)
- There's Tweet_ids have Duplicated source in the Column (expanded_urls)

##### `image_predictions` table
- There's Tweet_ids have Duplicated source in the Column (jpg_url).
- Missing values from the image_predictions dataset (2075 rows instead of 2356).

##### `json_tweets` table
- There's 48 Duplicated Tweet_ids.
- Erroneous datatypes ('favorites','retweets','user_followers','user_favourites'), are float not integers.
- Duplicated values in the json_tweets dataset (2388 rows instead of 2356).


### Tidiness
- In `image_predictions` table columns (p1, p1_conf, p1_dog, p2, p2_conf, p2_dog, p3, p3_conf, p3_dog) can be replaced by two columns represent the dog breed and confidence level.
- `Json_tweets` , `Twitter_archive` and `Image_predictions` tables should be represented as one table.
- There's Unnecessary columns which will not help in the analysis process.
    - No need for retweets data in `twitter_archive` table (retweeted_status_id, retweeted_status_user_id, retweeted_status_timestamp) we need to Keep original tweets only.
    - No need for these columns in the analysis (in_reply_to_status_id, in_reply_to_user_id)
- Timestamp column in `twitter_archive` table duplicated in `json_tweets` table in date_time column    
- (doggo, floofer, pupper, puppo) columns in `twitter_archive` table should replaced by one column which is Dogtionary.


<a id='Cleaning'></a>
#### Part III - Cleaning Data

#### Tasks have been done for cleaning:

- Apply a function that replace these columns with only two columns. 
- Add new columns to `image_predictions` table contains represent the dog breed and confidence and drop these columns (p1, p1_conf, p1_dog, p2, p2_conf, p2_dog, p3, p3_conf, p3_dog)
- Merge json_tweets and image_predictions tables to the twitter_archive table and all in one table which is `twitter_df`
- Drop retweets columns in `twitter_archive` table
- Drop these columns (in_reply_to_status_id, in_reply_to_user_id)
- Drop the duplicated column in `twitter_archive` table which is date_time
- Apply function to Combine the (doggo, floofer, pupper, puppo) columns into one column which is dogtionary Using Cat Documentation: https://pandas.pydata.org/pandas-docs/stable/generated/pandas.Series.str.cat.html
- Handle the tweets with multiple stages.
- Convert (Timestamp) to datetime.
- Convert the ('favorites','retweets','user_followers','user_favourites') to integers using `astype`.
- Convert (dogtionary, dog_breed, source) to categoriesusing `astype`.
- Drop duplicates in tweet_id
- Rename the dogs by using the text column in a new column which is 'dog_name'
- Drop the 'name' column
- Drop duplicated jpg_url

<a id='AV'></a>
#### Part IV - Analysis, and Visualization

#### Analyzing, and Visualizing WeRateDog Twitter Account

( Check the Wrangling report [here](https://github.com/ShimaaElabd/Analyze-Twitter-Account/blob/master/Reports/Wrangle_Report.html) and Visualization report [here](https://github.com/ShimaaElabd/Analyze-Twitter-Account/blob/master/Reports/Act_Report.pdf))
