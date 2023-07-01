---
layout: post
title:  "Book Review - Incident Response Techniques for Ransomware Attacks"
author: Balazs Greksza
date:   2022-05-09 00:00:00 +0000
categories: ransomware, book
permalink: /blog/:title/
tags: book ransomware
---

> **A comprehensive Ransomware Tactics summary with a wealth of Digital Forensics insights** 🔍<br>
<a href="https://www.amazon.com/dp/B09VCM6FWD?&linkCode=li3&tag=&linkId=52bf9eccbdb4c815b8830f55ade481f3&language=en_US&ref_=as_li_ss_il" target="_blank"><img border="0" src="//ws-na.amazon-adsystem.com/widgets/q?_encoding=UTF8&ASIN=B09VCM6FWD&Format=_SL250_&ID=AsinImage&MarketPlace=US&ServiceVersion=20070822&WS=1&tag=&language=en_US" ></a><img src="https://ir-na.amazon-adsystem.com/e/ir?t=&language=en_US&l=li3&o=1&a=B09VCM6FWD" width="1" height="1" border="0" alt="" style="border:none !important; margin:0px !important;" />
 
Understand modern ransomware attacks and build an incident response strategy to work through them - by Oleg Skulkin
--------------------

In the first chapter we find some interesting insights about the history of human operated ransomware groups, their recent activities, tooling, and a high level overview of how different groups were associated with each other. Also a brief summary of the famous indictments - the cases that have been solved and linked to a known individual or group.

Then, we get a good introduction of the NIST Cyber Incident Process and later the author's take on how does it apply to several high profile cases. Oleg Skulkin goes in a quite long, yet well condensed summary of a number of different campaigns, their most commonly used **tactics, techniques and procedures(TTPs).** Although, this may not be new to seasoned threat intelligence experts, it definitely gives a lot of different insights to aspiring security professionals, including **MITRE ATT&CK® explanations as well the described tradecraft.** Obviously a book of this volume cannot go into the very in-depth analysis of each campaign, but the external references provide a very good opportunity to dive deeper.

One can argue, that parts of the content can be found in the reports alone, however, it is still convenient to have the whole arsenal of TTPs collected.

> **This part is definitely the highlight of the book - a very valuable armory addressed to cybersecurity practicioners learning to combat ransomware. It also endows the reader with intimate knowledge of the inner workings of Ransomware operations.**

The second most insightful part of the book starts with the Practical IR at Chapter 7. This gives a **good overview of the Digital Forensics techniques** that can be used to obtain evidence, the key artifacts, and **plenty of the tools in professionals use**. Every new topic starts with explanations that are welcoming for the novice readers as well.

Overall, the DFIR artifact session is a good intro / refresher for all (except pro) levels of practitioners. This can be obviously discussed in volumes, so most are mentioned, but the reader should definitely do some additional digging to acquire fluency with the artifacts - they span from **Event logs to $MFT, from shellbags to volatile memory.**

The Investigation chapters then break down most common (human operated or else automated) techniques, that can be used to investigate not just ransomware type of security incidents. Again, great to see a summary that Security Engineers and Analysts can use to understand a wider variety of attacks.

The book does a very good job at showcasing a lot of different techniques in detail, with ransomware-relevancy. Most of the times the evidence presented are easy to be interpreted, however, sometimes the conclusions drawn are one-liners, where we have to believe that the conclusion is correct - which is easy, because the author presents the evidences in a very factual way.

The Post-Exploitation, Data Exfil and Deployment techniques are definitely giving great insights, on where you should focus your investigation efforts when putting the puzzle pieces together - it is easy to forget about some of those artifacts. 

The book closes with explaining how the different models(Cyber Kill®, MITRE ATT&CK®, The Unified Kill Chain) lead to the **Unified Ransomware Kill Chain** - which is **a novelty by the author - it signifies the repeated nature of Key Assets discovery, Network Propagation, Data Exfiltration in the Kill Chain.**

The book is well written, and for seasoned infosec professionals will be a relatively easy read with plenty of good reminders on subjects, some informative statistics,  external references, and a revised killchain.

The recommendation for a second edition or part II, would be to expand more on the possibilities for using decryptors, typical response scenarios, and proactive mitigation - however it is tough to fill so much information in just one book.


Chapters:
--------------------
 
1. The History of Human-Operated Ransomware Attacks
2. The Life Cycle of a Human-Operated Ransomware Attack
3. The Incident Response Process
4. Cyber Threat Intelligence and Ransomware
5. Understanding Ransomware Affiliates' Tactics, Techniques, and Procedures
6. Collecting Ransomware-Related Cyber Threat Intelligence
7. Digital Forensic Artifacts and Their Main Sources
8. Investigating Initial Access Techniques
9. Investigating Post-Exploitation Techniques
10. Investigating Data Exfiltration Techniques
11. Investigating Ransomware Deployment Techniques
12. The Unified Ransomware Kill Chain


| Title                 | **Incident Response Techniques for Ransomware Attacks**                                               |
|-----------------------|-------------------------------------------------------------------------------------------------------|
| Subtitle              | **Understand modern ransomware attacks and build an incident response strategy to work through them** |
| Author                | **Oleg Skulkin**                                                                                      |
| ISBN                  | **978-1803240442**                                                                                    |
| Date of publication   | **March 2022**                                                                                        |
| Number of pages       | **307**                                                                                               |
| Format                | **eBook/Kindle, Paperback**                                                                           |
| Amazon Affiliate Link | [https://amzn.to/3yn6l09](https://amzn.to/3yn6l09)                                                    |
| Resources             | **No additional software included**                                                                   |

<iframe sandbox="allow-popups allow-scripts allow-modals allow-forms allow-same-origin" style="width:120px;height:240px;" marginwidth="0" marginheight="0" scrolling="no" frameborder="0" src="//ws-na.amazon-adsystem.com/widgets/q?ServiceVersion=20070822&OneJS=1&Operation=GetAdHtml&MarketPlace=US&source=ss&ref=as_ss_li_til&ad_type=product_link&tracking_id=&language=en_US&marketplace=amazon&region=US&placement=B09VCM6FWD&asins=B09VCM6FWD&linkId=e1172c71ace727b9ce52566785197bb6&show_border=true&link_opens_in_new_window=true"></iframe>

