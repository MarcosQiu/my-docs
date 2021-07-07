## Step 1: Requirements clarifications

It's always a good idea to ask questions about the exact scope of the problem we are trying to solve, since design questions are mostly open-ended, and they don’t have one correct answer. Also, due to the limit of time, we should clarify the part we are going to focus on.

For example if we are designing a twitter like system, questions we should probably ask at the beginning includes,

 - Will users of our service be able to post tweets and follow other people?
 - Should we also design to create and display the user’s timeline?
 - Will tweets contain photos and videos?
 - Are we focusing on the backend only, or are we developing the front-end too?
 - Will users be able to search tweets?
 - Do we need to display hot trending topics?
 - Will there be any push notification for new (or important) tweets?

The answers to these questions decide how our system should look like.


## Step 2: Back-of-the-envelope estimation

With the answers to the questions we asked above, it's good idea now to estimate the scale of the system.

 - expected scale, e.g. number of tweets, number of views, number of timeline generated per second, etc
 - storage requirements, e.g. it would be different if tweets contain videos or images
 - the network bandwidth usage we are expecting, deicdes how we should manage the traffic and balance the load


## Step 3: System interface definition

Define what APIs are expected from the system. It's helpful because we can be sure we haven’t gotten any requirements wrong by establishing the contract. E.g.

```py
postTweet(user_id, tweet_data, tweet_location, user_location, timestamp, …)  
generateTimeline(user_id, current_time, user_location, …)  
markTweetFavorite(user_id, tweet_id, timestamp, …)  
```


## Step 4: Defining data model

It will clarify how data will flow between different system components. Later, it will also guide for data partitioning and management.

 - **User**: UserID, Name, Email, DoB, CreationDate, LastLogin, etc.
 - **Tweet**: TweetID, Content, TweetLocation, NumberOfLikes, TimeStamp, etc.
 - **UserFollow**: UserID1, UserID2
 - **FavoriteTweets**: UserID, TweetID, TimeStamp

Further, the data model also helps us to choose between SQL and NoSQL.


## Step 5: High-level design

Draw a block diagram with 5-6 boxes representing the core components of our system. We should identify enough components that are needed to solve the actual problem from end to end.

For our twitter like service, from the high level, we can identify and draw components, including,

 - cluster of app servers that serve all the requests
 - load balancer to balance the load
 - database to store tweets data
 - distributed file storage to store images and videos


## Step 6: Detailed design

Dig deeper into two or three major components. We should present different approaches, their pros and cons, and explain why we will prefer one approach over the other. E.g.

 - how to partition our data
 - how will we handle hot users
 - should we try to store our data so that it is optimized for scanning the latest tweets
 - where would we introduce cache
 - what components need better load balancing


## Step 7: Identifying and resolving bottlenecks

Try to discuss as many bottlenecks as possible and different approaches to mitigate them.

 - single point of failure?
 - do we have data replica & server copies to increase availability?
 - how do we monitor the performance