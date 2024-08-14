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
<br>17. Enter "net start wazuh" and go back to wazuh in your browser, click security events and you will be presented with active agent screens.<br>
![25  Agent connected and active](https://github.com/user-attachments/assets/ce1d036a-5d57-4b92-b207-9704f3348b99)<br>
*Ref 26: Agent connected and active*<br>
![26  agent active with 25](https://github.com/user-attachments/assets/2da42bd0-0d5c-4880-a94c-53207a1785f8)<br>
*Ref 27: Agent active*<br>
![27  Security events](https://github.com/user-attachments/assets/58db2e37-0d53-4473-9393-74805f9ed725)<br>
*Ref 28: Security Events*
<br>18. Navigate to C: drive, then program files(x86), and find ossec.conf to make a back up.<br>
![28  ossec-backup](https://github.com/user-attachments/assets/cadea236-d4c8-47e4-8ca6-0d5012bead30)<br>
*Ref 29: ossec-backup.conf*<br>
<br>19. In the original ossec file copy and paste onse local file tag and change the the location to the sysmon channel name found in event viewer, right click operational file under system folder to select properties and find the name. Paste om <localfile>, remove other <localfiles> tags except for active response. Always open services and restrart the service you configured (wazuh).<br>
![29 Event viewer sysmon operational](https://github.com/user-attachments/assets/707b70e9-9b1d-42b4-bb98-87599daffcbe)<br>
*Ref 30: Event viewer > sysmon> operational*<br>
![30  sysmon poroperties full name](https://github.com/user-attachments/assets/d17ee8f8-ebe0-4e2f-9126-a4e3aa0d5970)<br>
*Ref 31: Sysmon properties full name*<br>
![31  localfile location sysmon](https://github.com/user-attachments/assets/5d86227d-ad10-4f34-b516-abb46a33dfe4)<br>
*Ref 32: localfile location sysmon*<br>
![32  leave sysmon and active response](https://github.com/user-attachments/assets/c00f2f10-5123-489e-9857-c762f3e7453d)<br>
*Ref 33: sysmon and active response*<br>
<br>20. Go to Wazuh dashboard, click events and search for sysmon events.<br>
![33  search sysmon events](https://github.com/user-attachments/assets/2cbb0952-ac59-4b7c-9072-d86b49ff3d16)<br>
*Ref 34: Search sysmon events*<br>
<br>21. Download mimikatz, but exclude the downloads path in windows security on your windows 10 VM exclusions first. Then exctract the mimikatz zip.<br>
![34  Download folder exclusion](https://github.com/user-attachments/assets/1b6b39e6-905a-40e8-82d7-04b37fe48e51)<br>
*Ref 35: Download folder exclusion*<br>
<br>22. Open and adminstrator powershell and cd to mimikatz and run mimikatz.exe<br>
![35  Run mimikatz](https://github.com/user-attachments/assets/b45419f0-d48a-4856-8135-fdcd6bdf14e5)<br>
*Ref 36: Run mimikatz*<br>
<br>23. Check the wazuh dashboard for any mimikatz events. Go to your wazuh server console and open the ossex.conf file. Set logall and logall_json to yes. Restart the wazuh manager<br>
![36  ossec conf wazuh server](https://github.com/user-attachments/assets/00bea640-b30e-460b-a0ee-f627aab6f6ad)<br>
*Ref 37: ossec.conf on wazuh server console*<br>
![37  Set logall and logall_json to yes](https://github.com/user-attachments/assets/1ac011ba-3a00-48ec-b277-c143152fcadd)<br>
*Ref 38: Set logall*<br>
![38  restart wazuh manager](https://github.com/user-attachments/assets/67803ad2-3c30-4427-9943-af243aeeae27)<br>
*Ref 39: Restart wazuh manager*
<br>24. Open filebeat.yml. Change archives > enabled to true. Then restart the filebeat service.<br>
![39  open filebeat yml](https://github.com/user-attachments/assets/a4330ac4-43a4-4711-98fa-fa18a40095ed)<br>
*Ref 40: Open filebeat.yml*<br>
![40  Change filebeat modules archives enabled to true](https://github.com/user-attachments/assets/0e79ed89-9824-4677-a843-d3fad197e480)<br>
*Ref 41: archives > enabled*<br>
<br>25. In the wazuh dashboard click the hamburger icon then stack management. Then click Index patterns. Click create index, name the index, click next, select timestamp from dropdown menu, click create index pattern. Head back to discover and select archives<br>
![41  click stack management](https://github.com/user-attachments/assets/05d7ed4a-b2ae-4b94-9b5b-5aef4ce34beb)<br>
*Ref 42: Stack mgmt.*<br>
![42  Click index patterns](https://github.com/user-attachments/assets/31b75867-d788-437d-9a4e-5831a38b9728)<br>
*Ref 43: Index patterns*<br>
![43  Create new index](https://github.com/user-attachments/assets/e8c1df0a-ee6c-4588-97e1-61ee7e48b586)<br>
*Ref 44: Create Index*<br>
![44  Name the index](https://github.com/user-attachments/assets/a9a2966d-3d78-4f9b-914f-1009712acbbf)<br>
*Ref 45: Name Index*<br>
![45  Choose timestamp](https://github.com/user-attachments/assets/1c47cceb-2336-4e2b-9b43-417d5e66fd51)<br>
*Ref 46: Choose timestamp*<br>
<br>26. Search in the dashboard for mimikatz events. Find and expand a mimikatz event id 1.<br>
![46  find and expand mimikatz event id 1](https://github.com/user-attachments/assets/a8458982-68d5-47e4-b5e7-ffa8a8056b30)<br>
*Ref 47: Mimikatz event id 1*<br>
<br>27. Click the home button, click dropdown, click management, then rules. Click manage rule files, search sysmon, click the eye icon next to sysmon_id_1.<br>
![47  click dropdown then mgmt then rules](https://github.com/user-attachments/assets/f6d66881-0428-48b1-85ab-4a4c84ee831d)<br>
*Ref 48: Mgmt then Rules*<br>
![48 Click manage rule files](https://github.com/user-attachments/assets/a4ddd712-4a69-4e6f-b2e2-ba5c9ea51db4)<br>
*Ref 49: Manage Rule Riles*<br>
![49  Click sysmon id 1 eye icon](https://github.com/user-attachments/assets/85bb7491-8dbf-435f-b385-215128d9bb28)<br>
*Ref 50: sysmon_id_1*<br>
<br>28. Copy the list rule id, Go back and click custom rules. Click on the pencil icon to edit and paste the copied rule below the existing rule.<br>
![50  Click custom rules button](https://github.com/user-attachments/assets/4ec5c6de-8e13-4af8-b94f-f1c6ecd0147f)<br>
*Ref 51: Custom Rules Button*<br>
![51  Click pencil icon to edit](https://github.com/user-attachments/assets/03197097-53c3-4fb6-8218-e19dc053a9a3)<br>
*Ref 52: Pencil Icon*<br>
<br>29. Change the rule id above 1000000, the level value to a higher level (because the higher the more important), filename to originalFileName(has to match exactly), the type you remove everything after (?i) and add mimikatz. Remove options no full log. Change description to something meaningful to you, and change mitre id (to prevent credential dumping). Using the original file name ensures the file is tracked and not bypassed.<br>
![52  Change some rule sections](https://github.com/user-attachments/assets/1a360314-c6be-4bf8-b059-a8e6b0b3ae13)<br>
*Ref 53: Rule Sections*<br>
![53  Change description and mitre id](https://github.com/user-attachments/assets/95712600-46a0-49e6-90cb-28b79db74132)<br>
*Ref 54: Description and Mitre*<br>
<br>30. Sign into shuffle and create a new workflow. Click on triggers > webhook and drag and drop. Copy the webhook URI. Click on change me, make syre the action is "repeat back to me" then click the "+" and execution argument.<br>
![54  New workflow](https://github.com/user-attachments/assets/c0552920-8ae8-4ff7-8efd-76394af62653)<br>
*Ref 55: New workflow*<br>
![55  Webhook trigger](https://github.com/user-attachments/assets/ef4b6c18-8f3e-4fc7-9dae-a04ec4ca0b6a)<br>
*Ref 56: Webhook trigger*<br>
![56  Actions and plus sign](https://github.com/user-attachments/assets/9e7d2076-5374-4d6f-a7f0-6847a90f1d7f)<br>
*Ref 57: + and arguments*<br>
<br>31. Go back to the wazuh server console and open the ossec.conf file and paste in the integration tag in it (it's found on the wazuh page). Paste the webhook URI (add the space at the end). Change the level tag to rule_id. Restart both the wazuh-manager.service and mimikatz<br>
![57  ossec conf shuffle integration](https://github.com/user-attachments/assets/3a77b891-df21-48b7-a061-cbc50d5e6c2d)<br>
*Ref 58: ossec.conf integration*<br>
<br>32. Going back to <a href= "https://www.shuffler.io">shuffle.io</a> and click start. Click test workflow. Then select the webhook in workflows and select execution arguments > expand window.<br>
![58  Expand execution arguments](https://github.com/user-attachments/assets/f0a3f84d-af18-4e1f-969b-9b144aa9fa81)<br>
*Ref 59: Expand execution arguments*<br>
<br>33. Click on change me and under find actions change it to regex capture group. In input data select execution argument and select your hash. Enter regex and save your workflow, rerun the workflow under execution and expand results<br>
![59  Shuffle tools](https://github.com/user-attachments/assets/5c85cefd-a33d-4522-99e0-14d71bd3e24e)<br>
*Ref 60: Change me Regex*<br>
![60  Expand results](https://github.com/user-attachments/assets/a0d342a4-b49f-4607-b998-108cce9761a8)<br>
*Ref 61: Expand results*<br>
<br>34. Create a virustotal account and copy your API key to authenticate it. In shuffle search for the virustotal app and activate it. Drag and drop virustotal over to the workflow. Click on virustotal app in workflow and in find actions select hash report. Click authenticate virustotal, paste in your API key then click submit. Under the hash section select regex output and select list. Save workflow and click show executions, click middle workflow, click rerun workflow, expand virustotal output and find last_analysis_stats.<br>
![61  Authenticate virustotal](https://github.com/user-attachments/assets/b6ecbd41-c12f-4287-8088-d5611e36835e)<br>
*Ref 62: Authenticate virustotal*<br>
![62  Virustotal settings](https://github.com/user-attachments/assets/b80be093-e12b-4538-9122-63781d184b2b)<br>
*Ref 63: Virustotal settings*<br>
![63  Virustotal output](https://github.com/user-attachments/assets/8c34faa6-c707-495b-a4e8-506c27d81498)<br>
*Ref 64: Virustotal output*<br>
![64  Last_analysis+stats malicious](https://github.com/user-attachments/assets/11177089-d5ec-4136-9820-10b4d01a9e9b)<br>
*Ref 65: last_analysis_stats amd malicious*<br>
<br>35. In shuffle apps search for thehive. Click on theHive to activate, drag and drop it into workflows.
<br>36. 
