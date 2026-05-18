<img width="2545" height="915" alt="image" src="https://github.com/user-attachments/assets/fab9e8fc-383c-4e0f-aeb0-a47a1d948b66" /># Qradar101-Lab-CyberDefenders
### Analyze diverse log sources in QRadar SIEM to identify compromised systems, detect malicious tools, and reconstruct the sequence of attack events.

## Scenario:

### A financial company was compromised, and they are looking for a security analyst to help them investigate the incident. The company suspects that an insider helped the attacker get into the network, but they have no evidence.
 

### The initial analysis performed by the company's team showed that many systems were compromised. Also, alerts indicate the use of well known malicious tools in the network. As a SOC analyst, you are assigned to investigate the incident using QRadar SIEM and reconstruct the events carried out by the attacker.
 

## Dataset:
- Sysmon - swift on security configuration
- Powershell logging
- Windows Eventlog
- Suricata IDS
- Zeek logs (conn, HTTP)

## Solution
### Q1: How many log sources available?
### Sol: Navigating to the admin section in Qardar we will be able to see system configuration, Data sources, Apps. From data sources we can see the log sources.
<img width="2559" height="1300" alt="Log Sources" src="https://github.com/user-attachments/assets/ba9e1ea5-7cdd-49ea-bd45-d6650f7e00c5" />

### Ans: 15.

<img width="1242" height="249" alt="image" src="https://github.com/user-attachments/assets/0393f16d-a325-4938-87da-9021e3879c7a" />

### Q2: What is the IDS software used to monitor the network?
### Sol: Navigating to the admin section in Qardar we will be able to see system configuration, Data sources, Apps. From data sources we can see the log sources searching for the IDS Software.
<img width="2559" height="1306" alt="IDS" src="https://github.com/user-attachments/assets/ba595d5c-e5aa-428b-9d49-05d146fef6d2" />

### Ans: Suricata.
<img width="1235" height="255" alt="image" src="https://github.com/user-attachments/assets/3cab62d6-3c4a-4759-8e05-2a85fac2f665" />

### Q3: What is the domain name used in the network?
### Sol: Using the Event id "4720" to detecting the newly creating users to narrow down the search. Only one account created.
<img width="2559" height="696" alt="image" src="https://github.com/user-attachments/assets/e7cf3712-f02b-4054-baaa-05e7c28710c3" />
### The new user called rambo. So now searching for Event id "4624" and user name "rambo":

<img width="2559" height="1258" alt="Domain" src="https://github.com/user-attachments/assets/5f87199b-1a67-43bb-8022-8d169d3c06f3" />
### Ans: hackdefend.local

<img width="1274" height="266" alt="image" src="https://github.com/user-attachments/assets/4fe52865-c3d4-4e58-b48a-24e0beb408e8" />

### Q4: Multiple IPs were communicating with the malicious server. One of them ends with "20". Provide the full IP.
### Sol: From the previous question the created user "rambo" seeing which ip was used to create the user:
<img width="2559" height="666" alt="ip" src="https://github.com/user-attachments/assets/bebdcdc8-41be-49de-9d49-d6b3f95db43f" />

### Ans: 192[.]168[.]20[.]20
<img width="1248" height="253" alt="image" src="https://github.com/user-attachments/assets/de60e033-032e-49a5-832c-f4bc991a7d97" />

### Q5: What is the SID of the most frequent alert rule in the dataset?
### Sol: For this question start by filtering the search by Rule SID: 
<img width="1316" height="806" alt="SID" src="https://github.com/user-attachments/assets/e36f6834-0c8f-40bb-a3d9-18699eeaf66f" />

### After this We will see all the logs grouped by SIDs, then we navigate to the highest Magnitude:
<img width="2559" height="1036" alt="SID 2" src="https://github.com/user-attachments/assets/5832a2d7-2ad7-4c96-8900-46cf1904a2af" />

