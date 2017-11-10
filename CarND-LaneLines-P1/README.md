**Finding Lane Lines on the Road**

### 1. Pipeline Description 

My pipeline consisted of 3 steps:

+ Step 1: In this step, I try to extract the color yellow and white from the given image 

+ Step 2: Here I utilize Canny's algorithm to retain edges in the bottom rectangle region 

+ Step 3: In this step, after receiving line segments from Hough transformation, we need to detect two average lines corresponding to two lanes from these segments. In order to do that, I first cluster the line segments based on their slopes and intercepts using k-means with k=2. I have used clustering here to take into account of the cases both slopes are negative or positive which can happens in other situations eventhough in our our test cases, one slope is positive and another one is negative.
 After clustering to extract the average lane lines, I proceed to remove segment outliers. This is done based on computing the distance of segment endpoints to the average lane lines. After removing all the outliers, I recompute the average lane lines.


### 2. Identify potential shortcomings with your current pipeline

My pipeline works very well for test images as well as test videos except for a few cases in the challenge video. This is because the k-means algorithm failed to produce two clusters to represent two lane lines. In these cases, I notice that one cluster has much fewer members than the other cluster making k-means failed to produce the correct clustering. One reason of a cluster with few line segments than the other is the sun shade change making the pipeline failed to extract the lanes based on colors.  

### 3. Suggest possible improvements to your pipeline

We utilize a better clustering algorithm for uneven clusters. We need a better algorithm to select lanes based on color under various lightning conditions.  