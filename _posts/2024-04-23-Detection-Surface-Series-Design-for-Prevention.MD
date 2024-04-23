---
layout: post
title:  "Detection Surface Series 3: Design for Prevention Avoid Detecting Entirely"
author: Balazs Greksza
date:   2024-04-23 23:30:00 +0200
categories: detectionengineering, logging
permalink: /blog/:title/
tags: detectionengineering logging
---

--------------------
Software Architecture and Development Process considering Prevention
--------------------
![nist_sscs_sbom]({{urlimg}}/assets/img/nist_guidance_software_supply_chain_security.png)

Responsible Application Architects, whom are thinking about following a very healthy application development process, might consider to perform automatic testing baked into the CI/CD Pipeline, such as:
- Static Application Security Testing (SAST), 
- Dynamic Application Security Testing (DAST), 
- Out-of-band Application Security Testing (OAST)

In modern AppSec programs we should also find:
- Threat Modeling prioritized to be perfected throughout the SSDLC, considering the final Business Logic, Security Value and
- Runtime Application Self-Protection (RASP) for those experimenting with cutting-edge tech.

Any Security Engineer would also like to have some good sleep knowing they have configured well the Compute resources their applications are running on(regardless of bare metal, VM, containers or functions), so let's not forget about securing them as well:
- Managing Infrastructure state with Infrastructure-as-Code(IAC), 
- Hardening,
- Offensive security testing and
- Continuous Patch and Vulnerability Management also comes to mind at very least, but also not forgetting about Package Validation, Container Registries etc.

Did you hear anyone saying AppSec is easy? 

Now how is this all relevant to our topic of discussion?


Attack Surface as a Byproduct of Code
--------------------

Attack Surface is defined by NIST as: `The set of points on the boundary of a system, a system element, or an environment where an attacker can try to enter, cause an effect on, or extract data from, that system, system element, or environment.`

Notice how all elements in the last sections play a role of what type of attacks are possible to be carried out, are visible, when carried out, are already protected against, logged and detectable, and what aren't.

1. If we haven't performed SAST, we might have some hardcoded tokens, SSH keys, certificates, passwords, or vulnerabilities
2. If we haven't conducted a Threat Modeling, we might have missed critical possibilities of say Tampering with the application data
3. If we don't do Offensive security testing, we might be missing potentially exploitable details, that are only discovered after finding a chain of functions or a Logical Bug
4. Newly discovered Vulnerabilities while relying on underlying libraries are constantly undermining the security of a single system. Whilst they exist silently, they may be mitigated by not being fully exposed / known to the public.
5. If we don't log(which no-one does) when a vulnerable function is being executed, we won't see when it's misused(almost never do, at least, not directly). The systems might contain artifacts that indicate them, but artifacts are up for grabs for specialist *forensicators*, and hidden from regular security monitoring personnel
6. … we can imagine many more examples 

These all are adding up to what we call the Attack Surface of a single web application.

We should also repeat the whole exercise to operating systems, our providers should for the cloud services we use and so on.

Running or Callable Code(Application) Attack Surface
--------------------

Probably the broadest Attack surface of all, considering the Lines of Code(LoC) and corresponding vulnerabilities present in every information system nowadays. Widely talking about it, code may be inherently vulnerable if implemented with a flaw - and software flows are unavoidable. 

Of course there are great improvements with memory safe languages, live, IDE-embedded code recommendations, and AI tools, but refactoring still remains a massive problem, not to mention some of the inherent architectural issues explained in [the thirty million line problem](https://www.summarize.tech/youtube.com/watch?v=kZRE7HIO3vk)

Not all mistakes in software are equal, some of them are more of logical bugs resulting in incorrect results, but there is a big category of bugs that also present an immediate misuse or malice - this is the security relevant, vulnerable code.

However, there needs to be a distinction made between code that's actively running(more accurately: it's bytecode, p-code or interpreted code translated to machine code) and is frequently executed by the CPU, code, that can be called and code, that's being installed, but rarely or never used(as part of installed packages or binaries) or require a non-trivial interaction that is not possible with no-low privileges. Both structured software testing and fuzzying can trigger some elements of infrequently run code, that is unusual by normal use.

Code constitutes the largest category with many overlaps, as many network protocols are essentially implemented as code, even if in lower levels of the networking model they travel through physical mediums, or lead to for example the misuse of unproperly handled memory leading to memory corruption or resulting in code injection that changes the CPU's program execution flow to unintended paths. Hence the line is a bit blurry, and often even overlap, but these contemplations are still useful, to simplify the terminology.  


Identity Attack Surface representing People or Services
--------------------

While strictly speaking Identities in the Digital Realm also only representatively exist as some digital forms(bits) in a Database or "Identity Directory", Identities in modern environments often provide entry points through SSO for simple reuse to numerous IT systems / applications, and with multiple ongoing trends - the disappearance of the "simple" Perimeter security defense boundary, Remote Work with the use of VPNs, temporary gig workers, BYOD devices, Zero Trust - many security professionals consider Identities as the new Perimeter - the last well controllable point, that is worth mentioning. This is why the significance of IAM programs have arisen in the past years.

Network Attack Surface
--------------------

Network Security is one of the oldest contributor to the Attack Surface, as there are still a lot of insecure by design, and legacy protocols, permissive configurations that all can contribute to a widened network attack surface, not to mention the Denial of Service type attacks to consider availability as well - essentially anything "connected" with a Network Address(typically IP but others as well) or Domain is contributing to be part of the Attack surface.

While not mentioned separately elsewhere, but considering it's importance today: Email Security could be considered in this category, as the delivery mechanism is over a network, even if more asynchronous in it's nature of payload delivery and execution - instead of a malicious web requests being made - a cannon shooting through air, think of phishing emails as a form of a grenade thrown with an intact pin. The medium of email(and any other social/communication platform used for file delivery) is getting through is still through the use of several network protocols.

Physical Attack Surface
--------------------

Physical hardware also contribute to the risks - for Data Centers these risks are typically more mature to be safeguarded against, and due to the nature of the attack and resulting repercussions are a good deterrent nowadays. The physical location of some systems may not be known exactly, making it useless to carry out targeted probes. However, some hardware might be directly accessible such as for IoT devices, and shared and can be directly attacked, some are very static OT/IIoT environments, Third-party connections/Extranets, VPNs, etc.

Hardware may also be directly vulnerable due to it's physical architecture and logic, or by low-level software running on it.

This is the third post of the series, check out rest:

[Detection Surface Series 1: Loggable to Detectable](https://inverze.io/blog/detection-surface-series-loggable-to-detectable/)
[Detection Surface Series 2: Security Relevancy](https://inverze.io/blog/detection-surface-series-security-relevancy/)
