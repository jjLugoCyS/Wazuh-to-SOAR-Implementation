# Wazuh to SOAR Implementation

## Objective
[Brief Objective - Remove this afterwards]

The Detection Lab project aimed to establish a controlled environment for simulating and detecting cyber attacks. The primary focus was to ingest and analyze logs within a Security Information and Event Management (SIEM) system, generating test telemetry to mimic real-world attack scenarios. This hands-on experience was designed to deepen understanding of network security, attack patterns, and defensive strategies.

### Skills Learned
[Bullet Points - Remove this afterwards]

- Advanced understanding of SIEM concepts and practical application.
- Proficiency in analyzing and interpreting network logs.
- Ability to generate and recognize attack signatures and patterns.
- Enhanced knowledge of network protocols and security vulnerabilities.
- Development of critical thinking and problem-solving skills in cybersecurity.

### Tools Used
[Bullet Points - Remove this afterwards]

- Security Information and Event Management (SIEM) system for log ingestion and analysis.
- Network analysis tools (such as Wireshark) for capturing and examining network traffic.
- Telemetry generation tools to create realistic network traffic and attack scenarios.

## Steps
1. On <a href="https://www.Draw.io">Draw.io</a> creat a diagram top map out how we want to build this out logically. Include the steps that are taken in a SOAR alert system, using colors to differentiate the actions taken at each step.<br>
![Wazuh and SOAR](https://github.com/user-attachments/assets/b8d5d560-6152-47aa-ba39-e9b026c0b8f9)<br>
*Ref 1: Diagram*<br>
2. Now start by installing Wazuh after setting up a VM on <a href="https://digitalocean.com/">Digital Ocean</a>.
3. Install TheHive like we did Wazuh and make a new droplet for it.
4. Configure thehive and open cassandra.yaml<br>
![1  open cassandra yaml](https://github.com/user-attachments/assets/452d2a06-4ab8-47e7-bcba-16603a8fcf69)<br>
*Ref 2: Open Cassandra.yaml*<br>
5. Change the cluster name then go to listen_address and change it to the public IP for thehive vm.<br>
![2  change cluster name](https://github.com/user-attachments/assets/5cef2838-f3fb-48fc-913a-2ae6d229e029)<br>
*Ref 3: Cluster Name*<br>
![3  change listen_address to public IP for thehive](https://github.com/user-attachments/assets/ab646222-d4f1-4464-bf23-3c14c3cadec4)<br>
*Ref 4: listen_address*<br>
6. Do the same with the rpc_address.<br>
![4 change rpc_address to public IP for thehive](https://github.com/user-attachments/assets/0b33b6f0-1ae6-444b-a062-1051c6454246)<br>
*Ref 5: rpc_address*<br>
7. Find the seed_address, go under seed_provider then to seed and replace it with the public IP address like above, but keep the :7000 port.<br>
![5  change seed_address under seed_provider seeds public IP adress 7000](https://github.com/user-attachments/assets/0ff90929-de4e-41e8-8bc9-72634023521a)<br>
*Ref 6: seed_address*
