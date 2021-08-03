# HK WhiskyNav
![image](https://user-images.githubusercontent.com/80243823/127515288-aba383da-7a81-40dd-b987-f1453447bfad.png)

**Live Demo**

https://user-images.githubusercontent.com/80243823/127728671-34b19ae7-d8d7-458d-8c51-43ba419a1ff9.mp4

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

The aim here is to let users to take a photo of any bottle, the app will then recognize the brand and year of the whisky.
The approach we took was to train a neural network to read the label of the whisky bottle. For that, we used transfer learning and used 2 separate models in unison to acheive the goal.
One for locating the text, one for recognizing the text.

![image](https://user-images.githubusercontent.com/80243823/127945941-3e77467a-0e17-43b9-a069-2f82d1bf60c5.png)

It didn't work. The accuracy would be significantly affected by photo resolution, brightness, contrast, text orientation, camera focus etc. Thus, we changed our approach.

![image](https://user-images.githubusercontent.com/80243823/127946021-0a98e91a-502a-4c83-be50-cc79624ecd3b.png)

Instead of recognizing the text, we trained a neural network to classify the whisky based on the whole image. We used Convolutional Neural Network (CNN) to extract the features of a whisky bottle, like the shape, colour, position and words on the label.

![image](https://user-images.githubusercontent.com/80243823/127946185-18193067-3b44-4bfd-9386-ace1df4ee843.png)

There are good news and bad news. The good news is, there are good image recognition neural networks available online. The bad news is, none of them can recognise whisky. But since they are so good at image recognition, they must be good at feature extraction, so we used them for this purpose and InceptionV3 was our choice. We then trained our own neural network to classify the whisky based on the feature extraction result.

![image](https://user-images.githubusercontent.com/80243823/127946243-bdd87420-f868-470f-89c8-8ac8111b4a87.png)

We froze the feature extraction part, making it untrainable, and cut the classification part of InceptionV3, replacing it with our own neural network for the classification. Over 10 versions of the network were tested before we deployed the final one.

![image](https://user-images.githubusercontent.com/80243823/127946388-c804d6ff-2c14-46e9-9351-5395904c077e.png)

To train this neural network, we needed lots of data. We downloaded images of 100 different whiskies, around 25 images per whisky on average, all with different backgrounds. So we have more than 2500 images in total.

![image](https://user-images.githubusercontent.com/80243823/127946427-597b29ea-052a-41c6-a104-3ea3be31b716.png)

This is the performance of the network. We achieved 57% accuracy after days of training. However, we had bad news. No matter how hard we trained the model, it couldn’t break through the 60%, it was like there is a hidden wall there. We were not going to settle for 60% accuracy, so we adopted another new approach.

![image](https://user-images.githubusercontent.com/80243823/127946580-4f2497b3-89ea-4b15-bff7-54e936f64015.png)

Instead of feeding the network images with different backgrounds, this time, we fed it with cropped images of whisky, focusing on the bottle.

![image](https://user-images.githubusercontent.com/80243823/127946616-45437a81-18f5-44cf-a828-979c7b05ad47.png)

Not only that, we applied image augmentation to all the images we have. Each time, the program would pick a random number of random effects, by random magnitude. By doing so, we increased our sample size tenfold, to more than 25,000 images.

![image](https://user-images.githubusercontent.com/80243823/127946655-a19d422f-4707-4479-82d0-75ab1ec88a0d.png)

This was not the only trick up on our sleeves. We had a wild idea. Notice that all the images we fed to the network contained a bottle, so how does the network know the bottle is the focus here ? Imagine all the swans you see in your life are white, how do you know the colour of the swan is something you need to pay attention to ? So, we introduced a black swan to the network.
We trained the network to recognize non-whisky classes, all without a bottle. So by learning what is not, one knows what is.

![image](https://user-images.githubusercontent.com/80243823/127946789-543460a6-23fb-48a5-a4be-3d62b7e240e0.png)

This is the result. The model immediately broke through the 60% mark, and hit 71%. Not only that, whenever the accuracy plateaued at a certain level, I reduced the learning rate, and cut the batch size by half. Essentially, it means that instead of making big jumps for the gradient descent, the model made smaller, but more frequent jump to the minimum. The model eventually reached close to 95% accuracy.

![image](https://user-images.githubusercontent.com/80243823/127946853-ea155d30-8d59-4ee6-8199-2e4f65dda70f.png)

######## *During the later stage of the whole project, we discovered that there were data leakage during the 3rd stage of the neural network training, resulting in close training and validation accuracy. Fortunately, it didn't have negative impact to the recognition accuracy and the later field test still gave us very satisfactory results. This is one of the major lesson-learnt/insight we gained from this project.