### Furthermore, we will see the first log with our suspicious IP 192[.]168[.]20[.]20 going throw it we got the SID 
<img width="2531" height="806" alt="SID 3" src="https://github.com/user-attachments/assets/36d5fb3e-b8d1-4863-8161-8f45e59002ec" />

### Ans:	2027865
<img width="1256" height="264" alt="image" src="https://github.com/user-attachments/assets/49ea8d39-7f17-4ca0-88ff-d5bf8de210ff" />

### Q6: What is the attacker's IP address?
### Sol: From the previous questions we know that the ip that the attacker use in the local system is 192[.]168[.]20[.]20 with this info we will filter the logs as groups using sources ip and destination ip:
<img width="1635" height="926" alt="attacjer IP" src="https://github.com/user-attachments/assets/00267246-4ee2-4bab-94fa-13accae1db1b" />

### A lot of ips but the one looking very suspicious the one that using 448 as a destination port and Very high Zeek connection count.
<img width="2559" height="1329" alt="ip 2" src="https://github.com/user-attachments/assets/4fb5b155-8f3a-42f2-add1-0171054ba85a" />


### Ans: 192[.]20[.]80[.]25
<img width="1246" height="261" alt="image" src="https://github.com/user-attachments/assets/49d5689b-6bdf-419c-90f7-fa53c6348ddc" />


### Q7: The attacker was searching for data belonging to one of the company's projects, can you find the name of the project?
### Sol: Filtering the logs to match any log that has the word project in it's payload we got only four logs:
<img width="2537" height="521" alt="image" src="https://github.com/user-attachments/assets/482f49dd-be93-4dc4-95f3-e8762a3aef61" />

### examining them to find the project :
<img width="2559" height="428" alt="project" src="https://github.com/user-attachments/assets/2d128228-fd9a-4380-a2e3-96ca71f5266f" />




### Ans: project48
<img width="1253" height="297" alt="image" src="https://github.com/user-attachments/assets/570e40eb-0c0b-441f-b208-b6c38b71e48c" />

### Q8: What is the IP address of the first infected machine?
### Sol: From the same log that we found the project we can determine the ip of the infected victim:

<img width="2119" height="441" alt="victim" src="https://github.com/user-attachments/assets/ef66e46d-e233-4c2e-9123-22a430e56205" />

### Ans: 192[.]168[.]10[.]15
<img width="1256" height="263" alt="image" src="https://github.com/user-attachments/assets/235d9d0c-5efd-420a-8229-6638daa5fd1c" />

### Q9: What is the username of the infected employee using 192.168.10.15?
### Sol: From the same log:
<img width="2527" height="806" alt="victim user" src="https://github.com/user-attachments/assets/a9e91d62-7981-4bc9-bac1-d38f404b95b5" />

### Ans: nour
<img width="1258" height="258" alt="image" src="https://github.com/user-attachments/assets/245f04cf-ae90-4b29-8d3d-dc8ec23e0003" />

### Q10: Hackers do not like logging, what logging was the attacker checking to see if enabled?
### Sol: From the previous question we know that the user nour and log source is HD-FIN-03 we filter with this two we will see a lot of powershell use.
<img width="2464" height="623" alt="image" src="https://github.com/user-attachments/assets/1abae019-60fb-4657-a93b-c02c46944886" />


### Ans: PowerShell
<img width="1270" height="269" alt="image" src="https://github.com/user-attachments/assets/c8b915e7-6ac6-4721-94ca-9ea0262b532e" />

### Q11: Name of the second system the attacker targeted to cover up the employee?
### Sol: Filter logs with Process comandline that contains del: 
<img width="2559" height="684" alt="image" src="https://github.com/user-attachments/assets/e3bcb310-a2a7-4bad-ae02-a2206d19e9ad" />

Navigating throw the logs we found this:
<img width="2464" height="441" alt="logs" src="https://github.com/user-attachments/assets/dd018215-6e36-4a9d-b8f7-a8adaaf76ef0" />


### Ans: mgnt-01
<img width="1256" height="256" alt="image" src="https://github.com/user-attachments/assets/e4023df7-092e-418a-a7a4-9bea576f881c" />


