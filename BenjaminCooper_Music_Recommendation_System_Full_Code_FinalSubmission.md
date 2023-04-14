# **Capstone Project:** Music Recommendation System
 **Author:** Benjamin Cooper
 <br>
 
 **Date:** 04/13/2023


## **Problem Definition**

### **The Context:**

        With the advent of smartphones and the consumer economy, there has been a revolution in the ways that people consume products and content. At the same time, digital music and digital music distribution platforms have become some of the most widely accessible and highly consumed product markets in the world. Yet with this deluge of digital music content comes a challenge: how do users find new content that they enjoy, and how do digital music platforms enable music discovery by users? These challenges are exacerbated by the fact that in the modern fast-paced world, people are often time or attention limited, there are other platforms competing for user attention, and digital content-based company's revenue often relies on the time consumers spend on, or interact with, its platform. These companies need to be able to figure out what kind of content is needed in order to increase customer time spent on their platform, the ammount of interaction had with their platform, and the overall satisfaction with a users experience on the platform. The key challenge for companies is in figuring out what kind of content their users are most likely to consume. 

        Spotify is one such music content provider with a huge market base across the world. With the ever-increasing volume of streaming music becoming available, finding new music of interest has become a tedious task in and of itself. Spotify has grown significantly in the market because of its ability to make highly personalized music recommendations to each and every user of its platform based on a huge preference database gathered over time - millions of customers and billions of songs. This is done by using smart recommendation systems that can recommend songs based on users’ likes/dislikes, incorporating both content-based and latent features for song recommendations. However, the recommendation system used by Spotify and its parameter settings have remained a proprietary, closely-guarded secret. Here, I build a recommendation system to provide a top 10 of personalized song recommendations to a user that the user is most likely to enjoy/like/interact-with based on that users personal musical preferences.

### **The objective:**

Build a recommendation system to propose the top 10 songs for a user based on the likelihood of listening to those songs.

### **The key questions:**

- What is the structure of the dataset?
- What variables will be used to make the recommendation system?
- What is the distribution of the 'rating' variable?
- Which models will be used to build a recommendation system?
- How will models be evaluated?
- Based on criteria, which model is 'best'?
- Is this model good enough for production?

### **The problem formulation**:

Using data science, we are trying to provide personalized song recommendations (the 'best' songs) to a user that that user is most likely to enjoy/like/interact-with the most based on that users personal musical preferences. 

## **Data Dictionary**

The core data is the Taste Profile Subset released by the Echo Nest as part of the Million Song Dataset. There are two files in this dataset. The first file contains the details about the song id, titles, release, artist name, and the year of release. The second file contains the user id, song id, and the play count of users.

__song_data__

- song_id - A unique id given to every song

- title - Title of the song

- Release - Name of the released album

- Artist_name - Name of the artist 

- year - Year of release

__count_data__

- user _id - A unique id given to the user

- song_id - A unique id given to the song

- play_count - Number of times the song was played

## **Data Source**
http://millionsongdataset.com/

### **Importing Libraries and the Dataset**

### **Load the dataset**

### **Understanding the data by viewing a few observations**




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>user_id</th>
      <th>song_id</th>
      <th>play_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>b80344d063b5ccb3212f76538f3d9e43d87dca9e</td>
      <td>SOAKIMP12A8C130995</td>
      <td>1</td>
    </tr>
    <tr>
      <th>1</th>
      <td>b80344d063b5ccb3212f76538f3d9e43d87dca9e</td>
      <td>SOBBMDR12A8C13253B</td>
      <td>2</td>
    </tr>
    <tr>
      <th>2</th>
      <td>b80344d063b5ccb3212f76538f3d9e43d87dca9e</td>
      <td>SOBXHDL12A81C204C0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>3</th>
      <td>b80344d063b5ccb3212f76538f3d9e43d87dca9e</td>
      <td>SOBYHAJ12A6701BF1D</td>
      <td>1</td>
    </tr>
    <tr>
      <th>4</th>
      <td>b80344d063b5ccb3212f76538f3d9e43d87dca9e</td>
      <td>SODACBL12A8C13C273</td>
      <td>1</td>
    </tr>
    <tr>
      <th>5</th>
      <td>b80344d063b5ccb3212f76538f3d9e43d87dca9e</td>
      <td>SODDNQT12A6D4F5F7E</td>
      <td>5</td>
    </tr>
    <tr>
      <th>6</th>
      <td>b80344d063b5ccb3212f76538f3d9e43d87dca9e</td>
      <td>SODXRTY12AB0180F3B</td>
      <td>1</td>
    </tr>
    <tr>
      <th>7</th>
      <td>b80344d063b5ccb3212f76538f3d9e43d87dca9e</td>
      <td>SOFGUAY12AB017B0A8</td>
      <td>1</td>
    </tr>
    <tr>
      <th>8</th>
      <td>b80344d063b5ccb3212f76538f3d9e43d87dca9e</td>
      <td>SOFRQTD12A81C233C0</td>
      <td>1</td>
    </tr>
    <tr>
      <th>9</th>
      <td>b80344d063b5ccb3212f76538f3d9e43d87dca9e</td>
      <td>SOHQWYZ12A6D4FA701</td>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>






<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>song_id</th>
      <th>title</th>
      <th>release</th>
      <th>artist_name</th>
      <th>year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>SOQMMHC12AB0180CB8</td>
      <td>Silent Night</td>
      <td>Monster Ballads X-Mas</td>
      <td>Faster Pussy cat</td>
      <td>2003</td>
    </tr>
    <tr>
      <th>1</th>
      <td>SOVFVAK12A8C1350D9</td>
      <td>Tanssi vaan</td>
      <td>Karkuteillä</td>
      <td>Karkkiautomaatti</td>
      <td>1995</td>
    </tr>
    <tr>
      <th>2</th>
      <td>SOGTUKN12AB017F4F1</td>
      <td>No One Could Ever</td>
      <td>Butter</td>
      <td>Hudson Mohawke</td>
      <td>2006</td>
    </tr>
    <tr>
      <th>3</th>
      <td>SOBNYVR12A8C13558C</td>
      <td>Si Vos Querés</td>
      <td>De Culo</td>
      <td>Yerba Brava</td>
      <td>2003</td>
    </tr>
    <tr>
      <th>4</th>
      <td>SOHSBXH12A8C13B0DF</td>
      <td>Tangle Of Aspens</td>
      <td>Rene Ablaze Presents Winter Sessions</td>
      <td>Der Mystic</td>
      <td>0</td>
    </tr>
    <tr>
      <th>5</th>
      <td>SOZVAPQ12A8C13B63C</td>
      <td>Symphony No. 1 G minor "Sinfonie Serieuse"/All...</td>
      <td>Berwald: Symphonies Nos. 1/2/3/4</td>
      <td>David Montgomery</td>
      <td>0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>SOQVRHI12A6D4FB2D7</td>
      <td>We Have Got Love</td>
      <td>Strictly The Best Vol. 34</td>
      <td>Sasha / Turbulence</td>
      <td>0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>SOEYRFT12AB018936C</td>
      <td>2 Da Beat Ch'yall</td>
      <td>Da Bomb</td>
      <td>Kris Kross</td>
      <td>1993</td>
    </tr>
    <tr>
      <th>8</th>
      <td>SOPMIYT12A6D4F851E</td>
      <td>Goodbye</td>
      <td>Danny Boy</td>
      <td>Joseph Locke</td>
      <td>0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>SOJCFMH12A8C13B0C2</td>
      <td>Mama_ mama can't you see ?</td>
      <td>March to cadence with the US marines</td>
      <td>The Sun Harbor's Chorus-Documentary Recordings</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
</div>



### **Let us check the data types and and missing values of each column**

    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 2000000 entries, 0 to 1999999
    Data columns (total 3 columns):
     #   Column      Dtype 
    ---  ------      ----- 
     0   user_id     object
     1   song_id     object
     2   play_count  int64 
    dtypes: int64(1), object(2)
    memory usage: 45.8+ MB


    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 1000000 entries, 0 to 999999
    Data columns (total 5 columns):
     #   Column       Non-Null Count    Dtype 
    ---  ------       --------------    ----- 
     0   song_id      1000000 non-null  object
     1   title        999985 non-null   object
     2   release      999995 non-null   object
     3   artist_name  1000000 non-null  object
     4   year         1000000 non-null  int64 
    dtypes: int64(1), object(4)
    memory usage: 38.1+ MB


#### **Observations and Insights:**
- The Count dataset has 3 columns (user_id, song_id, and play_count)
- The Count dataset has 2,000,000 observations
- The Songs dataset has 5 columns (song_id,title,release,artist_name,year)
- The Songs dataset has 1,000,000 observations
- There are some missing titles and releases
- The primary/foreign key to merge these two datasets is song_id

#### **Observations and Insights:**
- The user_id and song_id are encrypted and can be encoded. However, this could cause problems if we were working on a real life data science business problem where user_id and song_id might need to be retained, or if later on in this analysis we wanted to encorporate other features from the 1 million songs data set online. Therefore, I will not encode these. 
- As the data also contains users who have listened to very few songs and vice versa, filtering these records out of the data could 'get two birds with one stone' by decreasing the **cold start** problem, and decreasing the **computational resources** needed to analyze this large dataset.

