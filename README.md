Project 9
Continuous Integration Pipeline: GitHub to NFS via Jenkins

Overview

This project establishes an automated Continuous Integration (CI) pipeline using Jenkins (v2.568.1) to track code changes in a GitHub repository, archive artifacts locally, and deploy updated source code directly to a 
target NFS server (/mnt/apps) via SSH using the Publish Over SSH plugin.

Infrastructure Overview (AWS EC2)

Role,Instance Name,Instance ID,Availability Zone,Instance Type,Status
CI/CD Server,Project 9 Jenkins,i-0896842635656b392,us-east-1d,t3.small,Running
NFS Server,Project 7 -NFS,i-0a8d61b9a302bee6b,us-east-1c,t3.micro,Running
Web Server 1,Project 7 -web server 1,i-053f79991056faa6b,us-east-1c,t3.micro,Stopped
Web Server 2,Project 7 -Web server 2,i-0521d47a45457af60,us-east-1c,t3.micro,Stopped
Web Server 3,Project7 - Web Server 3,i-0d8bf556a5cad4e74,us-east-1a,t3.micro,Stopped


