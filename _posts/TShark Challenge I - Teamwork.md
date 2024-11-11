---
layout: post
title: Tshark Part 2
date: 11-11-2024
categories: [notes]
---
**An alert has been triggered:** “The threat research team discovered a suspicious domain that could be a potential threat to the organisation.”

The case was assigned to you. Inspect the provided **teamwork.pcap** located in `~/Desktop/exercise-files` and create artefacts for detection tooling.

**Your tools:** TShark, [VirusTotal](https://www.virustotal.com/gui/home/upload).

Investigate the contacted domains.  
Investigate the domains by using VirusTotal.  
According to VirusTotal, there is a domain marked as malicious/suspicious.

What is the full URL of the malicious/suspicious domain address?

![](https://miro.medium.com/v2/resize:fit:700/1*kWrdlt1bsFS87mgrAJ1x1g.png)

Answer : **hxxp[://]www[.]paypal[.]com4uswebappsresetaccountrecovery[.]timeseaways[.]com/**

When was the URL of the malicious/suspicious domain address first submitted to VirusTotal?

![](https://miro.medium.com/v2/resize:fit:700/1*7j1Gqy_cvSu_vZjaRPam7A.png)

Answer : **2017–04–17 22:52:53 UTC**

Which known service was the domain trying to impersonate?

Answer : **Paypal**

What is the IP address of the malicious domain?

![](https://miro.medium.com/v2/resize:fit:660/1*uI_gNiop07c_VFes2tdSJQ.png)

What is the email address that was used?

![](https://miro.medium.com/v2/resize:fit:700/1*w_kloGuCk3FrS0QdMN80dg.png)

![](https://miro.medium.com/v2/resize:fit:700/1*osdIPWg6dbEolqdTIXUeag.png)

Answer : **johnny5alive[at]gmail[.]com**