### Q12: When was the first malicious connection to the domain controller (log start time - hh:mm:ss)?
### Sol: knowing the infected machine searching with it's ip address and network connection there is some logs sort it by time to see the first creations:
<img width="2559" height="981" alt="image" src="https://github.com/user-attachments/assets/1e7f492f-d85e-4d6c-a35a-0d8fa3047d60" />

going throw the logs we found that notebad.exe establish a network connection:
<img width="2559" height="947" alt="time" src="https://github.com/user-attachments/assets/7fda7828-6f86-47b1-b3cd-c4b4d4077ab3" />


### Ans: 11:14:10
<img width="1236" height="254" alt="image" src="https://github.com/user-attachments/assets/87cdcf9c-3238-4157-9ad1-effe2c005ad9" />

### Q13: What is the md5 hash of the malicious file?
### Sol: filter for hashes in the logs payload:
<img width="2559" height="758" alt="tt" src="https://github.com/user-attachments/assets/1f1aac03-8a54-451a-8d4e-563eeb827c0f" />


### From FileCreate Event we found the malicious file that the malware downloads `important_instructions.docx`
<img width="2326" height="342" alt="aa" src="https://github.com/user-attachments/assets/3b421947-6d56-45b7-8b40-131443cf8c34" />


### Ans: 9D08221599FCD9D35D11F9CBD6A0DEA3
<img width="1247" height="272" alt="image" src="https://github.com/user-attachments/assets/8a1ba762-4002-46a1-94e8-568d59218552" />

### Q14: What is the MITRE persistence technique ID used by the attacker?
### Sol: Searching for any change in registry keys we found that the attacker add a vbs file to the run key to make the malware run at start.
<img width="2545" height="915" alt="image" src="https://github.com/user-attachments/assets/4d373d56-3487-4449-a208-08c0b4428937" />
### From the first infected device:
<img width="2377" height="445" alt="image" src="https://github.com/user-attachments/assets/e0af1011-8eee-4805-a4e8-29f3ccb1f035" />

### Ans: T1547.001
<img width="1243" height="258" alt="image" src="https://github.com/user-attachments/assets/b9e8fced-50df-4ae1-8af2-2228b317da56" />

### Q15: What protocol is used to perform host discovery?
### Sol: knowing the IP for the first machine that infected so we filter with it for all the network flow that is not TCP or UDP:
<img width="2547" height="802" alt="image" src="https://github.com/user-attachments/assets/bbe4f6f3-3ae8-43fb-9a2e-945207015d28" />


### From the logs the protocol is ICMP 

### Ans: ICMP
<img width="1262" height="259" alt="image" src="https://github.com/user-attachments/assets/3d2dfb05-1e3d-4e6b-89e0-c1c2471e1da9" />

### Q16: What is the email service used by the company?(one word)
### Sol: knowing that the connection will be outside the compeny network we will filter with destination port equal to 53 dns port:
<img width="2545" height="614" alt="image" src="https://github.com/user-attachments/assets/c172e581-2d20-452d-b6b6-87511f0ee85f" />

### Searching for info about ip 13.107.252.10:
<img width="788" height="268" alt="image" src="https://github.com/user-attachments/assets/2a5d4fac-6a97-403f-a7a4-0a5c6aa02db6" />

### Knowing that the ip belongs to microsoft and microsoft provides three services for emails (Microsoft Exchange, Microsoft Outlook, Office 365)

### Ans: office365
<img width="1269" height="276" alt="image" src="https://github.com/user-attachments/assets/2ac2a13a-d9c9-4efb-a3dd-338db5548d65" />

### Q17: What is the name of the malicious file used for the initial infection?
### Sol: From question 13 when we got the md5 for the file.
### Ans: important_instructions.docx
<img width="1280" height="261" alt="image" src="https://github.com/user-attachments/assets/2c6d5069-ddd1-4b50-bb2f-ff071147adf8" />

