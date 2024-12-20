---
layout: post
title: Wazuh THM
date: 11-11-2024
categories: [documentation]
tag: [like]
---
#Wazuh
---

> All sorts of actions and events are captured and recorded on a Windows operating system. 
> This includes authentication attempts, networking connections, files that were accessed, and the behaviours of applications and services. 
> This information is stored in the Windows event log using a tool called Sysmon.

---

#### Q: For What we using the `0250-apache_rules.xml` ruleset?

---

**<span style="font-weight:bold; color:#0070c0">A: This ruleset can analyze apache2 logs for warnings and error messages like so:</span> We will need to insert this into the Wazuh’s agent that is sending logs to the Wazuh management servers configuration file located in `/var/ossec/etc/ossec.conf`:**

---

***Apache2 Log Analysis***

```shell-session
  <!-- Apache2 Log Analysis -->
  <localfile>
    <location>/var/log/example.log</location>
    <log_format>syslog</log_format>
  </localfile>
```

----
#### <span style="color:#0070c0">Q: What HTTP method would we use to retrieve information for a Wazuh management server API?</span>
	GET
---
#### <span style="color:#0070c0">Q: What HTTP method would we use to perform an action on a Wazuh management server API?</span>
	PUT
---
