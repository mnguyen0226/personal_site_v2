---
author: "Minh T. Nguyen"
title: "Machine Learning for Profile-Matching System"
date: "2023-05-27"
description: "(Potential) machine learning solutions for profile-matching problem."
tags: ["web development", "long-read"]
categories: ["software engineer", "machine learning", "systems design"]
series: ["Systems Design"]
aliases: ["migrate-from-jekyl"]
ShowToc: true
TocOpen: false
draft: false
weight: 5
---

<p style="color: #286EE0"><strong>Status:</strong> [Latest]</p>

Lately, I have an opportunity to interview with a start-up CEO for a software engineer intern position. During our discussion, the CEO raised a very interesting software-system problem with the plan to integrate machine learning (ML) solution gradually. **Let's say that we have a Software-as-a-service (SaaS) that has a feature of matching buyers (or customers) with suitable potential sellers (or agents)**. This blog documents my research on the intriguing profile-matching problem, focusing on the matching algorithms.

Similar services can be found in dating apps (Tinder, Bumble) or social media platforms (LinkedIn, Facebook, Instagram, Youtube).

<center>
    <img style="width: 50%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/profile_matching/imgs/people_connection.png" />
</center>
<figcaption class="img_footer">
    Fig. 1. The ability to connnect people with technology is very powerful.</br>
    (Image source: 
    <a href="https://www.freecodecamp.org/news/deep-dive-into-graph-traversals-227a90c6a261/" class="img_footer">freeCodeCamp</a>).
</figcaption>
</br>

In this blog I will introduce four potential ML-based solutions:
- Agent-Profile Recommendation.
- Similar Agent-Profile Listing.
- People You Might Know.
- Chatbot.

## Prerequisites
Prior to discussing the solutions for profile-matching, let's assume that the following two features have been done (or will be solved separately): 

**Buyer-profile creation:** 
- Enable buyers to create an account with credentials. Personal-information-filing steps will be mentioned in the later profile-matching algorithms.
- Robust authentications, e.g., 2-factor authentication (2FA).
- Provide options for buyers to specify their preferred communication channels and availability for booking a meeting/chat with sellers.

**Seller-profile creation:**
- Enable sellers to create an account with credentials. Personal-information-filing steps will be mentioned in the later profile-matching algorithms.
- Robust authentications, e.g., 2-factor authentication (2FA).
- Provide options for sellers to manage their availability and updates their profiles/commodity.

## Agent-Profile Recommendation

We can consider the task of matching buyer and seller as a recommendation system. The objective here is to match the buyer to the best potential seller (or vice-versa). 

<center>
    <img style="width: 70%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/profile_matching/imgs/system.png" />
</center>
<figcaption class="img_footer">
    Fig. 2. Agent-profile recommendation diagram.
</figcaption>
</br>

**Assumptions:** The buyer does not necessary need to chat or interact with the seller initially, but he/she can view the seller's profile and book schedule to talk/chat to. We also need to assume that the buyer needs to login (so we have collected data) from them. Additional, we need to have a lot of sellers' profiles in our database.

**Framing problem as ML task:** The task is to maximize the constrainted number of relevant sellers (says, top 5 relevant sellers). Here, engineers or managers can define relevance based on rules. An example of the rules is that the seller's profile is relevant if the buyer explicily pressed the "star" button to save the buyer's profile. Once we can define relevance, we can construct a dataaset, train our model to predict the relevance score between buyer and seller(s).

**Data Collection:** As the both the sellers and the buyers need to log in, there are two ways to collect personal information and preference data: through filtering-tabs or through questionnaires. These questions can be curated by the company's commodity specialist. Here are the example of seller, buyer, and interaction databases.

<center>
    <img style="width: 100%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/profile_matching/imgs/buyer_db.png" />
    <img style="width: 100%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/profile_matching/imgs/seller_db.png" />
    <img style="width: 100%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/profile_matching/imgs/buyer_seller_db.png" />
</center>
<figcaption class="img_footer">
    Fig. 3. Examples of Buyer, Seller, Buyer-Seller Interaction databases.
</figcaption>
</br>

