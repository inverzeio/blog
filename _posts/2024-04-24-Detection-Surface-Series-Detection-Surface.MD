---
layout: post
title:  "Detection Surface Series 4: Detection Surface"
author: Balazs Greksza
date:   2024-04-24 19:00:00 +0200
categories: detectionengineering, logging
permalink: /blog/:title/
tags: detectionengineering logging
---

![ra2yr_fow_visibility]({{urlimg}}/assets/img/ra2yr_fow_visibility.png)

With some minor detours, we have slowly arrived to the point of `Detection Surface`. Now that we have basically covered hosts, with all of their code, identities, networks, and hardware, the sum of all of the possible attack techniques is quite large - just have a look at the [MITRE ATT&CK Framework](https://attack.mitre.org/).

`Detection Surface` is helpful for us to cluster different pieces of the puzzle for detections.
Unfortunately with the given complexity, it will be very rare to have in-depth understanding of what could go wrong and how every single attack vector can be detected. There are multiple technically possible ways with different success rates.

What's useful to know, is that grouping certain attack types are worthwhile, for detections. Abstractions are often used in Security to help easing the complexity of the security problem, therefore an approach could be, that we of course say the union of all those clusters will be our 
 `Detection Surface: all the network devices logs, servers' and endpoints' telemetry, including runtime and in-line detections/preventions, where it is possible to capture.`

Sometimes custom appliances don't log externally, will not support an agent, to generate any telemetry, and will essentially create a network blind spot. When you meet these formerly "hardened, locked down" - in reality unmanaged and aging - potentially pwned boxes to examine and you need to request a vendor's admin to log into the system remotely to export its logs for you, using a generic admin account - while  `this box is critical in maintaining elements of the security posture` - you realize how bad of a security trade-off and lurking weakness it has been. The last years have been very affluent of cases where many security products have failed. Customers had to regularly do custom, urgent work just to make sure they are not falling victim to simple point-click exploits: frequent patches, run ad-hoc scripts to validate the integrity of the system, and further investigations were often necessary to validate whether or not they have been breached.

Another blurry case that subtracts from the value of the `Detection Surface` is when relevant logs that should be part of the Detection arsenal can only be exported with a delay, for example, from S3 Buckets, in some cases only daily. This creates a delayed possibility for Detection, as instead of using a sliding window of correlated events to monitor, you will have to rely on much more resources to search through larger time scales with greater corpus of logs. This alone may have implications of an unnoticed / very late breach detection.

I would raise the attention, how certain elements are overlapping here, as a hardware firewall / VPN concentrator's memory space is theoretically both part of the physical, and network attack surface, but may be primarily code if it is running as a Virtual Instance.

`The sum of Detections has a lot of unknowns, moving parts, as really there isn't a full transparency in terms of the commercial products built-in methods and telemetry`. A full breakdown as such would constitute something like a per-environment breakdown of built-in vendor detections, network signature capability, honeypots, host based artifacts such as EDR based memory scanning, anomaly detection and log based detection, identities and honey-accounts, additional canary-tokens when used on in-scope applications - all of this is not very easy to converse with, as an explicit breakdown is often not possible, and also would be thousands of lines length at least.

Had that been the case, the playing field would be even more tilted against Defenders.

Even if it's not possible to define easily, we can simplify the discussion with Detection Surface very easily; something along the lines of: we collect 0% < x < 100% of the network telemetry on the supported operating systems of our EDR solution, in combination with the network telemetry of all Internal IPv4 addresses as long as Firewall and DNS logs are covering the entire estate including all network segments.

Attack Surface vs. Detection Surface
--------------------

The difference between the sum of precinct system boundaries, elements or environments (a.k.a. Attack Surface) and the estate / asset type upon which we can observe attacker activity (a.k.a. Detection Surface) is that Attack Surface is representing the habitat misused, Detection Surface is representing the terrain of visibility.

Important to note that the biggest Detection Surface gaps are represented by the unmonitorable, unmanaged, third-party, legacy environments - that should be taken extra care, and safeguarded with even more controls if possible. These IT components will likely present a looming risk and be hard to detect any adversary activity.

Since, it's always better to prevent an attack - and today of course Detection cannot be neglected - however Prevention is something that needs to be focused on first, and implemented methodically to reduce the Attack Surface - with the reduction, we most likely will not impact the Detection Surface, unless we are removing unnecessary systems/components that otherwise also provide their own telemetry.

Strategically, when someone asks what is our Detection Surface, the first thing to start with also should be: what is the understanding of our Attack Surface, and how well has that been reduced?

An interesting distinction is that the Physical attack surface is often covered by Physical security guards, and different detection staffing(security guards vs. security analysts & engineers)
