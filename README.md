# Qradar101-Lab-CyberDefenders
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
