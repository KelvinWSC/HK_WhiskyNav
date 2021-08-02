# HK WhiskyNav
![image](https://user-images.githubusercontent.com/80243823/127515288-aba383da-7a81-40dd-b987-f1453447bfad.png)

**Live Demo**

https://user-images.githubusercontent.com/80243823/127728671-34b19ae7-d8d7-458d-8c51-43ba419a1ff9.mp4
<br><br />

## **Background**
A 3-week capstone project utilizing Machine Learning, Deep Learning, Web Scraping, Recommendation System, Natural Language Processing and Data Visualization.
<br><br />

## **Description**
HK WhiskyNav uses Machine Learning to provide whisky identification, selling info consolidation, flavour analysis and recommendation services in one go.
User can upload a photo or image of a whisky bottle, the app then applies Deep Learning technology to distinguish 100 different popular whiskies found in HK and identify the correct brand and year.

After identification, the app then consolidates related information in real time, including price range, name and address of all available shops in HK.

Furthermore, through Machine Learning, the app can analyse the flavour profile of the whisky and display an easy-to-understand flavour description to the user.
Through the anaylsis of the flavour profile, the app can also accurately recommend similar whisky, or completely different whisky for user to explore.
<br><br />

## **Table of content**
The section below documents the process of building this application, the challenges we faced, the solution we explored and applied, and the results we obtained.
There are 3 episodes,

![image](https://user-images.githubusercontent.com/80243823/127727856-a9e0d0ea-806c-4017-9680-70c5ca806359.png)
<br><br />

## **Episode 1 - Data Collection**
![image](https://user-images.githubusercontent.com/80243823/127764839-b7cc6e32-9489-42a8-a275-ad9d8d917cdd.png)

There are 4 types of data we have to acquire for this project,
![image](https://user-images.githubusercontent.com/80243823/127764876-b118e555-eb42-4097-a981-aa67c1eae7a9.png)

**Top 100 whisky**

Due to the project scope and complexity, it is not practical to cater all whiskies in the world. Covering top 100 whiskies strikes a perfect balance between users' need and resources required to develop the application.
For that, we applied web scraping to acquire whisky info online, filtered and sorted them based on the no. of ratings, i.e. the popularity.

One of the challenges we faced was that the scrapped data contained lots of duplicated data. Different version of the same whisky would have different data entries.
Thus, we had to use "regex" to clear all duplicated data.

![image](https://user-images.githubusercontent.com/80243823/127764934-d6aa6ea2-2181-4635-a422-2c4bcbc37ee3.png)

**Whisky image**

For the development of the neural network, we downloaded images of different whiskies. The details of the challenges will be mentioned in episode 2.

![image](https://user-images.githubusercontent.com/80243823/127798879-6dda0ad2-fe75-4058-8d8a-a5072e731fba.png)

**Whisky flavour profile**

To analyse the flavour profile of whisky, we acquired the tasting notes database from whisky experts from the internation whisky community.
Aside from the comments from experts, we also web-scrapped reviews from general public from major online platform
![image](https://user-images.githubusercontent.com/80243823/127799009-640929b2-a19a-4eea-a804-e5791ec87e16.png)

**Availability in Hong Kong**

Our focus is the Hong Kong local market. To have a full picture of the whisky market, we web-scraped websites of all major whisky retailers and online retail platform.
The major challenge was that, different website has different structure, some even have anti-scraping measures employed. We had to develop unique scraping program for each website, using both "Beautiful Soup" and "Selenium" from Python library.

![image](https://user-images.githubusercontent.com/80243823/127799190-4d5d966e-b6aa-4a08-98a6-1d6f11a2faee.png)
![image](https://user-images.githubusercontent.com/80243823/127799243-95882e37-0c00-41b5-8144-6603af1d6a0d.png)

After acquiring all the info, we cleansed the data and visualized them in a simple way.
Since Google Map plug-in is not a free service, we've come up with a way to manipulate the URL, and also a way to parse both English and Chinese addresses, to allow the users to use Google Map for the shop address.
![image](https://user-images.githubusercontent.com/80243823/127799685-969d4f0f-2a25-430a-b2af-16c3fa3dd112.png)
<br><br />
## **Episode 2 - Image recognition**
![image](https://user-images.githubusercontent.com/80243823/127800095-9e0ce2b0-a6e1-4e57-a2a6-6a2558541983.png)
