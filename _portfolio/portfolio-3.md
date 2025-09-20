---
title: "Churn Prediction for B2B Manufacturing"
excerpt: "Churn prediction project for a B2B manufacturing education platform"
collection: portfolio
---

# About Me
Churn Prediction for B2B Manufacturing EdTech

---

## Project Summary

**Client:** A platform that stores and organizes educational videos and materials for amateurs in the manufacturing industry.  

**Business model:** Manufacturing companies subscribe to the platform through monthly subscriptions.  

**Project goal:** Reduce churn rate among existing subscribed customers.  

**Solution:**
- Build a model to predict the churn rate of existing customers  
- Enable the internal marketing/sales team to actively engage customers with the highest predicted churn rate  
- Prioritize customer engagement based on churn risk ranking  

---

## My Contribution
- Conducted requirements analysis  
- Extracted and cleaned raw data from the CRM platform  
- Performed EDA and cohort analysis  
- Transformed fields and created new variables:  
  - **Frequency**: Engagement rate calculated by dividing access count by the number of unique amateur users  
  - **Recency**: Time since the last user activity (monthly)  
  - **Video Rate**: Number of educational videos uploaded (monthly)  
  - *Example:* Created a recency metric by calculating the time between the last activity date and the current month  
- Built a Gradient Boosting model with these three variables  

---

## Thoughts
A lot of time was spent on:  
- Identifying the right requirements  
- Running analysis in parallel while uncovering business needs  

Specifically, the business lead needed to define which issues to scope and how they could improve overall sales.  

It was also mentioned that being on-site would have allowed deeper issue discovery and more direct application of data science experience.  

---

## Gallery
**Dashboard view**  
<img src="/images/gallery.png" alt="Dashboard view" />