**Matching Algorithms:** For this type, there are 3 types of algorithms: Rule-based filtering (non-personalized), Profile-based filtering (personalized), and Collaborative filtering (personalized).

### Rule-based filtering
This way does not require any application of ML. The sellers' profiles are filtered generically through the buyer's selected filtering tabs or questionnaire. Thus, we only need to use the Seller database. It is a good start for our system.

**Pros:** Does not need to collect a lot of data to train the model.

**Cons:** Does not personalize and not use all 3 collected databases.

### Profile-based filtering
In this algorithm, we use sellers' profiles features to recommend new sellers' profiles to those the buyer found relevant in the base.

<center>
    <img style="width: 60%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/profile_matching/imgs/system_2.png" />
</center>
<figcaption class="img_footer">
    Fig. 4. Profile-based filtering example diagram.
</figcaption>
</br>

In Fig. 4, we see that `Buyer 1` engaged (starred profile, talked to, provided feedbacks, bought commodity,...) with `Seller 1`, `Seller 2`, `Seller 3` in the past. As `Seller 4` has similar profile as `Seller 1`, `Seller 2`, `Seller 3`, the system will recommend `Seller 4` to `Buyer 1`.

**Pros:** Has the ability to recommend newly added seller profile without the buyer accidentally view that profile prior.

**Cons:** Might be hard to discover buyer's new interest.

### Collaborative filtering
This filtering solution uses a buyer-buyer similarities to recommend new buyers' profiles. The idea is that similar buyers are interested in similar seller(s).

<center>
    <img style="width: 75%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/profile_matching/imgs/system_3.png" />
</center>
<figcaption class="img_footer">
    Fig. 5. Collaborative filtering example diagram.
</figcaption>
</br>

In Fig. 5, we can see that the goal is to recommend new seller's profile to `Buyer 2`. First, we find a similar buyer to `Buyer 2` based on their previous interaction, says `Buyer 1`. Then, we find the seller's profile that `Buyer 1` engaged but which `Buyer 1` has not seen yet, says `Seller 3`. We then recommend `Seller 3` to `Buyer 2`.

The main different between collaborative filtering and profile-based filtering is taht it does not user the sellers' profiles features and relies exclusively on the buyer's historical interaction to make recommendation.

**Pros:** No domain knowledge needed, as this filter does not use sellers' profiles. This leads to less computational power for our ML algorithm.

**Cons:** If we have few profiles of sellers, then the system can't make accurate reccomendation. This is called a *cold-start* problem as we lack of historical interaction. In addition, this way of filtering can't handle niche interest, although it is personalized as it relies upon similar buyers to make recommendation.

<center>
    <img style="width: 100%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/profile_matching/imgs/filter_compare.png" />
</center>
<figcaption class="img_footer">
    Fig. 6. Comparation table between profile-based filtering and collaborative filtering.
</figcaption>

## Similar Agent-Profile Listing
Let's say that in our SaaS platfomr, after a buyer has clicked on a seller's profile, there are a list of "similar sellers' profiles."  

<center>
    <img style="width: 70%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/profile_matching/imgs/system_4.png" />
</center>
<figcaption class="img_footer">
    Fig. 7. Similar agent-profile listing system diagram.
</figcaption>
</br>

**Assumptions:** The input is the list of sellers' profiles that the buyer is currently viewing (either through manual filtering or selection via click). The output is the ranked list of similar listing the buyer is likely to click on next. This system can be used for both non-logged-in (anonymous) or logged-in buyer.

**Framing problem as ML task:** The sequence of listings that the buyer clicks on usually have similar characteristics, such as sellers who are in the same city or sell the same commodity with acceptable price range. We rely on this observation to define the ML objective: to accurately predict the list of sellers' profiles that the buyer will click next.

