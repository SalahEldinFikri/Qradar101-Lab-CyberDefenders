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

### Ans: 192.168.20.20
<img width="1248" height="253" alt="image" src="https://github.com/user-attachments/assets/de60e033-032e-49a5-832c-f4bc991a7d97" />

### Q5: What is the SID of the most frequent alert rule in the dataset?
### Sol:

### Ans:
