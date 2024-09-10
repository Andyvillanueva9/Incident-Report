

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













<p align="center">
Centered Text: <br/>
<img src="imagelink"/>
<br />
<br />
Centered Text:  <br/>
<img src="imagelink"/>
<br />
<br />
Centered Text: <br/>
<img src="imagelink"/>
<br />
<br />
Centered Text:  <br/>
<img src="imagelink"/>
<br />
<br />
Centered Text:  <br/>
<img src="imagelink"/>
<br />
<br />
Centered Text:  <br/>
<img src="imagelink"/>
<br />
<br />
Centered Text:  <br/>
<img src="imagelink"/>
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
