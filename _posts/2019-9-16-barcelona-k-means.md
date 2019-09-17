---
layout: post
title: Clustering Barcelona's passes using k-means
---

The k-means clustering algorithm is one of the most frequently used machine learning algorithms. It's purpose is to partition unlabelled data points, which posses quantitative features, into k distinct groups. The algorithm achieves this grouping through an iterative process where k 'centroids' are calculated based on the data at hand. Each data point is assigned to the group with the centroid it is most similar to. 

Among the many applications of this clustering algorithm, k-means can be used to cluster a soccer team's passes. In fact, using k-means, passes can be separated into groups based on their stating location, length and direction. This technique has been done many times in the past, but here, I apply it to Barcelona's passing data, provided by Statsbomb. 

## Passing analysis with k-means: methodology 

The ultimate goal of this exercise is to determine what kind of passes Barcelona play more often (and less often) than their opponents. We can all agree that the peak of Barcelona's passing dominance came during the Pep-era, and so in this analysis, I'll use data from the 2011/12 season (Pep's last season in charge). 

The first step in acheiving the passing clusters is to calculate the actual centroids themselves. The centroids are calculated by feeding through all of Barcelona's passes, as well as their opponent's passes, into the k-means algorithm. 

**Important note:** I realize that this technique will mean that Barcelona's passes will weigh more heavily that those of their opponents in the calculation of the centroids, but given that Statsbomb only has Barcelona event-level data available for the 2011/12 La Liga season, I'll have to live with this limitation.

Luckily, python's sci-kit learn library has a great k-means clustering class. First though, I applied a standard scaler to the 4 features (x-starting position, y-starting position, length, direction) so that all features are weighed equally when clustering. Then, all that needed to be done was to choose the number of clusters and feed the data into the algorithm. In the end, through mostly visual inspection (the commonly used elbow-method did not prove to be very useful), I landed on **81 clusters**. You can see the 81 different clusters below: 

![_config.yml]({{ site.baseurl }}/images/barca_clusters.png)

Having defined our clusters, the next step was to determine the percentage of Barcelona's passes which were assigned to each cluster, as well as their opponents' percentages. The two sets could then be compared, and their differences would reveal which pass clusters Barcelona play more often than their opponents, and vice-versa. The results are shown in the plots below:

![_config.yml]({{ site.baseurl }}/images/barca_clusters_percentages_diff.png)

## Barcelona's top and bottom pass clusters

We can see, above, that the pass clusters that Barca used most often compared to their opponents are numbers 71, 76, 42, 78 and 62: 

![_config.yml]({{ site.baseurl }}/images/overrep.png)

The first thing we notice is that Barcelona have a tendency to play back towards the middle of the pitch when in forward positions, and when on the right wing. Their most over-represented pass cluster, #71, indicates that they like to play towards the left side of the pitch when starting in the middle third.

On the other hand, the pass clusters that Barca used least often compared to their opponents are numbers 10, 74, 63 and 59: 

![_config.yml]({{ site.baseurl }}/images/underrep.png)

The result above will be unsurprising to most: Barca play far less long balls than their opponents. Interestingly, Barca are also under-represented in pass cluster #59, where we see that they played few passes up the left wing. This is likely a consequence of the messi-effect, where Barca would have been much more likely to play passes on the right wing instead (partly evidenced by their over-representation in pass cluster #42 seen earlier).

## Conclusion

We saw in this post how to cluster a soccer team's passes using the k-means algorithm, and that this told us useful information about how Barcelona play. Ideally, it would have been nice to have data for all La Liga games so that the clusters were not calculated by heavily weighing Barca passes. Nevertheless, it is reassuring that we obtained results which were intuitive, but also insightful. 