==> NOTE <== <br>
A dataset of size 2000000 rows x 7 columns can be quite large and may require a lot of computing resources to process. This can lead to long processing times and can make it difficult to train and evaluate your model efficiently.
In order to address this issue, here we filter the dataset.
To do this, we will set a threshold and filter out all users who have listened to less than 90 songs,
and any songs that have been listen to less than 120 times

Now we will filter the dataset to decrease its size and reduce the class imbalance.

### Scaling play_count Method 1:
Because there are very few users who have listened to a song more than 5 times, we will set a threshold at 5 plays. We dont want to drop records with more than 5 plays because this is important information on users likes, but we can clip anything > 5 to 5.


    
![png](BenjaminCooper_Music_Recommendation_System_Full_Code_FinalSubmission_files/BenjaminCooper_Music_Recommendation_System_Full_Code_FinalSubmission_22_0.png)
    





    <seaborn.axisgrid.FacetGrid at 0x176ede110>




    
![png](BenjaminCooper_Music_Recommendation_System_Full_Code_FinalSubmission_files/BenjaminCooper_Music_Recommendation_System_Full_Code_FinalSubmission_23_1.png)
    


From this distribution plot, we can see that the number of songs played by each user (lets call it user interactions) is heavily right skewed. There are many (thousands) users who have only listened to a few songs, so any matrix we build from this data will be extremely sparse. We will attempt to reduce this by filtering out users who have less than a minimum number of total plays (therefore we have very little user preference data for them).




    <seaborn.axisgrid.FacetGrid at 0x1dd2270a0>




    
![png](BenjaminCooper_Music_Recommendation_System_Full_Code_FinalSubmission_files/BenjaminCooper_Music_Recommendation_System_Full_Code_FinalSubmission_26_1.png)
    


    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 1224498 entries, 0 to 1224497
    Data columns (total 7 columns):
     #   Column       Non-Null Count    Dtype 
    ---  ------       --------------    ----- 
     0   user_id      1224498 non-null  object
     1   song_id      1224498 non-null  object
     2   title        1224498 non-null  object
     3   release      1224498 non-null  object
     4   artist_name  1224498 non-null  object
     5   year         1224498 non-null  int64 
     6   play_count   1224498 non-null  int64 
    dtypes: int64(2), object(5)
    memory usage: 65.4+ MB


Filtering out less active users has decreased the imbalance somewhat. We still have a heavily right skewed distribution plot, but the class imbalance has been reduced by a factor of 5 (y limit is 1200 instead of 7000). This has also decreased the size of the dataset to 1.2 million records down from 2 million. <br><br>
Now lets continue to decrease the sparcity and imbalance of the data by filtering out any user/song records that have a play count less than 6. There are many more songs that users have only listened to 1 or a few times. We are trying to recommend highly rated songs, so we will get rid of these songs with low interactions and assume they are uninteracted with 'not-liked'.




    <seaborn.axisgrid.FacetGrid at 0x1dd80b970>




    
![png](BenjaminCooper_Music_Recommendation_System_Full_Code_FinalSubmission_files/BenjaminCooper_Music_Recommendation_System_Full_Code_FinalSubmission_30_1.png)
    


    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 185694 entries, 0 to 185693
    Data columns (total 7 columns):
     #   Column       Non-Null Count   Dtype 
    ---  ------       --------------   ----- 
     0   user_id      185694 non-null  object
     1   song_id      185694 non-null  object
     2   title        185694 non-null  object
     3   release      185694 non-null  object
     4   artist_name  185694 non-null  object
     5   year         185694 non-null  int64 
     6   play_count   185694 non-null  int64 
    dtypes: int64(2), object(5)
    memory usage: 9.9+ MB


We were able to dramatically reduce the size of the dataset with the previous step by 85%, this will speed up processing times for our models and also make the predictions more accurate by reducing the class imbalance. We can see in the above plot however, that there are still many songs that have only been played for a few users. This means that the matrix resulting from this data will still have a lot of sparcity. 
<br><br>Lets filter out all songs that have less than 20 user interactions:




    <seaborn.axisgrid.FacetGrid at 0x176f6bc70>




    
![png](BenjaminCooper_Music_Recommendation_System_Full_Code_FinalSubmission_files/BenjaminCooper_Music_Recommendation_System_Full_Code_FinalSubmission_34_1.png)
    





    <AxesSubplot: >




    
![png](BenjaminCooper_Music_Recommendation_System_Full_Code_FinalSubmission_files/BenjaminCooper_Music_Recommendation_System_Full_Code_FinalSubmission_35_1.png)
    


    <class 'pandas.core.frame.DataFrame'>
    RangeIndex: 124147 entries, 0 to 124146
    Data columns (total 7 columns):
     #   Column       Non-Null Count   Dtype 
    ---  ------       --------------   ----- 
     0   user_id      124147 non-null  object
     1   song_id      124147 non-null  object
     2   title        124147 non-null  object
     3   release      124147 non-null  object
     4   artist_name  124147 non-null  object
     5   year         124147 non-null  int64 
     6   play_count   124147 non-null  int64 
    dtypes: int64(2), object(5)
    memory usage: 6.6+ MB


With these filtering steps, we have reduced the class imbalance, decreased the size of the dataset to make models and gridsearch more tracteable, and we have decreased the extreme sparcity of our resulting recommendations matrices. Now we apply a threshhold limit to further reduce class imblance and the play_count range, and then apply a min max scalar to standardize the play_counts as a proxy for a 1-10 rating.

### Clipping and Scaling play_count:
Because there are very few users who have listened to a song more than 25 times, we will set a threshold at 25 plays. We dont want to drop records with more than 5 plays because this is important information on users likes, but we can clip anything > 25 to 25. Then we will apply a MinMaxScalar function from the sklearn package to scale the playcounts from 1-10.




    <seaborn.axisgrid.FacetGrid at 0x191a1b3a0>




    
![png](BenjaminCooper_Music_Recommendation_System_Full_Code_FinalSubmission_files/BenjaminCooper_Music_Recommendation_System_Full_Code_FinalSubmission_41_1.png)
    





    <seaborn.axisgrid.FacetGrid at 0x186305d20>




    
![png](BenjaminCooper_Music_Recommendation_System_Full_Code_FinalSubmission_files/BenjaminCooper_Music_Recommendation_System_Full_Code_FinalSubmission_42_1.png)
    


Our final play_counts, filtered, clipped and scaled look pretty good. The class imbalance between the left side of the X axis and the higher play_counts has been reduced, The play_counts are scaled from 1-10, and we have kept the records containing the highest ratings as 10's.




    (121900, 8)



The final dataset has 121,900 records. This is a much more maneagable number of records for training and testing models. We want to check tht we did not drop too many users or songs. After previous iterations testing the filtering, I had dropped over 90% of the songs so the final recommendations that were being made were not diverse and nearly the same for every user. Lets take a look at this and some other parts of the dataset in Exploratory Data Analysis...

## **Exploratory Data Analysis**

### **Let's check the total number of unique users, songs, artists in the data**

Total number of unique user id

    Number of unique USERS =  19212


Total number of unique song id

    Number of unique SONGS =  2210


Total number of unique artists

    Number of unique artists =  1194


#### **Observations and Insights:**
- There are 19212 unique users remaining in the dataset after filtering
- There are 2210 unique songs remaining in the dataset after filtering 
- There are 1194 Unique artists remaining in the dataset after filtering
- This looks like a great balance, we have filtered out rare users and songs but retained many different users and we have a diversity of songs and artists.

### **Let's find out about the most interacted songs and interacted users**

Most interacted songs




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>song_id</th>
      <th>play_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>138</th>
      <td>SOBONKR12A58A7A7E0</td>
      <td>1466</td>
    </tr>
    <tr>
      <th>80</th>
      <td>SOAUWYT12A81C206F1</td>
      <td>1445</td>
    </tr>
    <tr>
      <th>1624</th>
      <td>SOSXLTC12AF72A7F54</td>
      <td>1186</td>
    </tr>
    <tr>
      <th>478</th>
      <td>SOFRQTD12A81C233C0</td>
      <td>1133</td>
    </tr>
    <tr>
      <th>88</th>
      <td>SOAXGDH12A8C13F8A1</td>
      <td>1024</td>
    </tr>
    <tr>
      <th>357</th>
      <td>SOEGIYH12A6D4FC0E3</td>
      <td>993</td>
    </tr>
    <tr>
      <th>1188</th>
      <td>SONYKOW12AB01849C9</td>
      <td>831</td>
    </tr>
    <tr>
      <th>1901</th>
      <td>SOWCKVR12A8C142411</td>
      <td>748</td>
    </tr>
    <tr>
      <th>1343</th>
      <td>SOPUCYA12A8C13A694</td>
      <td>744</td>
    </tr>
    <tr>
      <th>647</th>
      <td>SOHTKMO12AB01843B0</td>
      <td>616</td>
    </tr>
  </tbody>
</table>
</div>



