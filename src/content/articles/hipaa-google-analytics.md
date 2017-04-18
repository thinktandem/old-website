---
layout: layouts/article.html
title: "Google Analytics and HIPAA"
tags: strategy, analytics, health-tech
permalink: true
author: Alec Reynolds
private: false
mainImage: images/articles/linter-is-coming/linteriscoming.jpeg
img-src: images/articles/linter-is-coming/linteriscoming.jpeg
teaser: Google Analytics provides great metrics. But by enabling tracking of information like gender, age, location, and other metrics, are you violating HIPAA?
date: 2017-03-15
---

## Question 1: Can I Use Google Analytics on a Site Governed By HIPAA?

It depends.

Let's break this down: a "site governed by HIPAA" is one that stores Protected Health Information (PHI). PHI is what happens when personally identifiable information (information like address, name, SSN, phone number...anything that can tell you who someone is) makes data love with health information (details on doctors visits, hospital stays, procedures performed, even insurance options).

These terms are defined fairly broadly. For example, technically _health information_ is defined by HIPAA as consisting of "any information, whether oral or recorded in any form or medium, that–

(A) is created or received by a health care provider, health plan, public health authority, employer, life insurer, school or university, or health care clearinghouse; and

(B) relates to the past, present, or future physical or mental health or condition of any individual, the provision of health care to an individual, or the past, present, or future payment for the provision of health care to an individual.”

This is kind of scary. If you're a covered entity, essentially ALL of the information you're creating is health information! Just combining two fairly minor pieces of information -- say an appointment time and a phone number -- would create PHI.

## Figure Out if Google Analytics is Storing PHI.

As a rule of thumb, a default configuration of Google Analytics shouldn't be including _any_ PHI by default. For the most part, usage data (what pages people viewed and when) won't be personally identifiable, nor will it include health information.

However, be careful to configure to avoid these obvious exceptions:

### IP Addresses

A specific IP address is tantamount to PII: it's fairly easy for you to tell who someone is if you have their IP. If that IP is combined with browsing history that could indicate health services provided or insurance selections, then BOOM: you've created PHI.

Fortunately, there are two easy solutions here. First, make sure your URLs don't include any explicit references (or even hints) to health information. Second, enable [IP Masking](https://support.google.com/analytics/answer/2905384?hl=en) in Google Analytics, which makes sure Analytics doesn't store the entire IP address. Don't worry! You can still use GA's IP Geolocation service to get a rough idea where users come from and improve your knowledge of your userbase.

### URLs with Health Information

This is a tricky area: make sure that none of your site's URL routes include references to health information. For example, let's say we have a tracking program for diabetics on our site and these are potential URLs for the user profile page:

The _wrong_ way: www.mygreathealthtracker.com/diabetes-tracker/user/robbie-reynolds

The _right_ way: www.mygreathealthtracker.com/diabetes-tracker/user/89438383943

In the incorrect example, we can clearly see that Robbie is participating in the Diabetes Tracking program. That fact is PHI and should never be entrusted to a third-party vendor like Google Analytics who we don't have a BAA with.

The correct example obfsucates _who_ is participating. As long as we aren't tracking PII alongside this URL (like a specific IP address, email, name, etc.), then we should be safe storing this information, since we have no idea _who_ the person is.

### Page Titles

This is a biggie. GA by default tracks your page titles, which can easily include PHI. Think something as innocuous as "Robbie's Diet Log": combining name and health information in one fell swoop!

The surefire solution: instead of including the GA tracking code on your pages, create an iframe within the page and put the code within there. That way it gets loaded on every page load, but doesn't include some of this extra info. --> NEED MORE INFO

### Custom Data Tracking

On that note, Google Analytics allows us to track custom data that could potentially create PHI. For example, if you've created a custom tracker that records the user's company, age, and gender, combining that information with our last example's obfsucated URL would constitute PHI.

### Event Tracking

So what if we only collect PII (take our last example of company/age/gender) on specific events, like when a user purchases an item or undergoes another conversion event we're tracking in GA? Isolated by itself, that information may not be PHI, but if it can be associated with health information by looking at the user's browsing history, we have a problem.

## Recommendations

### 1. Enable IP Masking

Easy win: prevent IP from being PII.

### 2. Obfsucate all URLs to eliminate ANY PII

This can be a little harder (it is nicer to have human-readable URLs), but in most instances where we reference a user or details about a user, it's easy for us to substitute a unique ID that's specific to our system.

### 3. If possible, obfsucate URLs to eliminate references to health information.

This may not be possible: usability definitely decreases if replace words like "diabetes-tracker" in our URLs with "service/5913". However, this can be a good way to further reduce risk.

### 4. Never track "complete" PII in custom trackers.

IE, make sure that combinations of data (like company + age + gender) aren't present that could constitute PII. Just tracking gender and company, or just tracking age and gender, could be acceptable.

## Conclusions

Using Google Analytics on a site with PHI can be done, but you must seriously evaluate _every_ piece of information stored by GA. Replacing health information and PII with IDs unique to your system is a great way to get around this. If you (or your boss or attorney) are worried about the information you're storing, check out [this resource](
https://www.hhs.gov/hipaa/for-professionals/privacy/special-topics/de-identification) from the Department of Health and Human Services that shows how to de-identify PHI to make it acceptable for storage in an environment like Google Analytics.



## Further Reading

- [Updating Your Privacy Policy to Use Google Analytics](http://www.iubenda.com/blog/privacy-policy-google-analytics/)
- For more information on _how_ Google handles the security of information for Analytics, see [this article.](https://support.google.com/analytics/answer/6004245).
- [Good StackOverflow Question](http://security.stackexchange.com/questions/14459/is-google-analytics-hipaa-compliant-how-can-i-find-out)
- [Summary of What Google Analytics Tracks](http://www.lunametrics.com/blog/2016/06/22/google-analytics-collects-information/)
- [Hacking Healthcare](http://shop.oreilly.com/product/0636920020110.do): Great into to IT in healthcare, including a ground-up approach to understanding HIPAA.
- [Best Practices to Avoid Sending PII in GA](https://support.google.com/analytics/answer/6366371)






## HIPAA is About Governing PHI

You don't want people just passing around information about your health flipplantly. That's why the feds passed the Health Insurance Portability and Accountability Act (HIPAA) back in the '90s. Protected Health Information.
What is PHI?


## The Key: Don't Store PHI.

Most of the metrics we care about for users isn't related to their health coverage.

If you (or your boss/attorney) is worried about the information you're storing, check out [this resource](
https://www.hhs.gov/hipaa/for-professionals/privacy/special-topics/de-identification) from the Department of Health and Human Services that shows 



## Never Store PHI on a Service Without a BAA