### Q18: What is the name of the new account added by the attacker?
### Sol: Filtering with event id = 4720:
<img width="2559" height="438" alt="image" src="https://github.com/user-attachments/assets/5d9a0c4c-6b5c-444c-a62e-3ee38e3b76b8" />
### we got the user :
<img width="2542" height="454" alt="image" src="https://github.com/user-attachments/assets/718d43c7-4c22-4944-b7fa-59c1dd3210d0" />

### Ans: rambo
<img width="1260" height="272" alt="image" src="https://github.com/user-attachments/assets/9a2a00df-7ae7-4cfd-9fc5-40f0398f62c4" />

### Q19: What is the PID of the process that performed injection?
### Sol: Filtering with eventids (1, 10, 8)
<img width="2556" height="577" alt="image" src="https://github.com/user-attachments/assets/96d25e00-1560-4334-876c-6e7eaf81ec80" />

### searching in create remote thread we found that a process creates a thread in another process.
<img width="2176" height="453" alt="image" src="https://github.com/user-attachments/assets/ffd74ba6-45af-4772-88ed-1e1426baae2b" />


### Ans: 7384 
<img width="1253" height="262" alt="image" src="https://github.com/user-attachments/assets/2fdca19d-f560-43c2-b9b4-0e77c5259276" />

### Q20: What is the name of the tool used for lateral movement?
### Sol: Searching for cmd or powershell commands:
<img width="2557" height="1107" alt="image" src="https://github.com/user-attachments/assets/43d5da6d-45d1-4420-8f5f-34426a641742" />

### Founding that the attacker used the registres to move from a device to another `cmd.exe /Q /c reg query HKLM\Software\Policies\Microsoft\Windows\PowerShell\ScriptBlockLogging 1> \\127.0.0.1\ADMIN$\__1604913874.5822518 2>&1`

### Searching on google we found a [github ](https://github.com/SecureAuthCorp/impacket)

### Ans: wmiexec.py
<img width="1256" height="265" alt="image" src="https://github.com/user-attachments/assets/9344dab6-09a6-4be0-9af7-de6cb71b2fc8" />


### Q21: Attacker exfiltrated one file, what is the name of the tool used for exfiltration
### Sol: using the same filter founding that the attacker use curl to uplaod a file to his ip:
<img width="2550" height="921" alt="image" src="https://github.com/user-attachments/assets/51c726a6-7c74-4107-af00-b912da1fc66a" />


### Ans: curl
<img width="1240" height="254" alt="image" src="https://github.com/user-attachments/assets/c3a20594-e319-46c3-804b-3a3e306647dc" />

### Q22: Who is the other legitimate domain admin other than the administrator?
### Sol: Filtering with username and Successful logon with administrative or special privileges:

<img width="2532" height="617" alt="image" src="https://github.com/user-attachments/assets/b875a1aa-7bd1-4e24-9395-b48904ca301a" />


### Ans: adam
<img width="1249" height="262" alt="image" src="https://github.com/user-attachments/assets/b5fb0169-8b3d-469d-b28e-110e51247a38" />

### Q23: The attacker used the host discovery technique to know how many hosts available in a certain network, what is the network the hacker scanned from the host IP 1 to 30?
### Sol: filtering with the ip address of the infected device `192.168.10.15` with log source `Zeek-conn`:
<img width="2559" height="955" alt="image" src="https://github.com/user-attachments/assets/c821b725-da98-49d2-8190-59076f939f61" />

### Ans: 192.168.20.0
<img width="1247" height="289" alt="image" src="https://github.com/user-attachments/assets/b264d84d-e7b9-489c-8da2-a051586b07f9" />

### Q24: What is the name of the employee who hired the attacker?
### Sol: From the cmd commands the attacker takes sami document then delete it form the devices:
<img width="1688" height="777" alt="image" src="https://github.com/user-attachments/assets/aa10f066-bac6-4e35-8214-30b4ebd14046" />


### Ans: sami
<img width="1258" height="271" alt="image" src="https://github.com/user-attachments/assets/8bfc2f84-a741-4c54-b688-bbcc45356cc7" />
