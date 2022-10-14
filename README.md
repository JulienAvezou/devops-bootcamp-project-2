# devops-bootcamp-project-2

Demo project for Module 6 - Artifact Repository Manager

Steps taken to complete demo:

1. Create droplet/server on DigitalOcean - make sure to have enough storage for running Nexus (8GB Memory, 160GB storage will be enough)

2. Config firewall rules for SSH login + install java v8 on remote server

3. Install Nexus on remote server

4. Create service user for Nexus -> adduser nexus

5. Change ownership permissions to nexus user to exec nexus app 
-> chown -R nexus:nexus nexus-3.42.0-01
-> chown -R nexus:nexus sonatype-work
-> check ownership changed: ls -l
-> change nexus config to allow to run as nexus user -> vim nexus-3.42.0-01/bin/nexus.rc (insert "nexus")
-> switch to nexus user: su - nexus

6. Start nexus -> /opt/nexus-3.42.0-01/bin/nexus start
-> check process running: ps aux | grep nexus

7. Open port 8081 to access Nexus from Browser -> config firewall rules in DigitalOcean
<img width="1203" alt="Capture d’écran 2022-10-14 à 20 16 34" src="https://user-images.githubusercontent.com/62488871/195914053-2f60fbd7-ea30-47e5-bc09-6d433f38b0d8.png">

8. Check Nexus is running in browser 
<img width="396" alt="Capture d’écran 2022-10-14 à 20 18 18" src="https://user-images.githubusercontent.com/62488871/195914351-77ba7109-c3b4-4a82-9bdf-c4889229b652.png">

9. login with default user created when deployed -> username admin password <INSERT_PASSWORD> 
(can get password: cat /opt/sonatype-work/nexus3/admin.password)

10. Create local nexus user with permission to upload
<img width="1141" alt="Capture d’écran 2022-10-14 à 20 56 19" src="https://user-images.githubusercontent.com/62488871/195920634-a7e5c062-d372-4dd2-ab3c-b429c9121e1c.png">

11. Create new role in Nexus
<img width="857" alt="Capture d’écran 2022-10-14 à 21 00 31" src="https://user-images.githubusercontent.com/62488871/195921368-62294241-08de-4fc1-b13a-1df43377bb67.png">

12. Assign role to local user to give permission to upload
<img width="902" alt="Capture d’écran 2022-10-14 à 21 02 28" src="https://user-images.githubusercontent.com/62488871/195921720-94adad6f-fc2c-4606-943e-796895065b8f.png">

13. Enrich gradle project to connect to Nexus and push to Maven repo (Nexus Repo URL + Credentials)
<img width="607" alt="Capture d’écran 2022-10-14 à 21 14 17" src="https://user-images.githubusercontent.com/62488871/195923638-15a94837-85a5-44a0-9da5-c1b3f9e2da51.png">
<img width="875" alt="Capture d’écran 2022-10-14 à 21 22 01" src="https://user-images.githubusercontent.com/62488871/195925767-c78ef3d7-49f3-4d30-a1bd-68b711ffc9b2.png">

14. Build artifact -> ./gradlew build
<img width="381" alt="Capture d’écran 2022-10-14 à 21 27 31" src="https://user-images.githubusercontent.com/62488871/195926667-4c295cbe-c6d1-4588-9a4a-1fa0679ae46e.png">

15. Upload artifact to Nexus -> ./gradlew publish
<img width="513" alt="Capture d’écran 2022-10-14 à 21 41 20" src="https://user-images.githubusercontent.com/62488871/195928747-be451a2b-16fa-41b5-8ea8-56932c5d5357.png">

16. Enrich maven project to connect to Nexus and push to Maven repo
add plugins to pom.xml file 
add credentials to settings.xml file inside .m2 folder (root level)

17. Build jar file -> mvn package
<img width="1349" alt="Capture d’écran 2022-10-14 à 21 57 44" src="https://user-images.githubusercontent.com/62488871/195931489-a5554045-8752-459a-8636-426da7be84c1.png">

18. Upload artifact to Nexus -> mvn deploy
<img width="1348" alt="Capture d’écran 2022-10-14 à 21 59 00" src="https://user-images.githubusercontent.com/62488871/195931701-093660c8-5734-4a54-b495-757675d96d43.png">
<img width="553" alt="Capture d’écran 2022-10-14 à 22 00 22" src="https://user-images.githubusercontent.com/62488871/195931908-d99fbabb-23e2-48fd-9fea-b610a6120b4d.png">

19. Create a new Blob store to attach to future repos
<img width="1084" alt="Capture d’écran 2022-10-14 à 22 36 54" src="https://user-images.githubusercontent.com/62488871/195939151-09db907c-a3d2-4e43-a872-837485e9260d.png">

20. Create cleanup policy and attach to repo
<img width="1107" alt="Capture d’écran 2022-10-14 à 22 47 34" src="https://user-images.githubusercontent.com/62488871/195940840-875323c2-db9a-4541-aa1b-bf4bd4f5ac8b.png">
<img width="894" alt="Capture d’écran 2022-10-14 à 22 49 00" src="https://user-images.githubusercontent.com/62488871/195941071-c2155f3a-fd34-4adf-9c7d-b519429c0c4a.png">
<img width="1136" alt="Capture d’écran 2022-10-14 à 22 51 58" src="https://user-images.githubusercontent.com/62488871/195941857-4a97d5dd-400f-47e6-8ce8-cb93b29bedda.png">

21. Run tasks manually to check they work
<img width="1137" alt="Capture d’écran 2022-10-14 à 22 57 11" src="https://user-images.githubusercontent.com/62488871/195942650-abcc531e-3a06-453b-9ba1-dd90cadab9e6.png">

22. Stop running Nexus
/opt/nexus-3.42.0-01/bin/nexus stop




