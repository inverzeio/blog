---
layout: post
title:  "Detection Surface Series: 2) Security Relevancy as an enabler of Visibility"
author: Balazs Greksza
date:   2024-02-01 19:00:00 +0200
categories: detectionengineering, logging
permalink: /blog/:title/
tags: detectionengineering logging
---

Let's consider the following thought experiment: imagine an information system, where we don't use any database for storing information, instead a system, where logging is *replacing* databases, and granular level permissions can be added to logs as well. After every action of an information system, we would create a logline, which may or may not be visible to different users: 
- the application administrator would see everything including the code and the logs
- the logging administrator would see all logs and the code that specifically generates the logs (similar to a DBA in the normal world)
- a group owner would see the actions performed in the group by all accounts, but not others
- the owner of an account would see the actions performed by that account only
- the application would be able to read the logs needed for it's own functionality, but not things that are meant to be private
- the security administrator would be able to see everything in the `security log`
    - security controls added, such as a new MFA device added by a user
    - the salted & hashed values of passwords, 
    - login details of everyone, 
    - known attacks carried out against the system,
    - symmetrically encrypted protected information,
    - fraudulent transactions performed by potentially the same person, using both the initiating user and authorizer user of a payment, connected from the same IP address with only minutes delay
    - new users being created by unusual, highly privileged accounts
    - a library function with a recently discovered vulnerability being called to handle an uploaded file, hence potentially endangering the system integrity.
    - a configuration change that removes a security control, making resources openly accessible
    - a third party API returning unusual, un-sanitized input, due to being trusted by default(when no API input validation -  similar to user input validation - has been implemented)
    - objects being accessed out of ordinary bounds, due to broken access control / object level authorization
    - a known vulnerable piece of the software is being run, and resulting in a permanent connection, and system level access through remote code execution
    - etc.

Now in this experiment, all the security personnel might need of this single system, is always in the `security log` in other words, all `security relevant` actions are logged.

As you might recognize, the point of this experiment was, to highlight, that **information systems in practice are not designed for security visibility**, but primarily for functionality, maintainability etc. Given that we have just demonstrated that one, relatively easy-to-add attribute(last IP Address) is also a code modification in at least 2 places(but what if I want to log for every action? I might want to know if a session is hijacked. Sure, I can bundle everything in a decorator, but the complexity will start to increase), and a Class modification, which potentially result in a DB schema modification as well, is already quite a bit of change.

Implementing logging this way would lead to really terrible performance and also pretty bad security. Logs when aren't indexed are secondary citizens when it comes to speed of search and read/retrieve, accuracy of generation due to fault tolerance, because they are only representations of the source of truth, a single event/transaction, as opposed to a current, valid state, that are typically stored in performant ACID compliant Databases.

For further illustrations only, to calculate the current system state of a similar(but distributed) system e.g. Bitcoin's blockchain, starting from the first block and calculating all transactions for a newly joining miner, just to be able to validate the next transaction, it is somewhere around 1 day's worth of pre-validation computation to get up-to-speed - depending on the rig used - then making one transaction would be between a few minutes to hours depending on transaction confirmation times. This means that system failure of information systems operated would also cause similar amount of downtime.

Value vs. Price
--------------------

Without the understanding of arbitrary black box systems, IT professionals tend to overrate the security value of such system's logs. This is true to third-party managed hardware, virtual appliances, and SaaS as well. In those cases, typically system access to proprietary components is not possible, therefore we only have the envisioned visibility granted by … the aforementioned logs, that are entirely dependent on the application developers' ideas and implementation. 

As security visibility / transparency is often an afterthought, there is has not been enough incentive for managed hardware/software providers to implement extensive logging practices, creating massive volume of logs, especially, when hosted by the service provider - these are extra costs to the operation of every single instance of a service. Don't believe me? Take a look at the [Audit Logs Wall of Shame](https://audit-logs.tax).

The difficulty of today's security landscape, is that the industry still hasn't found any enforcement of certain level and style of logging, that would be easy to be combined with other log sources, and would employ all-around uniformity.
We might be mixing Syslog with CEF formatted logs, OSQuery or Sysmon, and Identity provider logs with random Application logs, that are not only entirely different, but can be absolutely non-standard as well.


Don't you dare doxxing me dev
--------------------

Going back to our example, the Open Source Web Application Security Project(OWASP) is actually defining quite well what **not** to log:

{% highlight ruby %}
"The following should usually not be recorded directly in the logs, but instead should be removed, masked, sanitized, hashed or encrypted:

- Application source code
- Session identification values (consider replacing with a hashed value if needed to track session specific events)
- Access tokens
- Sensitive personal data and some forms of personally identifiable information (PII) e.g. health, government identifiers, vulnerable people
- Authentication passwords
- Database connection strings
- Encryption keys and other master secrets
- Bank account or payment card holder data
- Data of a higher security classification than the logging system is allowed to store
- Commercially-sensitive information
- Information it is illegal to collect in the relevant jurisdictions
Information a user has opted out of collection, or not consented to e.g. use of do not track, or where consent to collect has expired

Sometimes the following data can also exist, and whilst useful for subsequent investigation, it may also need to be treated in some special manner before the event is recorded:
- File paths
- Database connection strings
- Internal network names and addresses
- Non sensitive personal data (e.g. personal names, telephone numbers, email addresses)"

{% endhighlight %}

Reference: [OWASP Logging Cheat  Sheet](https://cheatsheetseries.owasp.org/cheatsheets/Logging_Cheat_Sheet.html)

Without going much deeper into logging, we can acknowledge, that the best practice is simply  **not** to log everything, and partially, for good reasons.

This is the second post of the series, check out rest:

[Detection Surface - Loggable to Detectable](https://inverze.io/blog/detection-surface-series-loggable-to-detectable/)
