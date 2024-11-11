
----
==***This will simulate Velociraptor:***==
- **Running as a server in => <span style="color:#9e46e2">Linux (Ubuntu)</span>** 
- **And as a client Running => <span style="color:#0070c0">Windows</span>**
----
Below is a brief explanation of each column.

| <span style="color:#00b050">column</span>  | <span style="color:#0070c0">Description</span>  |
|---|---|
|**Online State**|<span style="color:#00b050">A green dot indicates the endpoint is online and communicating with the Velociraptor server.</span> <span style="color:#ffff00">A yellow dot means the server hasn't received any communication from the endpoint within a 24-hour time frame</span>. <span style="color:#c00000">A red dot means it's been more than 24 hours since the server last heard from the endpoint.</span> |
|**Client ID**|This is a unique ID assigned to the client by the <span style="color:#9e46e2">**Velociraptor server**</span>, and the server will use this client ID to identify the endpoint. A client ID always starts with the letter **C**. |
|**Hostname**|This is the hostname the client identifies itself to the Velociraptor server. <span style="color:#0070c0">Remember that hostnames can change,</span> hence why Velociraptor uses the Client ID instead of identifying a client machine. |
|**Operating System Version**|The **<span style="color:#00b050">Velociraptor client</span>** can run on Windows, Linux, or MacOS. The details regarding the client operating system are displayed in this column. |
|**Labels**|<span style="color:#00b050">Client</span> machines may have multiple labels attached to them. This is useful to identify multiple clients as a group. |

﻿----
﻿