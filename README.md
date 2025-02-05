# Data Enginner

## Problem

The problem: digital media effectiveness

A little bit on digital marketing

Digital Marketing is all about attracting new customers using online tools, such as facebook, google search, LinkedIn, and others. All these platforms provide paid capabilities for companies willing to advertise their products to potential customers. In short, digital marketing is just like traditional marketing but using digital media instead of physical ones (like newspaper, magazines, outdoors). Also, a key difference between them is that with digital media is possible to track user engagement and adjust the marketing strategy accordingly, optimizing the money spent with marketing.

This challenge is about preparing data to analyze digital media effectivenes on our business. If you know nothing about digital marketing that's fine, you're not supposed to and previous knowledge in this matter is not needed. Here are some of the key digital marketing concepts:

Campaign: a marketing campaign is a series of coordinated advertising actions intended to target a specific group of potential customers;
Ad Creative: a graphical image or video that conveys the message being advertised;
Ad Impressions: one single occurrence of displaying an ad to a potential customer;
Clicks: one single click on the ad that leads the customer to the company's website;
Creditas conversion funnel

We can look at the path the customers goes from getting to know our company to converting into a customer as a multi-step process funnel. It is a funnel because for each further step we look, we will progressively find less people involved. The following image illustrates a very simplified version of the conversion funnel we have here at Creditas.

Initially the customer is unaware of our product, the goal of digital marketing is attract potential customers into the conversion funnel. After the customer fills out a lead form (that means he/she is interested), we will run the credit analysis and then formalize the operation signing the contract.

The operation may not be completed by many reasons, such as:

the customer is not approved in credit analysis;
the customer is suspected of being a fraud;
the customer loses interest and quits the process.

## Challenge

There are 4 different datasets to handle and integrate. They are all made up, it's not real data.

google_ads_media_costs.jsonl

This dataset contains ad campaign costs from Google Ads Platform, one json string per line.

Line example:

{
    "date": "2018-10-01",
    "google_campaign_id": 1001,
    "google_campaign_name": "emprestimo_garantia|auto|natal2018",
    "ad_creative_id": 20001,
    "ad_creative_name": "homem_sorrindo_fundo_carro_012",
    "clicks": 3979,
    "impressions": 157767,
    "cost": 20.4
}
facebook_ads_media_costs.jsonl

This dataset contains ad campaign costs from Facebook Ads Platform, one json string per line. It is very similar to the previous, but do not provide the ad creative id information.

Line example:

{
    "date": "2018-10-01",
    "fb_campaign_id": 3001,
    "fb_campaign_name": "emprestimo_garantia|auto|natal2018",
    "clicks": 2265,
    "impressions": 397781,
    "cost": 246.78
}
pageviews.txt

This file comes from the webserver logs and provide pageviews information about a customer visiting our website. It is a purely text file so to extract information from it you have to parse each line and capture just what is needed.

Line example:

'''
203.0.181.219 - [2018-10-01 00:00:00] "GET / HTTP/1.1" 200 http://www.creditas.com.br/emprestimo-com-garantia?ad_creative_id=20003&campaign_id=1002 | device_id: mmRe2Qts07 | referer: http://google.com.br
192.0.5.86 - [2018-10-01 00:00:00] "GET / HTTP/1.1" 200 http://www.bankfacil.com.br/emprestimo-com-garantia?campaign_id=3005 | device_id: i2IJLNavik | referer: http://www.facebook.com
192.14.66.90 - [2018-10-01 00:15:00] "GET / HTTP/1.1" 200 http://www.bankfacil.com.br/emprestimo-com-garantia | device_id: Pk9yEGx715 | referer: https://www.moreira.br/
'''

From the URL address you can find the ad_creative_id and the campaign_id. Also the referer indicates where it came from, whether from Google Ads (http://google.com.br), Facebook Ads (http://www.facebook.com) or organic traffic (anything else).

customer_leads_funnel.csv

This file represents a copy of a analytical table that already exists in our environment.

device_id	lead_id	registered_at	credit_decision	credit_decision_at	signed_at	revenue

'''
3HTZRCZdLc	578419657	2018-10-01 00:00:50	A	2018-10-05 19:37:50		
Mr35TsBJtE	581565131	2018-10-01 00:10:22	D	2018-10-01 10:17:22		
1ZBFWuW5Qd	100080974	2018-10-01 01:32:12	A	2018-10-04 21:00:12	2018-10-07 01:59:12	19340.61
'''

Keep in mind that "lead" is an interested person, which may or may not become a customer. The lead becomes a customer when he/she signs the contract.

Please note that in the column credit_decision, an A stands for Approved and a D stands for Denied. Also, you will notice that even if a customer is approved he/she may give up and don't sign the contract; which, in turn, will generate no revenue.

What the user needs to answer

The digital marketing team is a highly data driven and results oriented team. They need you to prepare the analytical database/tables where they will perform queries to answer the following business questions:

What was the most expensive campaign?
What was the most profitable campaign?
Which ad creative is the most effective in terms of clicks?
Which ad creative is the most effective in terms of generating leads?
What you need to do

Using python and other tools of your choice:

ingest the data in a database;
provide a single table ready to be used to answer the questions above;
provide 4 SQL queries in your README that are answers for each business question presented above;
explain how to reproduce your solution;
We expect you to understand the data, how the datasets fit together and how to best store/represent data to the end data user.

How to deliver your solution

Create a github private repository and grant access to the user marcionetov. Please also reply the original e-mail with the link to this page informing you submitted your solution.

### Pre-requiments and tools

Foram utilizadas as seguintes ferramentas para desenvolver a solução técnica:
* [Anaconda3](https://www.anaconda.com/distribution/) - Main Environment
* [MicrosoftVsCode](https://code.visualstudio.com/) - Development IDE
* [JupyterNotebook](https://jupyter.org/) - Development IDE

Linguagens:
* [Python3.7](https://www.python.org/)
* [ApacheSpark](https://spark.apache.org/)
* [SparkSQL](https://spark.apache.org/sql/)

### execution

* The solution is in a Jupyter Notebook and It was developed as a exploration project. Simple execute each line of the jupyter notebook.

''' Exploration.ipynb'''

* It's important to inform that my objetive is get the result for the 4 main questions. For that, I use only Spark and Python and I create the SQL solution inside de Jupyter notebook.
