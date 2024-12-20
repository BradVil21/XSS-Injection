# XSS Javascript Code Detected 

<div>
  <b>SEVERITY:</b> Medium | <b>DATE:</b> Feb, 26, 2022, (06:56 PM) | <b>RULE NAME:</b> SOC166 - Javascript Code Detected in Requested URL | <b>TYPE:</b> Web Attack
    <br>
  <br>
  <b>EventID:</b> 116
  <br>
  <b>Event Time:</b> Feb, 26, 2022, 06:56 PM
  <br>
  <b>Rule:</b> SOC166 - Javascript Code Detected in Requested URL
  <br>
  <b>Level:</b> Security Analyst
  <br>
  <b>Source Address:</b> 112.85.42.13
  <br>
  <b>Source Hostname:</b> WebServer1002
  <br>
  <b>Destination Address:</b> 172.16.17.17
  <br>
  <b>HTTP Request Method:</b> GET
  <br>
  <b>Alert Trigger Reason:</b> Javascript code detected in URL
  <br>
  <b>Request URL:</b> https://172.16.17.17/search/?q=<$script>javascript:$alert(1)<$/script>
  <br>
  <b>User Agent:</b> Mozilla/5.0 (Windows NT 6.1; WOW64; rv:40.0) Gecko/20100101 Firefox/40.1
  <br>
  <b>Device Action:</b> Allowed
</div>
<br>
[Introduction: This repository focuses on analyzing, detecting, and preventing Cross-Site Scripting (XSS) attacks within web applications. By integrating detection mechanisms into an existing web environment, we aim to monitor for malicious script injection attempts, log potential XSS attacks in real-time, and implement robust mitigation strategies to safeguard users and sensitive data.]
<br>
<br>
Please also use this as a guide on how to work phishing alerts using Let's Defend. For any questions or concerns you can <b>CONTACT</b> me directly on <a href= "https://www.linkedin.com/in/bradley-vilsaint-414329267/">LinkedIn</a> or email <a href="info@letsdefend.io">info@letsdefend.io</a> for support.
<br>
<br>
    
<b>STEP 1</b><br>
While working through this alert, it is important to track what the alert has provided. <b>What should I do first?</b> Well good question. If you head to <b>"CASE PLAYBOOK"</b>, you are provided with details on what you should check for. Examine the rule name. Rule names are usually created specifically for the attack to be detected. By examining the rule name, you can understand which attack you are facing. Detect between which two devices the traffic is occurring. It's a good starting point to understand the situation by learning about the direction of traffic, what protocol is used between devices, etc. Here is the collection data for this alert: <br><br>
Ownership of the IP addresses and devices.<br>
If the traffic is coming from outside (Internet)<br>
Ownership of IP address (Static or Pool Address? Who owns it? Is it web hosting?)<br>
Reputation of IP Address (Search in VirusTotal, AbuseIPDB, Cisco Talos)<br>
If the traffic is coming from the company network;<br>
The hostname of the device<br>
Who owns the device (username)<br>
Last user logon time<br>
<br>

<b>STEP 2</b><br>
After identifying the attack type, it is important to examine the traffic content within the HTTP request. Since the attackers do not only attack through the URLs, all the data from the source must be examined to understand whether there is a cyber attack or not. For this project, the suspicious link was provided as also shown above: https://172.16.17.17/search/?q=<$script>javascript:$alert(1)<$/script>. Based on analyzing this URL, this confirms to be an XSS attack due to the <b><$script>javascript:$alert(1)<$/script></b> indicated within the URL. This javascript code pops up with an alert message whenever a user fails to insert or complete what the code is attempting to do before this malicious script.
  <br>
  
  <b>STEP 3</b><br>
After identifying the attack type, it is also important to check if this is a planned test. Why check if this is a planned test? Well, to answer your question, penetration tests or attack simulations can trigger False Positive alarms if the rules are not set correctly.
<br>
<b>Objective:</b>
<br>
<ul>
  <li>Check if there is an email showing that there will be planned work by searching for information such as hostname, username, and IP address on the mailbox.</li>
  <li>Check if the device generating malicious traffic belongs to attack simulation products. If the Hostname contains the name of Attack Simulation products (such as Verodin, AttackIQ, Picus…), these devices belong to Attack Simulation products within the framework of LetsDefend simulation and it is a planned work.</li>
</ul>
<br>
After checking the SIEM, this was not a planned test. With further investigation, I was able to find an HTTP Response status of 200 indicating that there was a success on the attacker's end. The direction of traffic was <b>Internet > Company Network</b>
<br>

<b>STEP 4</b><br>
Since it is now detected that the device is compromised, it is important to contain this internal device to avoid any future attacks. By heading to <b>Endpoint Security</b> and requesting to contain the device.<br>
<br>
<b>Summary:</b><br>
