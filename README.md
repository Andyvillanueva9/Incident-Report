<html>

<h1>Incident Report</h1>
<br />
<br />
 

<h2>Index</h2>
<br />

<h3>Executive Summary </h3>
<br />
<h3>Technical Analysis</h3>
<br />
	&nbsp; &nbsp; Affected Systems & Data
<br />
	&nbsp; &nbsp; Evidence Sources & Analysis 
<br />
	&nbsp; &nbsp; Root Cause Analysis	
<br />
	&nbsp; &nbsp; Technical Timeline	
<br />
<h3>Response and Recovery Analysis</h3>
<br />
	&nbsp; &nbsp; Immediate Response Actions
<br />
	&nbsp; &nbsp; Post-incident Actions
<br />

<h3>Annex A</h3>
	&nbsp; &nbsp; Technical Timeline
<br />
<br />
<br />
<br />
<br />


<h2>Executive Summary</h2>
<br />
<ul>
  <li><b>Incident Severity</b>: High</li>
  <li><b>Incident Status</b>: Resolved</li>
  <li><b>Incident Overview</b>: On September 3, 2024 at 08:30:00, a suspicious amount of logs were found within the system events on the firewall. The logs indicated that the firewall was under a brute force attack from various IPs. After analyzing the logs it seems the brute force attack was aimed at compromising the administrator login on the firewall. Changes were quickly made to the firewall’s login timeout after 3 failed  attempts. This dramatically reduced the number of logs generated and resources used. In addition to the timeout, HTTPS administrative access was disabled on WAN and a VPN tunnel was created for offsite      administrative access. Once HTTPS access was disabled the attack was stopped. </li>
  <li><b>Key Findings</b>: Due to an improper WAN configuration on the firewall for remote access. Attackers were able to find the admin web interface using the public IP. This allowed attackers to run scripts that would attempt different passwords and usernames from various IPs but were not able to gain access to any administrator accounts.</li>
  <li><b>Immediate Actions</b>: A timeout after 3 failed login attempts was set in place to slow down the attack. This allowed enough time to configure A VPN tunnel and disabled the HTTPS administrator web interface after testing and ensuring that the VPN tunnel allowed administrator web interface access. </li>
  <li><b>Stakeholder Impact</b>: The impact on systems was minimal with no notice in network performance degradation. Many un-analyzed logs on the firewall memory were purged because of the extreme number of logs that were generated. </li>
</ul>  
<br />
<br />
<br />
<br />
<br />
<br />

<h2>Technical Analysis</h2>
<br />

<b>Affected Systems and Data </b>
<br />
The only systems affected were the systems that were logged in to the admin web interface remotely. Once the VPN was configured the remote machines were able to connect using the VPN. In addition, some data was lost during the incident. Currently the number of logs lost is unknown. This data consisted of un-analyzed logs that were purged on the firewall due to the influx of logs using up all available memory. 
<br />
<br />
<b>Evidence Sources & Analysis </b>
<br />
On September 3, 2024 at 08:30:00 A large amount of logs were observed in the system event section of the firewall. These logs indicated failed login attempts from external IPs using different usernames. Attackers were attempting to gain access to the admin account on the firewall using a brute force attack on the HTTPS admin interface. 

<br />

<img src="https://github.com/Andyvillanueva9/Projectimages/blob/main/Untitled.jpg?raw=true](https://github.com/Andyvillanueva9/Projectimages/blob/e2e2991c2109b147dedfb8e78696c64f2d7e6fbf/Screenshot%201.jpg">

<br />
Analysis of the attacking IP addresses on the remaining logs show that all the attacks originated from the EU and have already been flagged by Virustotal for being malicious.
<br />
<br />

185.122.204.186 
<br />
https://www.virustotal.com/gui/url/1cfb497340c3daf6c3b705fd1d6741bda0627d2fdc1fe27d44804626d4b0ccb5
<br />
185.190.24.178
<br />
https://www.virustotal.com/gui/url/66d6c94372a05a4ce087c8fbaaa183dbd96cc9859b6c6cd74d915bf91e373fe8/detection
<br />
5.181.86.12
<br />
https://www.virustotal.com/gui/url/88505ef93c4180d16a277ae15d82a62961fd5943260a871453a815f637f6239e
<br />
<br />
<b>Root Cause Analysis </b>
<br />
Improper configuration for the admin web interface on the firewall led to it being found by attackers through the public IP. The attackers could have used Hydra or tools similar to that to perform the web login brute force attacks. 

<br />
<br />
<b>Technical Timeline </b>
<br />
The exact time of when the attack started could not be determined due to logs being lost. The oldest log available had a timestamp of September 3, 2024, at 04:47:12. The logs indicated that the attacks from 185.190.24.178 were the most active at the time with 5.181.86.12 and 185.122.204.186 joining in 2 hours after. 
<br />
<br />
<b>September 3, 2024 10:14:43 </b>: Changes were made to disable login for 600 seconds after 3 failed attempts. This significantly reduced the number of login attempts. 
<br />
<br />
<b>September 3, 2024 11:24:00 </b>: VPN tunnel was configured for remote admin access and tested to confirm it was operational. 
<br />
<br />
<b>September 3, 2024 11:30:00 </b>: HTTPS admin web interface was disabled and access was no longer possible through the public IP.  At this stage the attack was completely stopped. 
<br />
<br />
<br />
<br />
<br />
<h2>Response and Recovery Analysis</h2>
<br />
<br />
<b>Immediate Response Actions </b>
<br />
After finding evidence of an ongoing brute force attack more logs were analyzed to find the scale of the attack. Once it was verified that the attack was coming from various external IP addresses and not internal devices the decision was made to update the lock out time for failed logins. This allowed us to find the misconfiguration that allowed the attack to take place. Once the configuration was found, a VPN tunnel was created that would allow admin remote access. After testing the VPN and confirming remote access, the HTTPS admin interface was disabled from the internet facing WAN configuration.
<br />
<br />
<b>Post-incident Actions </b>
<br />
After losing some log data from this attack plans have been put in place to integrate the logs with Wazuh. A high volume of events that causes log purge can be used to hide evidence of earlier attacks. For example, if an attacker were to be successful in compromising a VPN a flood of events can be used to purge the logs containing the VPN attacks. The integration a scheduled to be complete by September 06, 2024. 
<br />
<br />
<br />
<br />
<br />
<h2>Annex A </h2>
<br />
<br />
<b>Technical Timeline </b>
<br />
<br />
<b>September 3, 2024 04:47:12 </b>: Logs indicated that various external IPs were attempting a brute force attack on the admin web interface of the firewall.
<br />
<br />
<b>September 3, 2024 10:14:43 </b>: Changes were made to disable login for 600 seconds after 3 failed attempts. This significantly reduced the number of login attempts. 
<br />
<br />
<b>September 3, 2024 11:24:00 </b>: VPN tunnel was configured for remote admin access and tested to confirm it was operational. 
<br />
<br />
<b>September 3, 2024 11:30:00 </b>: HTTPS admin web interface was disabled and access was no longer possible through the public IP.  At this stage the attack was completely stopped. 
<br />
<br />
</html>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
