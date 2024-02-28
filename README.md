<h1>Microsoft Azure: Azure Sentinel (SIEM & SOAR) Project</h1>
<img src="https://imgur.com/MCDuyWe.png" height="80%" width="80%" alt="diagram"/>
<h2>Description</h2>
In this project, I setup Azure Sentinel (SIEM & SOAR) and connect it to a live virtual machine acting as a honey pot. I observe live attacks (RDP Brute Force) from all around the world. We will use a custom PowerShell script to look up the attackers Geolocation information and plot it on the Azure Sentinel Map.
<br />

<h2>Languages and Utilities Used</h2>

- <b>PowerShell</b> 
- <b>Microsoft Azure</b>
- <b>Remote Desktop Connection</b>

<h2>Environments Used </h2>

- <b>Windows 10</b> (21H2)

<h2>Program walk-through:</h2>

<p align="left">

I start by spinning up a brand new VM on Azure that is discoverable to all traffic: <br/>
<br />
<img src="https://imgur.com/LwZDG8f.png" height="80%" width="80%" alt="set up"/>
<br />
  
<br />
I make sure to change the security group inbound rules to make the VM discoverable to all inbound traffic:  <br/>
<br />
<img src="https://imgur.com/cj8s8vV.png" height="80%" width="80%" alt="set up"/>
<br />

<br />
I create a Log Analytics Workspace to log the inbound traffic to the VM: <br/>
<br />
<img src="https://imgur.com/WVrBleM.png" height="80%" width="80%" alt="set up"/>
<br />

<br />
I connect the Log Analytics Workspace to the VM:  <br/>
<br />
<img src="https://imgur.com/cvc2aWg.png" height="80%" width="80%" alt="set up"/>
<br />

<br />
I fire up the VM and then connect to it via an RDP connection from our local machine:  <br/>
<br />
<img src="https://imgur.com/cywVdub.png" height="80%" width="80%" alt="set up"/>
<br />

<br />
Here, I disable all the Windows Firewall profiles so that network traffic is allowed in:  <br/>
<br />
<img src="https://imgur.com/blLn2D8.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<br />
I sent a test ping from my local computer to the VM to ensure that its accepting traffic:  <br/>
<br />
<img src="https://imgur.com/pfj1r2L.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<br />
I sign up for a free account at https://ipgeolocation.io to gain a API key as we will be using their geolocation API to gain the geolocation information from our attackers IP's:  <br/>
<br />
<img src="https://imgur.com/55RDEz9.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<br />
I run a custom script that will grab the IP of the attackers from the security events, run it through the geolocation API and log all of that information into a log file :  <br/>
<br />
<img src="https://imgur.com/IZv9ErM.png" height="80%" width="80%" alt="Cyber Attack Event Management"/>
<br />

<br />
I'll save the script as log file and it'll create a txt file with all the failed login attempts Geo Data :  <br/>
<br />
<img src="https://imgur.com/BTvCbJb.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<br />
I can now create a custom log thats linked to the txt file with all the failed login attempts Geo Data:  <br/>
<br />
<img src="https://imgur.com/pOMAErE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<br />
Using KQL Queries within Azure Logs Workspace, I can observe the data from the custom log:  <br/>
<br />
<img src="https://imgur.com/feqrZqR.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<br />
Now I can extract the fields from the RawData custom logs:  <br/>
<br />
<img src="https://imgur.com/jLsYsXo.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<br />
I'll check the custom fields to confirm they appear before testing with new input:  <br/>
<br />
<img src="https://imgur.com/AHNYV0x.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<br />
Now I'll test the new custom fields which were extracted to see if they collect the data:  <br/>
<br />
<img src="https://imgur.com/rjCRuf2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<br />
Create a new Microsoft Sentinel instance to map where the attacks are coming from:  <br/>
<br />
<img src="https://imgur.com/Ij2CQgX.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<br />
Within Microsoft Sentinel, setup a map in workbooks using longitude and latitude:  <br/>
<br />
<img src="https://imgur.com/TnOTZlc.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />

<br />
Use the following KQL Query to isolate which data to be shown, and the following map settings to display on world map:  <br/>
<br />
<img src="https://imgur.com/jkC9uK0.png" height="80%" width="80%" alt="workbook setup"/>
<img src="https://imgur.com/TAeiN3Q.png" height="80%" width="80%" alt="workbook setup"/>
<img src="https://imgur.com/F7WlgYG.png" height="80%" width="80%" alt="workbook setup"/>
<br />

<br />
After a couple hours the VM will be found by the cyber attackers of the world. Now we can observe Geolocation information from where your attacks are attempting to breach the VM:  <br/>
<br />
<img src="https://imgur.com/srMTOOG.png" height="80%" width="80%" alt="Cyber Attack Event Management"/>

<br />
This Concludes This Microsoft Azure SIEM Project! <br />
<br/>
NOTE: Microsoft has decpreciated the usage of custom fields for tables in favour of Data Collection Rules and Ingestion Time Transfomations, therefor these steps are no longer possible on the newest build of Azure. You can find more information here: https://learn.microsoft.com/en-us/azure/azure-monitor/logs/custom-fields-migrate <br/>
<br />
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
