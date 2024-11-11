---
layout: post
title: Tshark Part 3
date: 11-11-2024
categories: [notes]
---
# Introduction

This room presents you with a challenge to investigate some traffic data as a part of the SOC team. Let’s start working with TShark to analyse the captured traffic. We recommend completing the [TShark: The Basics](https://tryhackme.com/room/tsharkthebasics) and [TShark: CLI Wireshark Features](https://tryhackme.com/room/tsharkcliwiresharkfeatures) rooms first, which will teach you how to use the tool in depth.

> Start the VM by pressing the green **Start Machine** button in this task. The machine will start in split view, so you don’t need SSH or RDP. In case the machine does not appear, you can click the blue **Show Split View** button located at the top of this room.

**NOTE:** Exercise files contain real examples. **DO NOT** interact with them outside of the given VM. Direct interaction with samples and their contents (files, domains, and IP addresses) outside the given VM can pose security threats to your machine.

# Case: Directory Curiosity!

**An alert has been triggered:** “A user came across a poor file index, and their curiosity led to problems”.

The case was assigned to you. Inspect the provided **directory-curiosity.pcap** located in `~/Desktop/exercise-files` and retrieve the artefacts to confirm that this alert is a true positive.

**Your tools:** TShark, [VirusTotal](https://www.virustotal.com/).

# Answer the questions below

_Investigate the DNS queries.  
Investigate the domains by using VirusTotal.  
According to VirusTotal, there is a domain marked as malicious/suspicious._

> What is the name of the malicious/suspicious domain?

_(Enter your answer in a_ **_defanged_** _format.)_

![](https://miro.medium.com/v2/resize:fit:1000/1*ST0j7SnQTGCPunRFE---CQ.png)

Correct Answer — **jx2-bavuong[.]com**

> What is the total number of HTTP requests sent to the malicious domain?

![](https://miro.medium.com/v2/resize:fit:1000/1*Qf5XHAonQyPpS0ue95zekg.png)

Correct Answer — **14**

> What is the IP address associated with the malicious domain?

_(Enter your answer in a_ **_defanged_** _format.)_

![](https://miro.medium.com/v2/resize:fit:1000/1*VNq7HTUdHGIW2zhUVT4JrQ.png)

Correct Answer-**141[.]164[.]41[.]174**

> What is the server info of the suspicious domain?

![](https://miro.medium.com/v2/resize:fit:1000/1*6XA95UBkRdM1RpvCn9OslQ.png)

Correct Answer — **Apache/2.2.11 (Win32) DAV/2 mod_ssl/2.2.11 OpenSSL/0.9.8i PHP/5.2.9**

## Follow the “first TCP stream” in “ASCII”.  
Investigate the output carefully.

> What is the number of listed files?

![](https://miro.medium.com/v2/resize:fit:1000/1*LQtpoAjH7E5ld6F3-no2Lg.png)

Correct Answer — **3**

> What is the filename of the first file?

_(Enter your answer in a_ **_defanged_** _format.)_

Correct Answer — **123[.]php**

> Export all HTTP traffic objects.

> tshark -r directory-curiosity.pcap — export-objects http,/home/ubuntu/Desktop/exercise-files -q

- **r directory-curiosity.pcap:** Reads the packet capture file named directory-curiosity.pcap.
- **— export-objects http,/home/ubuntu/Desktop/exercise-files:** Extracts and saves all HTTP objects (e.g., files like images, documents) from the packet capture. These objects are stored in the directory /home/ubuntu/Desktop/exercise-files.
- **-q:** Runs tshark in quiet mode, suppressing the usual packet summary output.

> What is the name of the downloaded executable file?

_(Enter your answer in a_ **_defanged_** _format.)_

![](https://miro.medium.com/v2/resize:fit:1000/1*joAsqVYcQKJ_3nwmlkKoAA.png)

Correct Answer — **vlauto[.]exe**

> What is the SHA256 value of the malicious file?

![](https://miro.medium.com/v2/resize:fit:1000/1*Yr0EXql62TpHwQjiK6J2Ug.png)

**_sha256 file_name_ (just type in the terminal)**

Correct Answer — **b4851333efaf399889456f78eac0fd532e9d8791b23a86a19402c1164aed20de**

## Search the SHA256 value of the file on VirtusTotal.

> What is the “PEiD packer” value?

![](https://miro.medium.com/v2/resize:fit:1000/1*0VvQxYK3wM2qBmuRNbtPXA.png)

Correct Answer — **.NET executable**

## Search the SHA256 value of the file on VirtusTotal.

> What does the “Lastline Sandbox” flag this as?

![](https://miro.medium.com/v2/resize:fit:700/1*Vm23eDA82RaQJ2xfw1Ls9g.png)

Correct Answer — **MALWARE TROJAN**