Most interacted users




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>user_id</th>
      <th>play_count</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>5683</th>
      <td>4be305e02f4e72dad1b8ac78e630403543bab994</td>
      <td>106</td>
    </tr>
    <tr>
      <th>766</th>
      <td>0a4c3c6999c74af7d8a44e96b44bf64e513c0f8b</td>
      <td>82</td>
    </tr>
    <tr>
      <th>827</th>
      <td>0b19fe0fad7ca85693846f7dad047c449784647e</td>
      <td>81</td>
    </tr>
    <tr>
      <th>8262</th>
      <td>6d625c6557df84b60d90426c0116138b617b9449</td>
      <td>74</td>
    </tr>
    <tr>
      <th>16334</th>
      <td>da3890400751de76f0f05ef0e93aa1cd898e7dbc</td>
      <td>69</td>
    </tr>
    <tr>
      <th>7930</th>
      <td>695179610d0b1fbb9d66267a3bd24946617af7fb</td>
      <td>67</td>
    </tr>
    <tr>
      <th>17477</th>
      <td>e9a7dba8248ced646ea192016660e3c9056c0d03</td>
      <td>66</td>
    </tr>
    <tr>
      <th>2996</th>
      <td>283882c3d18ff2ad0e17124002ec02b847d06e9a</td>
      <td>65</td>
    </tr>
    <tr>
      <th>5405</th>
      <td>48567d388c6a7dda0e9d0a7b6648bdb42440475c</td>
      <td>65</td>
    </tr>
    <tr>
      <th>10463</th>
      <td>8c78c69701072e204f4340ca4d6ee44fe39e40cc</td>
      <td>64</td>
    </tr>
  </tbody>
</table>
</div>



#### **Observations and Insights:**
- The most interacted song is 'SOBONKR12A58A7A7E0' which has been interacted with by 1466 different users
- The most active user is '4be305e02f4e72dad1b8ac78e630403543bab994', they have listened to 106 different songs

Songs played in a year




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>49</th>
      <th>48</th>
      <th>47</th>
      <th>46</th>
      <th>43</th>
      <th>45</th>
      <th>50</th>
      <th>41</th>
      <th>42</th>
      <th>...</th>
      <th>17</th>
      <th>21</th>
      <th>7</th>
      <th>6</th>
      <th>3</th>
      <th>5</th>
      <th>12</th>
      <th>1</th>
      <th>2</th>
      <th>4</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>year</th>
      <td>0</td>
      <td>2009</td>
      <td>2008</td>
      <td>2007</td>
      <td>2006</td>
      <td>2003</td>
      <td>2005</td>
      <td>2010</td>
      <td>2001</td>
      <td>2002</td>
      <td>...</td>
      <td>1977</td>
      <td>1981</td>
      <td>1967</td>
      <td>1966</td>
      <td>1962</td>
      <td>1965</td>
      <td>1972</td>
      <td>1958</td>
      <td>1960</td>
      <td>1963</td>
    </tr>
    <tr>
      <th>play_count</th>
      <td>26580</td>
      <td>12782</td>
      <td>10616</td>
      <td>7499</td>
      <td>6693</td>
      <td>5718</td>
      <td>4861</td>
      <td>4617</td>
      <td>4316</td>
      <td>4147</td>
      <td>...</td>
      <td>151</td>
      <td>145</td>
      <td>137</td>
      <td>134</td>
      <td>113</td>
      <td>110</td>
      <td>77</td>
      <td>66</td>
      <td>62</td>
      <td>61</td>
    </tr>
  </tbody>
</table>
<p>2 rows × 51 columns</p>
</div>






    Text(0, 0.5, 'number of releases')




    
![png](BenjaminCooper_Music_Recommendation_System_Full_Code_FinalSubmission_files/BenjaminCooper_Music_Recommendation_System_Full_Code_FinalSubmission_63_1.png)
    


#### **Observations and Insights:** 
- It is not clear whether the 'year' feature is, but it is most likely the year a song/album was released.
- We can clearly see that there in an increasing trend from 1960-2008 in the number of songs released
- This makes sense as there are more people, more artists, and musical equiptment, recording equiptment, and streaming platforms have made it easier to produce music

Now that we have explored the data, let's apply different algorithms to build recommendation systems.

## Building a baseline popularity-based recommendation systems

### **Popularity-Based Recommendation Systems**

Let's take the count and sum of play counts of the songs and build the popularity recommendation systems based on the sum of play counts.

#### Function for Rank Based Recommendation System

Let's create a function to find the top n songs for a recommendation based on the average play count of song. We will also add a threshold for a minimum number of playcounts for a song to be considered for recommendation.




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>artist_name</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>221</td>
      <td>keller williams</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Call It Off (Album Version)</td>
      <td>Tegan And Sara</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Clara meets Slope - Hard To Say</td>
      <td>Clara Hill</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Kelma</td>
      <td>Rachid Taha</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Numb (Album Version)</td>
      <td>Disturbed</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Voices On A String (Album Version)</td>
      <td>Thursday</td>
    </tr>
    <tr>
      <th>6</th>
      <td>What If I Do?</td>
      <td>Foo Fighters</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Encore Break</td>
      <td>Pearl Jam</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Reign Of The Tyrants</td>
      <td>Jag Panzer</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Dance_ Dance</td>
      <td>Fall Out Boy</td>
    </tr>
  </tbody>
</table>
</div>



# Part I: Collaborative Filtering, Matrix Factorization, and Clustering

### Some useful functions

**Think About It:** Which metric should be used for this problem to compare different models?

Function to calculate precision@k and recall@k, RMSE, and F1_Score@k to evaluate the model performance:

Function to get top n recommendations for a user based on model predictions:

Function to **tune recommendations by song popularity** - corrects the predicted interaction with a song by applying a weight to increase the 'rating' of songs that are in general more popular among users:

Function to compare metrics from different models:

Function to return predictions for a user for 3 songs:

### Split the Data into Train and Test

### **User User Similarity-Based Collaborative Filtering**

To build the user-user-similarity-based and subsequent models we will use the "surprise" library.

    RMSE: 3.1852
    MAE:  2.5755
      algorithm      rmse       mae  precision  recall  f1_score  popularity
    0  KNNbasic  3.185239  2.575525      0.682   0.772     0.724        24.3


