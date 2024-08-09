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
<br>5. Change the cluster name then go to listen_address and change it to the public IP for thehive vm.<br>
![2  change cluster name](https://github.com/user-attachments/assets/5cef2838-f3fb-48fc-913a-2ae6d229e029)<br>
*Ref 3: Cluster Name*<br>
![3  change listen_address to public IP for thehive](https://github.com/user-attachments/assets/ab646222-d4f1-4464-bf23-3c14c3cadec4)<br>
*Ref 4: listen_address*<br>
<br>6. Do the same with the rpc_address.<br>
![4 change rpc_address to public IP for thehive](https://github.com/user-attachments/assets/0b33b6f0-1ae6-444b-a062-1051c6454246)<br>
*Ref 5: rpc_address*<br>
<br>7. Find the seed_address, go under seed_provider then to seed and replace it with the public IP address like above, but keep the :7000 port.<br>
![5  change seed_address under seed_provider seeds public IP adress 7000](https://github.com/user-attachments/assets/0ff90929-de4e-41e8-8bc9-72634023521a)<br>
*Ref 6: seed_address*<br>
<br>8. Stop the Cassandra service. Remove all old files. Start Cassandra<br>
![6  Stop cassandra service](https://github.com/user-attachments/assets/b7b1d31e-6b9b-400b-a175-9eccf9dc072d)<br>
*Ref 7: Stop cassandra*<br>
![7  remove everything](https://github.com/user-attachments/assets/bc5c0f29-457a-4130-a2eb-a0e4aebb4261)<br>
*Ref 8: Remove old files*<br>
![8  start cassandra service](https://github.com/user-attachments/assets/68874021-76e8-4c99-a308-f3a4d555bdf4)<br>
*Ref 9: Start cassandra*<br>
<br>9. Open Elasticsearch.yml, and uncomment cluster.name and change it to thehive, also just uncomment node.name<br>
![9  open elasticsearch yml](https://github.com/user-attachments/assets/abcbd93b-d878-4bc5-aa73-3e7bfa7576c3)<br>
*Ref 10: Open elasticseatch.yml*<br>
![10  uncomment then change cluster name to thehive and just uncomment node name](https://github.com/user-attachments/assets/a0c85588-1bcd-44cf-b545-9bff9fc25cfa)<br>
*Ref 11: Change cluster.name and node.name*<br>
<br>10. Now uncomment network.host and change that to thehive public IP. Just uncomment http.port<br>
![11  uncomment and change network host tothehive public IP and uncomment http port](https://github.com/user-attachments/assets/22e85e32-504a-4ecd-bdff-de79e957bc4d)<br>
*Ref 12: Change network.host*<br>
<br>11. Uncomment cluster.initial_master_nodes and delete node 2. Start elasticsearch<br>
![12  uncomment clusterinitial master nodes and delete node-2](https://github.com/user-attachments/assets/d5567fd1-d9f2-447b-8784-c044e235d2d0)<br>
*Ref 13: Change cluster.initial_master_nodes*<br>
<br>12. Change the ownershu[ to thehive path<br>
![13  change ownership to thehive path](https://github.com/user-attachments/assets/f828de6d-7c58-44af-a708-d32e9c004f77)<br>
*Ref 14: Change ownership*<br>
<br>13. Now open thehive configuration file. Under database and index configuration change hostname to thehive public IP. Change cluster-name to the cluster that was put into Cassandra. Then under index.search change the hosname to thehive public IP. Finally under service configuration change application.baseUrl to thehive public IP and keep the 9000.{<br>
![14  open thehive conf file](https://github.com/user-attachments/assets/a193e090-9930-4667-931d-96f5b4a73aa6)<br>
*Ref 15: Open thehive conf*<br>
![15  change hostname to thehive public IP under db and index config](https://github.com/user-attachments/assets/36f0607a-6edc-4f45-b701-0ecd1955b0b7)<br>
*Ref 16: hostname to public IP*<br>
![16  change cluser-name to your cassandra cluster name](https://github.com/user-attachments/assets/626e7643-bfb7-4901-8b8e-7a6188e24a7f)<br>
*Ref 17: Change cluster-name*<br>
![17  change index search hostname to thehive public IP](https://github.com/user-attachments/assets/a656ce36-986e-4182-9ce5-b25c5e9695f2)<br>
*Ref 18: Change index.search*<br>
![18  change app baseURL to public IP 9000 of thehive under service config](https://github.com/user-attachments/assets/b8bfdd3b-d553-4fa0-842b-93fc22b9213b)<br>
*Ref 19: Change application.baseUrl*<br>
<br>14. Start and enable thehive.<br>
![19  start and enable thehive](https://github.com/user-attachments/assets/93824e7b-dbb3-466c-b523-1eb289b4df4b)<br>
*Ref 20: Start and enable thehive*<br>
<br>15. After logging into Wazuh you'll see a No Agents message, click add agent. Click Windows. Enter the Wazuh server public IP. Assign an agent name.<br>
![20  install agent by clicking add agent](https://github.com/user-attachments/assets/8b4684ab-8c58-4c30-99f8-d19f69b699a9)<br>
*Ref 21: Add agent*<br>
![21  click windows](https://github.com/user-attachments/assets/2f4e9f62-31a5-4106-b834-d6d55b19f5d1)<br>
*Ref 22: Click windows*<br>
![22  enter wazuh public IP in server add](https://github.com/user-attachments/assets/5dd70e45-bda5-4153-af49-730ac38f315d)<br>
*Ref 23: Wazuh public IP*<br>
![23 assign agent name](https://github.com/user-attachments/assets/97d017ad-cf4c-418d-b38d-f430e03fa178)<br>
*Ref 24: Assign agent name*
<br>16. In a windows 10 VM we copy and paste the output given to us by Wazuh.<br>
![24  start wazuh and begin the agent](https://github.com/user-attachments/assets/a7959329-34da-4d30-811b-7f2f9d220847)<br>
*Ref 25: Paste Wazuh commands*<br>
<br>17. Enter "net start wazuh <and agentname>" and go back to wazuh in your browser, click security events and you will be presented with active agent screens.<br>
![25  Agent connected and active](https://github.com/user-attachments/assets/ce1d036a-5d57-4b92-b207-9704f3348b99)<br>
*Ref 26: Agent connected and active*<br>
![26  agent active with 25](https://github.com/user-attachments/assets/2da42bd0-0d5c-4880-a94c-53207a1785f8)<br>
*Ref 27: Agent active*<br>
![27  Security events](https://github.com/user-attachments/assets/58db2e37-0d53-4473-9393-74805f9ed725)<br>
*Ref 28: Security Events*
<br>18.
