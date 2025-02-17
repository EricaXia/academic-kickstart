---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Tracking Health and Nutrition Signals from Social Media Data"
summary: ""
authors: []
tags: ['NLP', 'Social Media', 'Web Scraping', 'Data Analysis', 'Spatial Analysis', 'Modeling']
categories: []
date: 2020-03-28T10:42:05-08:00

# Optional external URL for project (replaces project detail page).
external_link: ""

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: "Smart"
  preview_only: false

# Custom links (optional).
#   Uncomment and edit lines below to show custom links.
# links:
# - name: Follow
#   url: https://twitter.com
#   icon_pack: fab
#   icon: twitter

url_code: ""
url_pdf: ""
url_slides: ""
url_video: ""

# Slides (optional).
#   Associate this project with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides: ""
---
<!-- 
![](https://github.com/EricaXia/shelter/raw/master/imgs/rescue-animals-and-shelter-pups.jpg) -->
### Instgram Web Scraping and Data Analysis Project
#### Center for Knowledge-Powered Interdisciplinary Data Science (CKIDS) at USC
Project Advisors:  
<br />
Professor Andrés Abeliuk, Information Sciences Institute, USC  
<br />
Dr. Abigail Horn, Postdoctoral Fellow, Preventive Medicine, USC


---
**Description:** 
Social media provides an abundance of data for diet and nutritional behaviors. We are interested in whether social media data from Instagram serves as a reliable indicator into nutrition and dietary health despite implicit biases (self-presentation and self-selection).

**Research Questions:** 
- How can we analyze population dietary trends with 2020 Instagram data? 
- How does the nutritional content of food posts vary by geography and and hashtag associations?
- What new insights on population health and nutrition trends can be obtained by studying image and spatial data?


---

#### Table of Contents

1. [Background and Motivation](#1-background)
2. [Web Scraping](#2-web-scraping)
3. [Data Visualization](#3-data-visualization)
4. [COVID-19 Effects](#4-covid-19-effects) - Changes in population dietary behavior due to COVID-19 Crisis

---

## 1. Background 

<br />

![](https://github.com/EricaXia/academic-kickstart/raw/master/content/project/ckids/food-photo.jpg)

Official public health estimates population-level nutritional quality and patterns come from self-report survey data based on small samples and provide coarse surveillance measures; the best available data source in Los Angeles employs a sample population on the order of 5,000 LA residents to provide a limited set of diet/nutrition variables such as frequency of fruit and vegetable consumption and fast food consumption. Social media data suffers from multiple important biases including self-presentation and self-selection, but provides information that survey data cannot: it is at a large population scale, can provide sentiment information, and demonstrate social components including likes, follows, and behavior clustering. Using an Instagram dataset of all geo-located posts at food outlets in Los Angeles for 3 months in 2014, this project will investigate whether Instagram posts, despite implicit biases (and to the extent possible, accounting for these biases), can provide a representative health signal, informative of the quality of population nutrition and dietary patterns at a highly-resolved (e.g. census tract level) spatial scale. 

<br />

There is an ongoing discourse in public health fields regarding the validity of social media data for diet and nutritional behavior surveillance, and how it compares to official measures, and/or what we can learn from this data that has practical health significance, but to date these research questions have not been investigated directly (largely out of a general disbelief of its utility). Therefore regardless of whether this project finds strong or weak indications, the work will contribute to the ongoing conversation on whether or not social media data can provide a signal into nutrition and dietary health. 

<br />
<br />

## 2. Web Scraping

**Approach and Methodology: **
- Obtaining the dataset from Instagram: Web scraping with Python tools

We start scraping Instagram by specific hashtags (#burger, #foodie, #kale, and more). We get metadata from each post including:

- Post description, additional hashtags, comments, number of likes
- Food outlet location
- Timestamp
- Image
- Poster's profile info
- Social data
  - Usernames + comments for top 50 commenters
  - Usernames for top 50 likes




<br />

## 3. Data Visualization


### 3.1 Natural Language Processing - Hashtag Analysis

![](https://github.com/EricaXia/academic-kickstart/raw/master/content/project/ckids/biweek_11__wordcloud.png)

![](https://github.com/EricaXia/academic-kickstart/raw/master/content/project/ckids/loc_march_top20_hashtags.png)

### 3.2 Spatial Analysis

![](https://github.com/EricaXia/academic-kickstart/raw/master/content/project/ckids/worldmap.png)


## 4. COVID-19 Effects
***Under construction: coming Soon***



<!-- - Image recognition and image analysis to analyze nutritional content
- Social network analysis (track friendship networks by Instagram follow-backs) -->

<!-- {{< figure library="true" src="heroku.png" lightbox="true" >}} -->