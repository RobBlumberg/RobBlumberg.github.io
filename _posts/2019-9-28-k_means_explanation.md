---
layout: post
title: Introduction to k-means clustering
---

Imagine you are a fisherman, and you cast a huge net which catches hundreds of fish of different shapes and sizes. You may want to separate the fish into different groups based on their shapes and sizes, since larger fish are more expensive than little ones. This is precisely the idea behind k-means clustering: separating a set of data points into groups based on their numerical features.

The easiest way to see what the k-means algorithm does is by looking at the diagram below. On the left, a set of data points have been plotted, but it is difficult to identify specific groups within the whole set, and where to draw the line between potential groups. However, the plot on the right shows the different groups determined by the k-means algorithm, which clearly divides the dataset into distinct groups.

![_config.yml]({{ site.baseurl }}/images/k_means_full.png)

Image taken from: https://mubaris.com/posts/kmeans-clustering/

## How does k-means determine the groups?

To divide a dataset into groups, we first need to tell k-means how many groups we want. The number of groups we choose is what determines the value of k. If we think that the data points should be separated into 2 groups, we choose k=2. If we want 10 groups, we choose k=10. The specific number of groups we choose depends on the data we're working with. Going back to our fish example, if we wanted to group the fish based on their shapes and sizes, we might choose k=3, since intuitively, there are small, medium and large fish.

Once we've told k-means how many groups we want, the algorithm starts off by picking k random data points out of the whole set. These k random points define the k groups. We refer to these group-defining points as 'centroids'. The other data points in the set are then each assigned to one of the k groups based on which centroid they are closest to. This idea is depicted below, where features 1 and 2 are the numerical values based on which we are grouping our data. In our fish example, feature 1 could be the length of the fish, and feature 2 could be its width.

![_config.yml]({{ site.baseurl }}/images/k_means_first_it.png)

Once all the data points have been assigned to a group, each group's centroid is redefined by taking the mean of the points in that group. For example, if one of the groups is made up of points (1,1), (2,2) and (3,3), the centroid of that group becomes (2,2). This step is shown in the plot below. Notice that the group-defining centroids no longer need to be actual points in the dataset.

![_config.yml]({{ site.baseurl }}/images/k_means_new_centroids.png)

Next, since we've redefined the centroids, there may be points which were initially assigned to one group, but are now in fact closer to a centroid in another group. So we run a second iteration of the algorithm, just like the first time, except now our starting centroids are different. Again, we assign each data point to the centroid it is closest to, and then redefine the centroids by taking the mean of the points in each group. If needed, we keep repeating these steps. We know when to stop repeating the algorithm once there are no points which need to be reassigned to a different group after redefining the centroids. And finally we're done! We have separated our dataset into k groups!

##Conclusion

In this post, we have seen how k-means can be useful in separating a dataset into different groups based on the similarities between points. We spoke about separating fish into groups based on their shapes and sizes, but k-means can be used to find groupings in any dataset where the points have numerical features. One last important aspect to mention is that throughout this article, we've focused on grouping data points based on two numerical features. This made the algorithm easier to visualize, since we were able to plot the points on a 2D-graph. However, in practice, the algorithm could be generalized to group data points based on any number of numerical features.
