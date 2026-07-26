Project 9
Continuous Integration Pipeline: GitHub to NFS via Jenkins

Overview

This project establishes an automated Continuous Integration (CI) pipeline using Jenkins (v2.568.1) to track code changes in a GitHub repository, archive artifacts locally, and deploy updated source code directly to a 
target NFS server (/mnt/apps) via SSH using the Publish Over SSH plugin.

Infrastructure Overview (AWS EC2)

<img width="614" height="353" alt="image" src="https://github.com/user-attachments/assets/51041def-f4bc-4fd1-bf24-dfd02e23e2de" />

Step-by-Step Configuration

1. Jenkins Job Setup
1-Log into your Jenkins Web Dashboard ([http://3.89.202.227:8080](http://3.89.202.227:8080)).

2-Click New Item, name it tooling_github, select Freestyle project, and click OK.

3-Under Source Code Management:

   -Select Git.

  -Set Repository URL: [https://github.com/amarsaleem333/tooling.git](https://github.com/amarsaleem333/tooling.git)

  -Set Branch Specifier: */main

2. Configure Automated GitHub Webhook Trigger
   A. Jenkins Settings
   1-Go to tooling_github $\rightarrow$ Configure.
   2-Under Triggers, check GitHub hook trigger for GITScm polling.
   3-Under Post-build Actions, add Archive the artifacts and enter **.
   4-Click Save.

B. GitHub SettingsGo to [https://github.com/amarsaleem333/tooling]
  1-(https://github.com/amarsaleem333/tooling) $\rightarrow$ Settings $\rightarrow$ Webhooks $\rightarrow$ Add webhook.
  2-Payload URL: [http://3.89.202.227:8080/github-webhook/](http://3.89.202.227:8080/github-webhook/) (Trailing slash / required).
  3-Content type: application/json.
  4-Select Just the push event and click Add webhook.

3-  Deploy Artifacts to NFS Server via SSH
A. Global SSH Plugin Setup
 1-Go to Manage Jenkins $\rightarrow$ Plugins $\rightarrow$ Available plugins.
 2-Search for and install Publish Over SSH.
 3-Go to Manage Jenkins $\rightarrow$ System $\rightarrow$ Publish over SSH:
    -Paste your .pem SSH key into the Key field.
    -Add SSH Server:
         -Name: NFS-Server
         -Hostname: 172.31.17.253 (NFS Private IP)
         -Username: ec2-user
         -Remote Directory: /mnt/apps
    -Click Test Configuration to verify Success.

B. Post-Build Action Setup
 1-Go to tooling_github $\rightarrow$ Configure $\rightarrow$ Post-build Actions.
 2-Add Send build artifacts over SSH:
   -SSH Server: NFS-Server
   -Source files: 
 3-**Click Save.

Common Issues Encountered & Solved
1. ERROR: Couldn't find any revision to build
Cause: Default branch mismatch (master vs main).

Solution: Changed branch specifier in Jenkins S           