**Data Collection:** In the case of the logged-in users, as the both the sellers and the buyers need to log in, there are two ways to collect personal information and preference data: through filtering-tabs or through questionnaires. These questions can be curated by the company's commodity specialist. In the case of anonymous users, we can use the ELK (ElasticSearch, Kibana, Logstash) stack and Mozilla Interaction Observer API to capture users' webapp engagement. Facebook uses this stack for their newsfeed algorithm by analyze user scroll feed. Netflix uses this stack to recommend content based on users' scroll activity. Amplitude, a software company, provides this exact service mainly to extract data for meaningful (business) insight. They provide Amplitude API for developer to create data analytic dashboards which show the users' webapp engagement level. Here are the example of seller, buyer, and interaction databases.

<center>
    <img style="width: 100%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/profile_matching/imgs/buyer_db_2.png" />
    <img style="width: 100%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/profile_matching/imgs/seller_db_2.png" />
    <img style="width: 100%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/profile_matching/imgs/buyer_seller_db_2.png" />
</center>
<figcaption class="img_footer">
    Fig. 8. Examples of Buyer, Seller, Buyer-Seller Interaction databases.
</figcaption>
</br>

**Matching Algorithm:** Instead of making profile recommendation rely on the buyers' historical interaction to understand their long-term interest, we want to use recently viewed listing for more accurate recommendations. This is called session-based recommendation system: Given a sequence of recent sellers' profiles browsed by a buyer, our system will predict the next profile. A good system heavily depends on the user's most recent interactions, not their genetic interests. We build a system by training a model which maps each listing into an embedding vector, so that if two listings frequently co-occur in the buyers' browsing history, their embedding vectors are in close proximity in the embedding space.

<center>
    <img style="width: 50%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/profile_matching/imgs/embed_space.png" />
</center>
<figcaption class="img_footer">
    Fig. 9. KNN for similar seller profile listing.
</figcaption>
</br>

To recommend similar listing, we search the embedding space for listings closest to the ones currently being viewed. In Fig. 9, we choose the top 3 listings with the closest embedding. A simple supervised learning algorithm such as K-Nearest Neighbor (KNN).

## People You Might Know

<center>
    <img style="width: 80%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/profile_matching/imgs/system_5.png" />
</center>
<figcaption class="img_footer">
    Fig. 10. People-you-might-know system diagram.
</figcaption>

**Assumptions:**

**Framing problem as ML task:**

**Data Collection:**

<center>
    <img style="width: 100%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/profile_matching/imgs/buyer_db.png" />
    <img style="width: 100%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/profile_matching/imgs/seller_db.png" />
</center>
<figcaption class="img_footer">
    Fig. 11. Examples of Buyer database and Seller database.
</figcaption>
</br>

**Matching Algorithms:** 

### Pointwise Learning Rank
<center>
    <img style="width: 40%" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/profile_matching/imgs/binary_class.png" />
</center>
<figcaption class="img_footer">
    Fig. 12. Buyer-seller profile-matching classification diagram.
</figcaption>

### Edge Prediction

## Chatbot

**Assumptions:**

**Framing problem as ML task:** Multi-class classification

**Data Collection:**

**Matching Algorithm:** 

## Citation
Cited as:

<blockquote>
    <summary>Nguyen, Minh. (May 2023). Machine Learning for Profile-Matching System.</summary>
    <summary>https://mnguyen0226.github.io/posts/profile_matching/post/.</summary>
</blockquote>

Or 

```sh
@article{nguyen2023mlpm,
  title   = "Machine Learning for Profile-Matching System.",
  author  = "Nguyen, Minh",
  journal = "mnguyen0226.github.io",
  year    = "2023",
  month   = "May",
  url     = "https://mnguyen0226.github.io/posts/profile_matching/post/"
}
```

## References


<center>
    <img class="img_size" src="https://raw.githubusercontent.com/mnguyen0226/mnguyen0226.github.io/main/content/posts/profile_matching/imgs/halongbay.png" />
</center>
<figcaption class="img_footer">
    Fig. 13. Early morning mist at Ha Long Bay, Viet Nam. (Image source: 
    <a href="https://unsplash.com/photos/-HtfdIHSbsE" class="img_footer"> Warren @ Unsplash</a>).
</figcaption>

<!-- CSS Styling -->
<style>
.img_size {
  width: 100%;
}

.img_footer {
    color: #888888;
    text-align: center;
}
</style>