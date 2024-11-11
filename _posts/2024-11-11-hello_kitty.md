---
layout: post
title: Hello Kitty
date: 11-11-2024
categories: [documentation]
tag: [like]
---
### Command-Line Wireshark Features I | Statistics

>At the beginning of this module, we mentioned that TShark is considered a command line version of Wireshark. In addition to sharing the same display filters, TShark can accomplish several features of Wireshark explained below.

**Three important points when using Wireshark-like features:**

- These options are applied to all packets in scope unless a display filter is provided.
- Most of the commands shown below are CLI versions of the Wireshark features discussed in [Wireshark: Packet Operations](https://tryhackme.com/room/wiresharkpacketoperations) (Task 2).
- TShark explains the parameters used at the beginning of the output line.

- For example, you will use the `phs` option to view the protocol hierarchy. Once you use this command, the result will start with the "**P**acket **H**ierarchy **S**tatistics" header.

|   |   |
|---|---|
|**Parameter**|**Purpose**|
|--color|- Wireshark-like colourised output.<br>- `tshark --color`|
|-z|- Statistics<br>- There are multiple options available under this parameter. You can view the available filters under this parameter with:<br><br>- `tshark -z help`<br><br>- Sample usage.<br><br>- `tshark -z filter`<br><br>- Each time you filter the statistics, packets are shown first, then the statistics provided. You can suppress packets and focus on the statistics by using the `-q` parameter.|

---

#### Colourised Output

>TShark can provide colourised outputs to help analysts speed up the analysis and spot anomalies quickly. If you are more of a Wireshark person and feel the need for a Wireshark-style packet highlighting this option does that. The colour option is activated with the `--color` parameter, as shown below.  
