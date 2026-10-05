# SIEM-Multiple-Authentication-Failure



**Multiple Authentication Failure Investigation**

**Objective**

Investigate Windows authentication failures detected by Wazuh and determine whether repeated failed logons indicate suspicious activity.

Lab Environment

* Windows 11 endpoint
* Sysmon
* Wazuh Agent
* Ubuntu Server running Wazuh Manager
* Wazuh Dashboard
* VirtualBox

Detection

Multiple Windows authentication failures were generated on the Windows 11 endpoint during controlled testing.

Field	                    Value
Event ID	                 4625
Wazuh Rule ID	             60122
Rule Level	               5
Target Account             Nihan
Logon Type	               2 (Interactive)
Source IP                  127.0.0.1

Investigation

The events were reviewed in Wazuh Threat Hunting and the underlying Windows event data was examined.

The authentication failures originated from 127.0.0.1 and targeted the same local Windows account. The events occurred repeatedly within a short time period.

The authentication status and substatus values were:

* 0xc000006d — authentication failure
* 0xc000006a — incorrect password

Analysis

The repeated Event ID 4625 events could resemble password-guessing activity when observed without context.

However, these events were intentionally generated as part of a controlled Wazuh lab exercise. The repeated failures therefore do not represent an actual attack in this test environment.

Verdict

Benign — Controlled Security Testing

The Wazuh detection successfully identified the Windows authentication failures and provided sufficient event data for investigation.

SOC Workflow Demonstrated

Windows Event → Wazuh Detection → Alert Triage → Event Analysis → Contextual Investigation → Verdict

Key Learning

This exercise demonstrated how a SOC analyst can distinguish between a security detection and a genuine security incident by combining event data with contextual information.




IF the authentication failures originate from a non-loopback IP address, the source system should be identified and investigated. The analyst should review the targeted account, logon type, failure frequency, authentication status, successful logons around the same time, and activity from the same source IP. Additional Wazuh and Sysmon events should be correlated to determine whether the activity is legitimate, suspicious, or potentially malicious.
