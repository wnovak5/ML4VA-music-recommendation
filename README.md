# ML4VA-music-recommendation

## Abstract
We aim to create a ML algorithm that takes in a dataset of well-known, loved songs that will return a small list of songs
that will be catered to the user’s taste. We will experiment with many existing clustering algorithms and determine which applies best to our data. Using a dataset composed of many numerical and categorical features describing different aspects of songs, we will be able to create nuanced clusters of song recommendations.

## Introduction
Music is seen by many as a universal language. If you take a walk around grounds, you can be almost sure to see a
plethora of head phone users. We live in a generation where music is more accessible than it has ever been. But with
the sheer amount of media available at your disposal, it can be overwhelming and often difficult to find new music.
Finding a new song is a great feeling. It gives you the opportunity to share it with friends and family, and often times,
new songs will lead to the discovery of new artists. Streamlining this system could be impactful for both the consumer
and hidden young artists, which could have significant impacts within the Virginia community.

To begin our project we first found our dataset on Kaggle. Our dataset contained 30 features including genre, violence, danceability, loudness, acousticness just to name a few. The dataset contained data from 28,372 different songs spanning from the years 1950-2019. These songs came a plethora of different genres and artists. With our data imported and ready to go we began to analyze patterns and begin to write our algorithm. 


## Method
We began by importing the dataset and then moved on to visualization of the different categories. We decided to drop the majority of the object categories as they added little to no relevance to our ML algorithm (things like song ID and artist name). The only object categories that we kept were genre and topic as we felt these were relevant. We then created a pipeline using standard scaler for our numerical categories and a one hot encoder for our two object categories. We then normalized our pipeline as to ensure a normalized dataset. 

After this we began to visualize some of our metrics based on decade as to gain some insight on how music has changed over this time period. We found some very interesting patterns. For instance we found that violence has steadily increased in music since 1950 and subsequently romance has declined. We also found that energy and danceability increased as well. Here are pictures of acousticness and danceability which both changed significantly since 1950. 

After visualizing our data we began to run our first clustering algorithm. The first one we ran was k-means. We began by finding the elbow point to decide our number of clusters and after a bit of tuning found our elbow point to be 12. We then wrote our first song recommendation algorithm which took in the id of the song then found what cluster it was in and within this cluster used cosine distance to find the five closest songs within that cluster to our inputted song. 

After running k-means we decided to run the Balanced Iterative Reducing and Clustering using Hierarchies (BIRCH) as it supposed to be very good with clustering large datasets. We then ran the Gaussian Mixture Models (GMM) that takes a probabilistic approach to clustering. After this we ran both Density-Based Spatial Clustering of Applications with Noise (DBSCAN) and Hierarchical Density-Based Spatial Clustering of Applications with Noise (HDBSCAN) respectively. DBSCAN and HDBSCAN are both really good at identifying groups that are clustered very close together and identifying outliers as noise. HDBSCAN builds upon DBSCAN but uses a hierarchy of clusters to find the most suitable solution. We also applied our song recommendation algorithm to each of these algorithms. 

## Experiments
 With our initial dataset, we found that our models were struggling to provide recommendations that we felt were similar to the given song. For example, when entering a rock song, many of our models outputted either EDM or pop music. We experimented with some other students, asking if they liked the recommended songs or thought that the recommendations were relevant. In most cases, fellow students did not see much similarity between their chosen song and the five songs our models provided. We attributed this to the disproportionate number of pop songs in our dataset, which was skewing our output. We put some more time into finding a more balanced dataset, and were more deliberate in our preprocessing.
 
 Once we had our dataset, we found that some of our clustering algorithms did not produce expected results. DBSCAN and HDBSCAN, with our initial hyperparameters, struggled to cluster the songs. For example, HDBSCAN initially classified all points as noise points. Initially, while  just working with the hyperparameters, both models were only able to get either 1-2 large clusters with all the points, or all points being classified as noise points. To resolve this, we found that we needed to appropriately scale our dataset and then normalize it prior to feeding it into the clustering algorithm. This significantly improved our clusters. 

## Results
To analyze results, we first wanted to visualize all of our clustering algorithms. This was very difficult to do because our dataset had 30 features. To reduce the dimensionality, we used T-SNE visualization to project our results into two dimensions. Here are the results we got for each algorithm: 

The results from each algorithm all produced very similar clusters but all provided a slightly different number of clusters. HDBSCAN was an outlier, having around 42 clusters. When running our recommendation algorithm all of our models provided very similar songs and for the most part the 5 songs provided were identical. The algorithm that provided the least similar results to the rest was GMM and the top 5 would only alter by 1 or 2 songs for a particular run. 

After surveying 10 different students and receiving feedback on 3 different song recommendations each we received very positive feedback. Some patterns we saw were that the background of some song were very similar and thus would be recommended but the singing or style of the song would be very different.  

## Conclusion
Altogether, I think we achieved our initial goal. We built a robust music recommendation model that considers many different clustering algorithms. The recommended songs on any given input are consistent across algorithms, further validating our results. We think that are project could certainly help Virginia residents with music discovery. Beyond simply producing a working model, I think we learned many things in working on this project. Seeing how different features contributed to recommendations was fascinating. I think we both were intrigued by the cases where our model recommended songs that were clearly in very different genres. However, the songs often had clear overlap in other areas such as tempo, groove, instrumentation, key, etc. I think going forward, we could somehow factor in all clustering algorithms into a singular model as opposed to providing a recommender for each. We could possibly approach this through majority rules, where if multiple models agree on one song the overall model would recommend it. If there was no overlap, we could output the algorithm with the highest probability. Another way we could advance this project is through a clean UI. It would be great to allow users to select a song and have their songs outputted in an app of some sort. 

## References
https://medium.com/@ashu19/music-recommendation-system-using-machine-learning-8bc8cc52d143
https://www.kaggle.com/datasets/saurabhshahane/music-dataset-1950-to-2019