**Observations and Insights:**<br>
For the untuned User-user similarity-based model,
- The RMSE is 3.18
- The MAE is 2.57
- The f1 score is 0.72
- The average popularity of recommended songs is 24.3

    predictions using <surprise.prediction_algorithms.knns.KNNBasic object at 0x18512cfa0> for user 6ccd111af9b4baa497aacd6d1863cbf5a141acc6:
    *************************
    prediction for Red Dirt Road by Brooks and Dunn
    user: 6d625c6557df84b60d90426c0116138b617b9449 item: SODBSUF12A8C141975 r_ui = 10.00   est = 3.97   {'actual_k': 21, 'was_impossible': False}
    *************************
    predictions for Till I collapse by Eminem and Nate Dogg
    user: 6d625c6557df84b60d90426c0116138b617b9449 item: SOBPKPW12A6701E8F9 r_ui = 1.00   est = 3.74   {'actual_k': 40, 'was_impossible': False}
    *************************
    prediction for SOTTGXB12A6701FA0B by Phoenix (other pheonix songs are 7.6
    user: 6d625c6557df84b60d90426c0116138b617b9449 item: SOTTGXB12A6701FA0B r_ui = None   est = 3.45   {'actual_k': 21, 'was_impossible': False}


**Observations and Insights:**
- For the song the user has seen with a rating of 10, the model predicted a rating of 3.97
- For the song the user has seen with a rating of 1, the model predicted a rating of 3.74
- For the unheard songs by the user, the model predicted 3.45
- The user-user similarity-based collaborative filtering method has good RMSE, MAE and f1_score, but...
- The user-user model isnt predicting ratings very well
- All three songs have similar predicted 'ratings' for this user

Now, let's try to tune the model and see if we can improve the model performance.

    2.8805243519619927
    {'k': 50, 'min_k': 9, 'sim_options': {'name': 'msd', 'user_based': True}}
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the msd similarity matrix...
    Done computing similarity matrix.
    Computing the cosine similarity matrix...
    Done computing similarity matrix.


    RMSE: 2.8309
    MAE:  2.2550
            algorithm      rmse       mae  precision  recall  f1_score  popularity
    0        KNNbasic  3.185239  2.575525      0.682   0.772     0.724        24.3
    1  KNNbasic_tuned  2.830942  2.254989      0.698   0.799     0.745        64.9


**Observations and Insights:**<br>
After tuning the user-user model,
- The RMSE has decreased over the untuned model
- The MAE has also decreased
- The f1 score has increased
- The popularity of recommended songs has increased

    predictions using <surprise.prediction_algorithms.knns.KNNBasic object at 0x18b1b8730> for user 6ccd111af9b4baa497aacd6d1863cbf5a141acc6:
    *************************
    prediction for Red Dirt Road by Brooks and Dunn
    user: 6d625c6557df84b60d90426c0116138b617b9449 item: SODBSUF12A8C141975 r_ui = 10.00   est = 8.95   {'actual_k': 21, 'was_impossible': False}
    *************************
    predictions for Till I collapse by Eminem and Nate Dogg
    user: 6d625c6557df84b60d90426c0116138b617b9449 item: SOBPKPW12A6701E8F9 r_ui = 1.00   est = 3.14   {'actual_k': 40, 'was_impossible': False}
    *************************
    prediction for SOTTGXB12A6701FA0B by Phoenix (other pheonix songs are 7.6
    user: 6d625c6557df84b60d90426c0116138b617b9449 item: SOTTGXB12A6701FA0B r_ui = None   est = 3.38   {'actual_k': 21, 'was_impossible': False}


**Observations and Insights:**
- The model is predicting a rating of 8.95 for the song the user has heard and rated a 10, this is very good.
- The model is predicting a rating of 3.14 for the song the user has heard and rated a 1, this is not bad.
- The model is rating the unheard song 3.38.
- It seems that tuning the model has improved its ability to predict ratings

#### Correcting the play_counts and Ranking the recommended songs




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>artist_name</th>
      <th>count_plays</th>
      <th>predicted_interaction</th>
      <th>corrected_ratings</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Clara meets Slope - Hard To Say</td>
      <td>Clara Hill</td>
      <td>89</td>
      <td>9.205088</td>
      <td>9.099088</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Numb (Album Version)</td>
      <td>Disturbed</td>
      <td>68</td>
      <td>8.825430</td>
      <td>8.704162</td>
    </tr>
    <tr>
      <th>2</th>
      <td>When You're Gone</td>
      <td>Avril Lavigne</td>
      <td>76</td>
      <td>8.568666</td>
      <td>8.453958</td>
    </tr>
    <tr>
      <th>3</th>
      <td>#40</td>
      <td>DAVE MATTHEWS BAND</td>
      <td>72</td>
      <td>8.503340</td>
      <td>8.385488</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Speechless (Album Version)</td>
      <td>The Veronicas</td>
      <td>45</td>
      <td>8.512847</td>
      <td>8.363776</td>
    </tr>
    <tr>
      <th>5</th>
      <td>XRDS</td>
      <td>Covenant</td>
      <td>51</td>
      <td>8.475145</td>
      <td>8.335117</td>
    </tr>
    <tr>
      <th>6</th>
      <td>(iii)</td>
      <td>The Gerbils</td>
      <td>88</td>
      <td>8.352223</td>
      <td>8.245623</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Modern world</td>
      <td>Modern Lovers</td>
      <td>51</td>
      <td>8.274458</td>
      <td>8.134430</td>
    </tr>
    <tr>
      <th>8</th>
      <td>The Memory Remains</td>
      <td>Metallica / Marianne Faithfull</td>
      <td>94</td>
      <td>8.209485</td>
      <td>8.106343</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Sunburn</td>
      <td>Muse</td>
      <td>15</td>
      <td>8.156890</td>
      <td>7.898691</td>
    </tr>
  </tbody>
</table>
</div>



**Observations and Insights:**
- Here we have predicted 10 songs for the user '6d625c6557df84b60d90426c0116138b617b9449' with the user-user collaborative filtering method
- Some of the songs that are recommended to the user have a predicted rating close to 10, this is very good. 
- Evaluating the tuned and untuned models, the tuned model has improved performance. 

### Item Item Similarity-based collaborative filtering recommendation systems 

    RMSE: 2.9990
    MAE:  2.2550
            algorithm      rmse       mae  precision  recall  f1_score  popularity
    0        KNNbasic  3.185239  2.575525      0.682   0.772     0.724        24.3
    1  KNNbasic_tuned  2.830942  2.254989      0.698   0.799     0.745        64.9
    2   KNNbasic_item  2.998977  2.254952      0.658   0.736     0.695        25.1


**Observations and Insights:**
- The RMSE for the item-item model is 2.99
- The item-item collaborative filtering model has nearly the the same MAE as the tuned user-user model
- the f1 score is 0.695
- The popularity of recommended songs is 25

    predictions using <surprise.prediction_algorithms.knns.KNNBasic object at 0x18baaaf80> for user 6d625c6557df84b60d90426c0116138b617b9449:
    *************************
    prediction for Red Dirt Road by Brooks and Dunn
    user: 6d625c6557df84b60d90426c0116138b617b9449 item: SODBSUF12A8C141975 r_ui = 10.00   est = 4.40   {'actual_k': 40, 'was_impossible': False}
    *************************
    predictions for Till I collapse by Eminem and Nate Dogg
    user: 6d625c6557df84b60d90426c0116138b617b9449 item: SOBPKPW12A6701E8F9 r_ui = 1.00   est = 4.44   {'actual_k': 23, 'was_impossible': False}
    *************************
    prediction for SOTTGXB12A6701FA0B by Phoenix (other pheonix songs are 7.6
    user: 6d625c6557df84b60d90426c0116138b617b9449 item: SOTTGXB12A6701FA0B r_ui = None   est = 4.72   {'actual_k': 12, 'was_impossible': False}


**Observations and Insights:**
- The model is predicting 4.4 for the heard song that had rating of 10
- The model is predicting 4.44 for the heard song that had rating of 1
- The model is predicting 4.72 for the unheard song
- Overall, the prediction of ratings is poor

    2.9243151529965794
    {'k': 50, 'min_k': 3, 'sim_options': {'name': 'cosine', 'user_based': False}}


    RMSE: 2.9040
    MAE:  2.3017
                 algorithm      rmse       mae  precision  recall  f1_score  \
    0             KNNbasic  3.185239  2.575525      0.682   0.772     0.724   
    1       KNNbasic_tuned  2.830942  2.254989      0.698   0.799     0.745   
    2        KNNbasic_item  2.998977  2.254952      0.658   0.736     0.695   
    3  KNNbasic_item_tuned  2.903997  2.301706      0.688   0.785     0.733   
    
       popularity  
    0        24.3  
    1        64.9  
    2        25.1  
    3        25.5  


**Observations and Insights:**
- The RMSE decreased slightly after tuning
- The MAE has increased slightly
- The f1 score increased  
- The popularity is the same

We can also find out **similar items** to a given item or its nearest neighbors based on this **KNNBasic algorithm**. Below we are finding the 5 most similar items to the item 0




    [35, 288, 291, 392, 500]



    predictions using <surprise.prediction_algorithms.knns.KNNBasic object at 0x18a1774c0> for user 6d625c6557df84b60d90426c0116138b617b9449:
    *************************
    prediction for Red Dirt Road by Brooks and Dunn
    user: 6d625c6557df84b60d90426c0116138b617b9449 item: SODBSUF12A8C141975 r_ui = 10.00   est = 4.61   {'actual_k': 50, 'was_impossible': False}
    *************************
    predictions for Till I collapse by Eminem and Nate Dogg
    user: 6d625c6557df84b60d90426c0116138b617b9449 item: SOBPKPW12A6701E8F9 r_ui = 1.00   est = 4.44   {'actual_k': 23, 'was_impossible': False}
    *************************
    prediction for SOTTGXB12A6701FA0B by Phoenix (other pheonix songs are 7.6
    user: 6d625c6557df84b60d90426c0116138b617b9449 item: SOTTGXB12A6701FA0B r_ui = None   est = 4.72   {'actual_k': 12, 'was_impossible': False}


**Observations and Insights:**
- similar to the untuned item-item model, our predictions are rather poor
- In general, the predicted ratings of all the songs are about the same as the untuned model
- Given that all of these songs are quite different, these predictions may not reflect the users actually taste. 




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>artist_name</th>
      <th>count_plays</th>
      <th>predicted_interaction</th>
      <th>corrected_ratings</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Ni Tú Ni Nadie (Versión Demo)</td>
      <td>Alaska Y Dinarama</td>
      <td>31</td>
      <td>10.000000</td>
      <td>9.820395</td>
    </tr>
    <tr>
      <th>1</th>
      <td>My Perfect Cousin</td>
      <td>The Undertones</td>
      <td>21</td>
      <td>9.842105</td>
      <td>9.623887</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Walk On Water Or Drown (Album)</td>
      <td>Mayday Parade</td>
      <td>24</td>
      <td>9.684211</td>
      <td>9.480086</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Docking Bay 94</td>
      <td>The Alter Boys</td>
      <td>25</td>
      <td>9.661287</td>
      <td>9.461287</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Waters Of Nazareth (album version)</td>
      <td>Justice</td>
      <td>29</td>
      <td>9.210526</td>
      <td>9.024831</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Valentine</td>
      <td>Justice</td>
      <td>24</td>
      <td>8.934211</td>
      <td>8.730086</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Please_ Before I Go</td>
      <td>Derek Webb</td>
      <td>32</td>
      <td>8.905551</td>
      <td>8.728775</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Hitsville U.K.</td>
      <td>The Clash</td>
      <td>25</td>
      <td>8.421053</td>
      <td>8.221053</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Go Places</td>
      <td>The New Pornographers</td>
      <td>20</td>
      <td>8.342105</td>
      <td>8.118498</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Uptown</td>
      <td>Drake / Bun B / Lil Wayne</td>
      <td>24</td>
      <td>8.061607</td>
      <td>7.857483</td>
    </tr>
  </tbody>
</table>
</div>



**Observations and Insights:**
- Interestingly, the item-item model recommends a completely different top 10 songs than the user-user model

### Model Based Collaborative Filtering - Matrix Factorization

Model-based Collaborative Filtering is a **personalized recommendation system**, the recommendations are based on the past behavior of the user and it is not dependent on any additional information. We use **latent features** to find recommendations for each user.

    RMSE: 2.7215
    MAE:  2.1682
                 algorithm      rmse       mae  precision  recall  f1_score  \
    0             KNNbasic  3.185239  2.575525      0.682   0.772     0.724   
    1       KNNbasic_tuned  2.830942  2.254989      0.698   0.799     0.745   
    2        KNNbasic_item  2.998977  2.254952      0.658   0.736     0.695   
    3  KNNbasic_item_tuned  2.903997  2.301706      0.688   0.785     0.733   
    4                  SVD  2.721453  2.168153      0.696   0.798     0.744   
    
       popularity  
    0        24.3  
    1        64.9  
    2        25.1  
    3        25.5  
    4       138.3  


**Observations and Insights:**
- The SVD model has the best RMSE and MAE of any models yet
- The f1 score is higher than any other untuned models
- The popularity of recommended songs is far higher than the other models

    predictions using <surprise.prediction_algorithms.matrix_factorization.SVD object at 0x18bad1330> for user 6d625c6557df84b60d90426c0116138b617b9449:
    *************************
    prediction for Red Dirt Road by Brooks and Dunn
    user: 6d625c6557df84b60d90426c0116138b617b9449 item: SODBSUF12A8C141975 r_ui = 10.00   est = 8.95   {'was_impossible': False}
    *************************
    predictions for Till I collapse by Eminem and Nate Dogg
    user: 6d625c6557df84b60d90426c0116138b617b9449 item: SOBPKPW12A6701E8F9 r_ui = 1.00   est = 2.06   {'was_impossible': False}
    *************************
    prediction for SOTTGXB12A6701FA0B by Phoenix (other pheonix songs are 7.6
    user: 6d625c6557df84b60d90426c0116138b617b9449 item: SOTTGXB12A6701FA0B r_ui = None   est = 5.39   {'was_impossible': False}


**Observations and Insights:**
- The predictions for the heard song with rating 10 is 8.95
- The predictions for the heard song with rating 1 is 2.06
- The prediciton for the unheard song is 5.39
- These are the most accurate predictions yet of any of the models

#### Improving matrix factorization based recommendation system by tuning its hyperparameters

Function to Tune the number of factors:

Function to plot the number of factor tuning:

Lets run the factor checking function and see if there is an ideal number of latent features we can specify in our tuned model:


    
![png](BenjaminCooper_Music_Recommendation_System_Full_Code_FinalSubmission_files/BenjaminCooper_Music_Recommendation_System_Full_Code_FinalSubmission_129_0.png)
    


According to the figure, there is a decreasing trend of better performance with higher k. The lowest RMSE is achieved when 
k
=
80
. However, it is worth mentioning that 
k
=
52 and >84 are also good. The result suggests a range of values which can be used in GridSearchCV()for parameter tunning.

    2.7097656150739744
    {'n_epochs': 30, 'lr_all': 0.01, 'reg_all': 0.4, 'n_factors': 80}


    RMSE: 2.6736
    MAE:  2.1434
                 algorithm      rmse       mae  precision  recall  f1_score  \
    0             KNNbasic  3.185239  2.575525      0.682   0.772     0.724   
    1       KNNbasic_tuned  2.830942  2.254989      0.698   0.799     0.745   
    2        KNNbasic_item  2.998977  2.254952      0.658   0.736     0.695   
    3  KNNbasic_item_tuned  2.903997  2.301706      0.688   0.785     0.733   
    4                  SVD  2.721453  2.168153      0.696   0.798     0.744   
    5            SVD_tuned  2.673590  2.143426      0.694   0.799     0.743   
    
       popularity  
    0        24.3  
    1        64.9  
    2        25.1  
    3        25.5  
    4       138.3  
    5        43.2  


**Observations and Insights:**
- The tuned SVD model has a slightly lower RMSE and MAE than the base SVD model
- the f1_score of the the tuned SVD model increased .01
- The popularity of the tuned model dropped significantly
- The popularity of the base model may have been affected by a single highly rated song.

    predictions using <surprise.prediction_algorithms.matrix_factorization.SVD object at 0x18ed870a0> for user 6d625c6557df84b60d90426c0116138b617b9449:
    *************************
    prediction for Red Dirt Road by Brooks and Dunn
    user: 6d625c6557df84b60d90426c0116138b617b9449 item: SODBSUF12A8C141975 r_ui = 10.00   est = 8.22   {'was_impossible': False}
    *************************
    predictions for Till I collapse by Eminem and Nate Dogg
    user: 6d625c6557df84b60d90426c0116138b617b9449 item: SOBPKPW12A6701E8F9 r_ui = 1.00   est = 4.71   {'was_impossible': False}
    *************************
    prediction for SOTTGXB12A6701FA0B by Phoenix (other pheonix songs are 7.6
    user: 6d625c6557df84b60d90426c0116138b617b9449 item: SOTTGXB12A6701FA0B r_ui = None   est = 5.13   {'was_impossible': False}


**Observations and Insights:**
- The predictions for the heard song with rating 10 is about the same as the untuned model
- the prediction for the heard song with rating 1 came up a bit to 2
- In general the predicted ratings are much better than the non matrix factorization models, but tuning the SVD model did not improve performance much if at all.




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>artist_name</th>
      <th>count_plays</th>
      <th>predicted_interaction</th>
      <th>corrected_ratings</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Catch You Baby (Steve Pitron &amp; Max Sanna Radio...</td>
      <td>Lonnie Gordon</td>
      <td>616</td>
      <td>10.000000</td>
      <td>9.959709</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Clara meets Slope - Hard To Say</td>
      <td>Clara Hill</td>
      <td>89</td>
      <td>9.879379</td>
      <td>9.773379</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Make Her Say</td>
      <td>Kid Cudi / Kanye West / Common</td>
      <td>156</td>
      <td>9.186673</td>
      <td>9.106609</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Something (Album Version)</td>
      <td>Jaci Velasquez</td>
      <td>95</td>
      <td>8.532769</td>
      <td>8.430171</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Electric Feel</td>
      <td>MGMT</td>
      <td>179</td>
      <td>8.380396</td>
      <td>8.305653</td>
    </tr>
    <tr>
      <th>5</th>
      <td>He's A Pirate</td>
      <td>Klaus Badelt</td>
      <td>20</td>
      <td>8.514556</td>
      <td>8.290949</td>
    </tr>
    <tr>
      <th>6</th>
      <td>221</td>
      <td>keller williams</td>
      <td>51</td>
      <td>8.379492</td>
      <td>8.239464</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Gunn Clapp</td>
      <td>O.G.C.</td>
      <td>86</td>
      <td>8.313128</td>
      <td>8.205295</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Call It Off (Album Version)</td>
      <td>Tegan And Sara</td>
      <td>66</td>
      <td>8.098702</td>
      <td>7.975610</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Girls</td>
      <td>Death In Vegas</td>
      <td>25</td>
      <td>8.072738</td>
      <td>7.872738</td>
    </tr>
  </tbody>
</table>
</div>






<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>artist_name</th>
      <th>count_plays</th>
      <th>predicted_interaction</th>
      <th>corrected_ratings</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>False Pretense</td>
      <td>The Red Jumpsuit Apparatus</td>
      <td>21</td>
      <td>7.612781</td>
      <td>7.394563</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Sorrow (1997 Digital Remaster)</td>
      <td>David Bowie</td>
      <td>77</td>
      <td>6.734795</td>
      <td>6.620835</td>
    </tr>
    <tr>
      <th>2</th>
      <td>I'd Hate To Be You When People Find Out What T...</td>
      <td>Mayday Parade</td>
      <td>21</td>
      <td>6.831190</td>
      <td>6.612972</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Recado Falado (Metrô Da Saudade)</td>
      <td>Alceu Valença</td>
      <td>143</td>
      <td>6.648431</td>
      <td>6.564807</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Q-Ball</td>
      <td>Brotha Lynch Hung</td>
      <td>33</td>
      <td>6.705204</td>
      <td>6.531126</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Underground</td>
      <td>Eminem</td>
      <td>24</td>
      <td>6.631778</td>
      <td>6.427654</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Cold Blooded (Acid Cleanse)</td>
      <td>The fFormula</td>
      <td>38</td>
      <td>6.565968</td>
      <td>6.403747</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Walk Through Hell (featuring Max Bemis Acousti...</td>
      <td>Say Anything</td>
      <td>31</td>
      <td>6.578550</td>
      <td>6.398944</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Night Village</td>
      <td>Deep Forest</td>
      <td>20</td>
      <td>6.575026</td>
      <td>6.351420</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Drive</td>
      <td>Savatage</td>
      <td>24</td>
      <td>6.539166</td>
      <td>6.335042</td>
    </tr>
  </tbody>
</table>
</div>



**Observations and Insights:**
- The recommended songs from the tuned svd model are much different than the untuned svd model
- In general, it seems that the tuned model is recommending less popular songs

### Cluster Based Recommendation System

In **clustering-based recommendation systems**, we explore the **similarities and differences** in people's tastes in songs based on how they rate different songs. We cluster similar users together and recommend songs to a user based on play_counts from other users in the same cluster.

    RMSE: 2.9591
    MAE:  2.2116
                 algorithm      rmse       mae  precision  recall  f1_score  \
    0             KNNbasic  3.185239  2.575525      0.682   0.772     0.724   
    1       KNNbasic_tuned  2.830942  2.254989      0.698   0.799     0.745   
    2        KNNbasic_item  2.998977  2.254952      0.658   0.736     0.695   
    3  KNNbasic_item_tuned  2.903997  2.301706      0.688   0.785     0.733   
    4                  SVD  2.721453  2.168153      0.696   0.798     0.744   
    5            SVD_tuned  2.673590  2.143426      0.694   0.799     0.743   
    6         CoClustering  2.959111  2.211564      0.622   0.666     0.643   
    
       popularity  
    0        24.3  
    1        64.9  
    2        25.1  
    3        25.5  
    4       138.3  
    5        43.2  
    6        37.3  


**Observations and Insights:**
- The clustering model has an RMSE of 2.9 and MAE of 2.2
- The f1 score is .643
- Overal the clustering metrics are performing similarly slightly poorer compared to other models

    predictions using <surprise.prediction_algorithms.co_clustering.CoClustering object at 0x18ed866e0> for user 6d625c6557df84b60d90426c0116138b617b9449:
    *************************
    prediction for Red Dirt Road by Brooks and Dunn
    user: 6d625c6557df84b60d90426c0116138b617b9449 item: SODBSUF12A8C141975 r_ui = 10.00   est = 4.71   {'was_impossible': False}
    *************************
    predictions for Till I collapse by Eminem and Nate Dogg
    user: 6d625c6557df84b60d90426c0116138b617b9449 item: SOBPKPW12A6701E8F9 r_ui = 1.00   est = 4.00   {'was_impossible': False}
    *************************
    prediction for SOTTGXB12A6701FA0B by Phoenix (other pheonix songs are 7.6
    user: 6d625c6557df84b60d90426c0116138b617b9449 item: SOTTGXB12A6701FA0B r_ui = None   est = 3.17   {'was_impossible': False}


**Observations and Insights:**
- The predicted rating for the song with rating 10 is 4.71
- The predictions for the other heard song with raitng 1 is 4

#### Improving clustering-based recommendation system by tuning its hyper-parameters

    3.0094114249385258
    {'n_cltr_u': 3, 'n_cltr_i': 3, 'n_epochs': 40}


**Think About It**: How do the parameters affect the performance of the model? Can we improve the performance of the model further? Check the available hyperparameters [here](https://surprise.readthedocs.io/en/stable/co_clustering.html).

    RMSE: 2.9613
    MAE:  2.2139
                 algorithm      rmse       mae  precision  recall  f1_score  \
    0             KNNbasic  3.185239  2.575525      0.682   0.772     0.724   
    1       KNNbasic_tuned  2.830942  2.254989      0.698   0.799     0.745   
    2        KNNbasic_item  2.998977  2.254952      0.658   0.736     0.695   
    3  KNNbasic_item_tuned  2.903997  2.301706      0.688   0.785     0.733   
    4                  SVD  2.721453  2.168153      0.696   0.798     0.744   
    5            SVD_tuned  2.673590  2.143426      0.694   0.799     0.743   
    6         CoClustering  2.959111  2.211564      0.622   0.666     0.643   
    7   CoClustering_tuned  2.961292  2.213922      0.622   0.666     0.643   
    
       popularity  
    0        24.3  
    1        64.9  
    2        25.1  
    3        25.5  
    4       138.3  
    5        43.2  
    6        37.3  
    7        37.3  


**Observations and Insights:**
- Tuning the clustering model has not improved it

    predictions using <surprise.prediction_algorithms.co_clustering.CoClustering object at 0x18ed86d10> for user 6d625c6557df84b60d90426c0116138b617b9449:
    *************************
    prediction for Red Dirt Road by Brooks and Dunn
    user: 6d625c6557df84b60d90426c0116138b617b9449 item: SODBSUF12A8C141975 r_ui = 10.00   est = 4.70   {'was_impossible': False}
    *************************
    predictions for Till I collapse by Eminem and Nate Dogg
    user: 6d625c6557df84b60d90426c0116138b617b9449 item: SOBPKPW12A6701E8F9 r_ui = 1.00   est = 3.99   {'was_impossible': False}
    *************************
    prediction for SOTTGXB12A6701FA0B by Phoenix (other pheonix songs are 7.6
    user: 6d625c6557df84b60d90426c0116138b617b9449 item: SOTTGXB12A6701FA0B r_ui = None   est = 3.23   {'was_impossible': False}


**Observations and Insights:**
- The prediction for the heard song with rating 10 is 3.7

### Correcting the play_count and Ranking the above songs




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>artist_name</th>
      <th>count_plays</th>
      <th>predicted_interaction</th>
      <th>corrected_ratings</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Love Is Gone (Original Mix)</td>
      <td>David Guetta - Joachim Garraud - Chris Willis</td>
      <td>20</td>
      <td>8.561523</td>
      <td>8.337917</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cold Blooded (Acid Cleanse)</td>
      <td>The fFormula</td>
      <td>38</td>
      <td>8.275809</td>
      <td>8.113588</td>
    </tr>
    <tr>
      <th>2</th>
      <td>The World Is Mine</td>
      <td>David Guetta</td>
      <td>21</td>
      <td>8.056761</td>
      <td>7.838544</td>
    </tr>
    <tr>
      <th>3</th>
      <td>What Is Light? Where Is Laughter? (Album Version)</td>
      <td>Twin Atlantic</td>
      <td>20</td>
      <td>7.872448</td>
      <td>7.648841</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Kelma</td>
      <td>Rachid Taha</td>
      <td>58</td>
      <td>7.642269</td>
      <td>7.510962</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Love Is Not A Fight</td>
      <td>Warren Barfield</td>
      <td>36</td>
      <td>7.561523</td>
      <td>7.394857</td>
    </tr>
    <tr>
      <th>6</th>
      <td>I Wonder Why</td>
      <td>Dion &amp; The Belmonts</td>
      <td>41</td>
      <td>7.517873</td>
      <td>7.361699</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Hasta siempre</td>
      <td>Varios</td>
      <td>20</td>
      <td>7.552595</td>
      <td>7.328988</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Numb (Album Version)</td>
      <td>Disturbed</td>
      <td>68</td>
      <td>7.418666</td>
      <td>7.297398</td>
    </tr>
    <tr>
      <th>9</th>
      <td>221</td>
      <td>keller williams</td>
      <td>51</td>
      <td>7.411147</td>
      <td>7.271119</td>
    </tr>
  </tbody>
</table>
</div>



**Observations and Insights:**
- Ther top 10 recommended songs are similar to the user-user and SVD models

# Part II: Content Based Recommendation System

So far we have only used the play_count of songs to find recommendations but we have other information/features on songs as well, and these features can be used to increase the personalization of the recommendation system. For example, we can use the artist name and album title to recommend songs to users from artists/albums they like but songs they have not heard yet. We can also include the year the song was released and recommedn music from the same time period. 

### Some Useful Functions

function to pre-process the text data:

Function to get top 20 similar songs based on text cosign similarity:

Function to get user recommendations from cosign similarity text matrix based on a users top listened to songs:

### Preprocessing features for tf-idf




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>song_id</th>
      <th>artist_name</th>
      <th>release</th>
      <th>year</th>
      <th>year_text</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>SODGVGW12AC9075A8D</td>
      <td>Justin Bieber</td>
      <td>My Worlds</td>
      <td>2010</td>
      <td>twothousandtens</td>
    </tr>
    <tr>
      <th>1</th>
      <td>SODGVGW12AC9075A8D</td>
      <td>Justin Bieber</td>
      <td>My World 2.0</td>
      <td>2010</td>
      <td>twothousandtens</td>
    </tr>
    <tr>
      <th>2</th>
      <td>SOEPZQS12A8C1436C7</td>
      <td>Deadmau5</td>
      <td>Ghosts 'n' Stuff</td>
      <td>2009</td>
      <td>twothousandzeros</td>
    </tr>
    <tr>
      <th>3</th>
      <td>SOGDDKR12A6701E8FA</td>
      <td>Eminem / Hailie Jade</td>
      <td>The Eminem Show</td>
      <td>2006</td>
      <td>twothousandzeros</td>
    </tr>
    <tr>
      <th>4</th>
      <td>SOWGXOP12A6701E93A</td>
      <td>Eminem</td>
      <td>Without Me</td>
      <td>2002</td>
      <td>twothousandzeros</td>
    </tr>
  </tbody>
</table>
</div>






<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>year_text</th>
      <th>text</th>
    </tr>
    <tr>
      <th>song_id</th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>SODGVGW12AC9075A8D</th>
      <td>twothousandtens</td>
      <td>Justin Bieber My Worlds twothousandtens</td>
    </tr>
    <tr>
      <th>SODGVGW12AC9075A8D</th>
      <td>twothousandtens</td>
      <td>Justin Bieber My World 2.0 twothousandtens</td>
    </tr>
    <tr>
      <th>SOEPZQS12A8C1436C7</th>
      <td>twothousandzeros</td>
      <td>Deadmau5 Ghosts 'n' Stuff twothousandzeros</td>
    </tr>
    <tr>
      <th>SOGDDKR12A6701E8FA</th>
      <td>twothousandzeros</td>
      <td>Eminem / Hailie Jade The Eminem Show twothousa...</td>
    </tr>
    <tr>
      <th>SOWGXOP12A6701E93A</th>
      <td>twothousandzeros</td>
      <td>Eminem Without Me twothousandzeros</td>
    </tr>
  </tbody>
</table>
</div>



### tfidf and cosign similarity

We can now either get recommendations based on a song, or get recommendations for a user with the function we made based on that users top songs




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>artist_name</th>
      <th>count_plays</th>
      <th>predicted_interaction</th>
      <th>corrected_ratings</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Cats In The Cradle</td>
      <td>Ugly Kid Joe</td>
      <td>30</td>
      <td>7.789474</td>
      <td>7.606899</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Cold Blooded (Acid Cleanse)</td>
      <td>The fFormula</td>
      <td>38</td>
      <td>7.000000</td>
      <td>6.837779</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Hold Me_ Thrill Me_ Kiss Me_ Kill Me</td>
      <td>U2</td>
      <td>33</td>
      <td>6.770725</td>
      <td>6.596648</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Twilight Galaxy</td>
      <td>Metric</td>
      <td>28</td>
      <td>6.696697</td>
      <td>6.507715</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Last Nite</td>
      <td>The Strokes</td>
      <td>21</td>
      <td>6.724206</td>
      <td>6.505988</td>
    </tr>
    <tr>
      <th>5</th>
      <td>The Calculation (Album Version)</td>
      <td>Regina Spektor</td>
      <td>44</td>
      <td>6.636842</td>
      <td>6.486086</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Mansard Roof (Album)</td>
      <td>Vampire Weekend</td>
      <td>26</td>
      <td>6.587426</td>
      <td>6.391310</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Face To Face</td>
      <td>Daft Punk</td>
      <td>32</td>
      <td>6.525241</td>
      <td>6.348465</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Injection</td>
      <td>Rise Against</td>
      <td>23</td>
      <td>6.485387</td>
      <td>6.276872</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Chinese</td>
      <td>Lily Allen</td>
      <td>14</td>
      <td>6.092105</td>
      <td>5.824844</td>
    </tr>
  </tbody>
</table>
</div>



**Observations and Insights:**
- This is excellent, we are recommending songs by the same artists/albums the user has likes and adding in some weight for the decade of the users song preferences. 
- We are also ranking the recommendations based on song popularity, so more listened to songs by other users will be weighted heavier for this user

# Part III: hybrid recommendation system
We have explored five different recommender methods (six if you include the popularity-based method) for recommending songs to a user in a personalized way. This is all well and good, but how do we know which method is recommending songs the user will actualy listen to? As an avid listener of music, is it not also true that a users preferences can change, and may change drastically during the day or from day to day? It also seems that the models we have presented so far sometimes recommend similar songs, but other models are drastically different as in the item-item recommendations and content based recommendations. In this section, I build a hybrid recommender system which takes into account recommendations from multiple models, applys weights based on which models we want to be most represented in the results, and then provides a 'hybrid' recommendation. 

### Functions

define a function to combine the predictions using the weights to combine recommender matrices from multiple models and compute the RMSE score:

Function to combine matrices from multiple models, with specified weightings, and Content Based recommendations, and output hybrid recommendation list:

Here I fit models and make predictions for two models:
- SVD (default settings)
- User-User collaborative Filtering (tuned)<br>

I chose these two models because both had the best F1_scores metrics, both had fairly good predictions, and both recommended markedly different songs. 

- I then add in a subset of recommendations from the content-based filtering method to increase the 'familiarity' for the user of the recommended songs/artists

This will hopefully provide a highly personalized recommendation for a user with a balance of new songs and familiar artists to give choices based on potential dynamic user preferences.



now evaluate the performance of different weight combinations using the hold-out set. For example, we can try different combinations of wA and wB, ranging from (0.1, 0.9) to (0.9, 0.1), and compute their respective RMSE scores:

    RMSE: 2.7976
    MAE:  2.2302
    Weight combination (0.1, 0.9): RMSE = 2.7976, MAE = 2.2302
    RMSE: 2.7495
    MAE:  2.1971
    Weight combination (0.3, 0.7): RMSE = 2.7495, MAE = 2.1971
    RMSE: 2.7186
    MAE:  2.1749
    Weight combination (0.5, 0.5): RMSE = 2.7186, MAE = 2.1749
    RMSE: 2.7057
    MAE:  2.1634
    Weight combination (0.7, 0.3): RMSE = 2.7057, MAE = 2.1634
    RMSE: 2.7110
    MAE:  2.1619
    Weight combination (0.9, 0.1): RMSE = 2.7110, MAE = 2.1619


**Observations and Insights:**
- there is not much difference in RMSE for the different combinations of model weights
- The 'best' weight combination is SVD .7 - collaborative filtering .3

    popularity of recommended songs:  85.1





<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>artist_name</th>
      <th>count_plays</th>
      <th>predicted_interaction</th>
      <th>corrected_ratings</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Clara meets Slope - Hard To Say</td>
      <td>Clara Hill</td>
      <td>89</td>
      <td>9.677092</td>
      <td>9.571092</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Catch You Baby (Steve Pitron &amp; Max Sanna Radio...</td>
      <td>Lonnie Gordon</td>
      <td>616</td>
      <td>8.470891</td>
      <td>8.430600</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Make Her Say</td>
      <td>Kid Cudi / Kanye West / Common</td>
      <td>156</td>
      <td>7.772713</td>
      <td>7.692649</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Cats In The Cradle</td>
      <td>Ugly Kid Joe</td>
      <td>30</td>
      <td>7.789474</td>
      <td>7.606899</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Recado Falado (Metrô Da Saudade)</td>
      <td>Alceu Valença</td>
      <td>143</td>
      <td>7.642525</td>
      <td>7.558901</td>
    </tr>
    <tr>
      <th>5</th>
      <td>#40</td>
      <td>DAVE MATTHEWS BAND</td>
      <td>72</td>
      <td>7.661807</td>
      <td>7.543956</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Walk Through Hell (featuring Max Bemis Acousti...</td>
      <td>Say Anything</td>
      <td>31</td>
      <td>7.678929</td>
      <td>7.499324</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Eternal Flame (Single Version)</td>
      <td>Atomic Kitten</td>
      <td>49</td>
      <td>7.411352</td>
      <td>7.268495</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Love Is Not A Fight</td>
      <td>Warren Barfield</td>
      <td>36</td>
      <td>7.379032</td>
      <td>7.212366</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Voices On A String (Album Version)</td>
      <td>Thursday</td>
      <td>128</td>
      <td>7.295797</td>
      <td>7.207409</td>
    </tr>
    <tr>
      <th>10</th>
      <td>The Quest</td>
      <td>HYPOCRISY</td>
      <td>27</td>
      <td>7.333201</td>
      <td>7.140751</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Hasta La Vista</td>
      <td>Jordan Francis/Roshon Bernard Fegan</td>
      <td>53</td>
      <td>7.219907</td>
      <td>7.082546</td>
    </tr>
    <tr>
      <th>12</th>
      <td>(Nice Dream)</td>
      <td>Radiohead</td>
      <td>73</td>
      <td>7.133452</td>
      <td>7.016411</td>
    </tr>
    <tr>
      <th>13</th>
      <td>He's A Pirate</td>
      <td>Klaus Badelt</td>
      <td>20</td>
      <td>7.165812</td>
      <td>6.942205</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Sunburn</td>
      <td>Muse</td>
      <td>15</td>
      <td>7.181355</td>
      <td>6.923156</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Cold Blooded (Acid Cleanse)</td>
      <td>The fFormula</td>
      <td>38</td>
      <td>7.000000</td>
      <td>6.837779</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Hold Me_ Thrill Me_ Kiss Me_ Kill Me</td>
      <td>U2</td>
      <td>33</td>
      <td>6.770725</td>
      <td>6.596648</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Twilight Galaxy</td>
      <td>Metric</td>
      <td>28</td>
      <td>6.696697</td>
      <td>6.507715</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Last Nite</td>
      <td>The Strokes</td>
      <td>21</td>
      <td>6.724206</td>
      <td>6.505988</td>
    </tr>
    <tr>
      <th>19</th>
      <td>The Calculation (Album Version)</td>
      <td>Regina Spektor</td>
      <td>44</td>
      <td>6.636842</td>
      <td>6.486086</td>
    </tr>
  </tbody>
</table>
</div>



## **Conclusion and Recommendations**

**1. Comparison of various techniques and their relative performance based on chosen Metric (Measure of success)**:
- In General the Method 2 dataset had better MSE and MAE than the method 1 dataset, but the Method 1 dataset had better f1_score and the predictions for listened to songs were closer to the actual playcounts
- The SVD and user-user based models performed the best according to RMSE, MAE, and f1
- The item-item model recommended different songs that the SVD, clustering, and user-user
- In general, tuning the models did improve their performance, however it became clear that one of the biggest effects on model performance is the data going into the model. 
- The Content based recommender system, just based on artist name, album title and year does a decent job of recommending artists the user likes, and songs from albums the user has listened to.
- Many of the songs in the SVD,clustering, collaboritive filtering recommendations were not artists in the users top listened artist/song list, therefore I added the Content Based Recommendations into the hybrid recommender system.
- I chose to tune my hybrid recommendation system using SVD with default settings because it was the best performing model, and user-user collaborative Filtering model. Combining these added more potential song diversity that might align with the user preferences into the final recommendation. 
- I also added content-based recommendations into the hybrid model for 'familiarity'
- There is room for improvement in the performance of the models and final recommender system:
 - more features such as genre, loudness, danceability, and lyrics could be added as features to improve Content based recommendations
 - Further improvement could be made on filtering/scaling the play_counts to achieve better predictions
 - A different approach could be tried, such as Neural Networks

**2. Refined insights**:
- The impact of the Y variable - in this case play_count - cannot be understated. 
- The distribution and scarcity in the play_counts, and how I chose to filter and transform it had large impacts on the model performance
- The Content-based recommender system, although perhaps the 'simplist' of the models besides the popularity based recommender system, performs predictably and precisely recommends songs based on content
- matrix factorization outperformed other models. It runs quickly, and while it has only marginally better performace metrics than other collaborative or cluster-based models, its predictions were the closest to actual.
- The metrics you choose to assess model performance with are extremely important. depending on the metrics you choose, they can change the decisions you make about models and recommendations.

**3. Proposal for the final solution design:** 
- I am proposing the hybrid recommender system I built be adopted. It provides a good balance of artists/albums the user is known to like, but may not have listened to other songs of, and new content recommended by usesr-user collaborative filtering and matrix factorization,
- In short, it is highly personalized!
- This hybrid recommender system could be adjusted and improved further based on more features for content-based recommending or alternative compositions of models/weights

**Final 10 song recommendation for user 6d625c6557df84b60d90426c0116138b617b9449:** 




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>artist_name</th>
      <th>count_plays</th>
      <th>predicted_interaction</th>
      <th>corrected_ratings</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Clara meets Slope - Hard To Say</td>
      <td>Clara Hill</td>
      <td>89</td>
      <td>9.677092</td>
      <td>9.571092</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Catch You Baby (Steve Pitron &amp; Max Sanna Radio...</td>
      <td>Lonnie Gordon</td>
      <td>616</td>
      <td>8.470891</td>
      <td>8.430600</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Make Her Say</td>
      <td>Kid Cudi / Kanye West / Common</td>
      <td>156</td>
      <td>7.772713</td>
      <td>7.692649</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Cats In The Cradle</td>
      <td>Ugly Kid Joe</td>
      <td>30</td>
      <td>7.789474</td>
      <td>7.606899</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Recado Falado (Metrô Da Saudade)</td>
      <td>Alceu Valença</td>
      <td>143</td>
      <td>7.642525</td>
      <td>7.558901</td>
    </tr>
    <tr>
      <th>5</th>
      <td>#40</td>
      <td>DAVE MATTHEWS BAND</td>
      <td>72</td>
      <td>7.661807</td>
      <td>7.543956</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Walk Through Hell (featuring Max Bemis Acousti...</td>
      <td>Say Anything</td>
      <td>31</td>
      <td>7.678929</td>
      <td>7.499324</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Eternal Flame (Single Version)</td>
      <td>Atomic Kitten</td>
      <td>49</td>
      <td>7.411352</td>
      <td>7.268495</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Cold Blooded (Acid Cleanse)</td>
      <td>The fFormula</td>
      <td>38</td>
      <td>7.000000</td>
      <td>6.837779</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Hold Me_ Thrill Me_ Kiss Me_ Kill Me</td>
      <td>U2</td>
      <td>33</td>
      <td>6.770725</td>
      <td>6.596648</td>
    </tr>
  </tbody>
</table>
</div>



# Executive Summary

### *Problem Summary*
<font size="4">        With the advent of smartphones and the consumer economy, there has been a revolution in the ways that people consume products and content. At the same time, digital music and digital music distribution platforms have become some of the most widely accessible and highly consumed product markets in the world. Yet with this deluge of digital music content comes a challenge: how do users find new content that they enjoy, and how do digital music platforms enable music discovery by users? These challenges are exacerbated by the fact that in the modern fast-paced world, people are often time or attention limited, there are other platforms competing for user attention, and digital content-based company's revenue often relies on the time consumers spend on, or interact with, its platform. These companies need to be able to figure out what kind of content is needed in order to increase customer time spent on their platform, the ammount of interaction had with their platform, and the overall satisfaction with a users experience on the platform. The key challenge for companies is in figuring out what kind of content their users are most likely to consume. Spotify is one such music content provider with a huge market base across the world. With the ever-increasing volume of streaming music becoming available, finding new music of interest has become a tedious task in and of itself. Spotify has grown significantly in the market because of its ability to make highly personalized music recommendations to each and every user of its platform based on a huge preference database gathered over time - millions of customers and billions of songs. This is done by using smart recommendation systems that can recommend songs based on users’ likes/dislikes, incorporating both content-based and latent features for song recommendations. However, the recommendation system used by Spotify and its parameter settings have remained a proprietary, closely-guarded secret. Here, I build a recommendation system to provide a top 10 of personalized song recommendations to a user that the user is most likely to enjoy/like/interact-with based on that users personal musical preferences. 
</font>

### *Solution Summary*
<font size="4">       In total, I explored six recommendation systems using the 1 millions songs dataset<sup>1</sup> as part of the solution design for this project: popularity-based, user-user collaborative filtering, item-item collaborative filtering, matrix factorization, cluster-based, and content-based. To evaluate the different models analyzed here, I relied on the F1_score, model predictions of user/song interactions, and the top 10 recommended songs by each model. These metrics clearly demonstrate a higher level of performance by three of the six models: matrix factorization (Singular Value Decomposition with default settings, with a 70% weight applied), user-user collaborative filtering (KNN basic algorithm with msd distance, max cluster size of 50, minimum cluster size of 9, and 30% weight applied), and the content-based model (tf-idf encoding and cosign-similarity distance on album title, artist name, and release year). Therefore,  I propose a Hybrid-Based Recommendation System, built by combining these three models with the specified parameters, be adopted for personalized recommendations of music with maximum user interaction potential. The proposed hybrid recommendation system boasts fast computational times, high prediction accuracy of user preferences, and a balanced recommendation of familiar and diverse new music for users. However, the model is subject to limitations such as a 'cold start' problem when making predictions for new users with few listens, and with the ever-increasing volume of songs becoming available and users adopting the platform this will lead to longer and longer computation times (and presumably less user satisfaction). Addtionally, the model generally favors popular artists and songs, which could have an impact on the music industry by making it more difficult for new artists to break into the scene using this platform.<br>
       Importantly, to reduce the computational resources required to test, train, and evaluate the solution design for this project, it was necessary to reduce the size of the dataset to make it more computationally tractable. The resulting filtered dataset reduced the original '1 million  songs' dataset (with 2 million records) to 121,900 records and increased the accuracy of predicted user interactions by reducing high degree of imbalance in the data from infrequent users and unpopular songs. While these results do not address the 'cold start' issue, they deomstrate the importance of a filtering step for making fast and relevant recommendations. Therefore, I suggest the application of a pre-recommendation filter as part of the final final solution design. Additionally, the content-based part of the recommendation system could also be improved by incorporating further features such as genre, lyrics, danceability, and encoded recordings. With these additions to the content portion of the recommendation system, the weight of the content-based model in the final hybrid recommendation system might be increased in future versions of the product. I recommend that these limitations and proposals be considered in future releases of the recommendation system for improved user personalization and increased user satisfaction.
</font> 

### *Recommendations for implementation*
<font size="4">        In the short-term I recommend the adoption of a hybrid recommendation system based on the recommender built in part III of this analysis, but with the inclusion of multiple additional content-based features like those discussed above. However, keeping in mind that this is a minimum viable product (MVP) that has not been tested on users, I recommend this hybrid recommendation system (MVP) be launched as a development version prior to deployment into production. With the deployment of the development version, the product could be introduced to a subset of randomly selected users, who would have songs recommended to them using multiple configurations of the hybrid system. User interactions with these recommendations could then be tracked to determine which recommendation configuration is the most successful at producing user interactions with the recommended material. Following evaluation of the development deployment, I recommend the hybrid system configuration and individual model weights be adjusted for maximum user interaction/satisfaction and deployed into production on the full user platform. Finally, I recommend that all user interactions on the platform be tracked along with other user data such as age, location, and gender. These data will provide key insights for ML Ops Engineers to retrain the recommendation system for future releases of the product. 
</font>

# References
1. Thierry Bertin-Mahieux, Daniel P.W. Ellis, Brian Whitman, and Paul Lamere. The Million Song Dataset. In Proceedings of the 12th International Society for Music Information Retrieval Conference (ISMIR 2011), 2011.
