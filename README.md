# Swiggy Ads CTR Prediction & Sponsored Restaurant Ranking System

## Overview
This project builds an end-to-end machine learning system to predict click-through 
rate (CTR) for sponsored restaurant ads and rank them using a bid-aware optimization 
strategy. The system is inspired by real-world ad platforms like Swiggy Ads and focuses 
on balancing advertiser revenue with customer experience.

---

## Business Problem
Food delivery platforms display sponsored restaurant ads across home and search pages. 
If ads are poorly ranked, it leads to low engagement, wasted advertiser spend, and 
degraded user experience.

The challenge is to rank sponsored restaurant ads such that users are more likely to 
click, while also ensuring fair monetization for advertisers.

---

## Objective
- Predict the probability that a user will click on a sponsored restaurant ad
- Rank ads using a revenue-aware optimization strategy
- Improve engagement without negatively impacting customer experience

---

## Dataset Design
Due to proprietary restrictions on real Swiggy ads data, a synthetic dataset was created 
to simulate realistic sponsored restaurant ad interactions.

The dataset models:
- User context (time of day, cuisine preference)
- Restaurant attributes (rating, distance, price range)
- Ad-specific signals (bid amount, discount)
- User interaction outcome (clicked / not clicked)

Click behavior is generated probabilistically based on relevance and incentives.

---

## Feature Engineering
Key features include:
- Cuisine match between user and restaurant
- Distance as a proxy for delivery friction
- Restaurant rating as a quality signal
- Time-of-day to capture user intent
- Discount and bid amount as ad-related signals

These features help capture both relevance and monetization aspects of ads.

---

## Modeling Approach
A baseline Logistic Regression model was trained to establish performance benchmarks.
Due to its linear nature, it failed to capture complex feature interactions.

An XGBoost classifier was then used to model non-linear relationships between user context, 
restaurant attributes, and ad signals, resulting in improved ranking performance.

---

## Evaluation Strategy
Accuracy was avoided as it is not suitable for ranking-based ad systems.

The model was evaluated using:
- AUC-ROC for ranking quality
- Log Loss for probability calibration
- Precision@K to measure relevance of top-ranked ads

---

## Ad Ranking Strategy
Predicted CTR scores are combined with advertiser bid values to compute a final ranking score:

Ranking Score = Predicted_CTR × Bid_Amount

Top-K ads are selected per user session, balancing relevance and monetization.

---

## Experimentation
An offline A/B testing simulation was conducted:
- Control group: Random ad ranking
- Treatment group: ML-based ranking

The treatment group showed improvement in CTR and expected ad revenue, validating the 
effectiveness of the approach.

---

## System Design (High-Level)
1. Fetch candidate sponsored restaurants
2. Generate real-time and historical features
3. Predict CTR using trained model
4. Apply bid-aware ranking logic
5. Serve top-K ads within latency constraints

---

## Limitations
- Synthetic dataset
- Offline evaluation only
- No real-time feedback loop

---

## Future Improvements
- Integrate real clickstream data
- Deploy real-time inference service
- Add deep learning–based ranking models
- Implement monitoring and retraining pipelines
