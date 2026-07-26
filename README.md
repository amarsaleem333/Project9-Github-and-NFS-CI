Project 9
Continuous Integration Pipeline: GitHub to NFS via Jenkins

Overview

This project establishes an automated Continuous Integration (CI) pipeline using Jenkins (v2.568.1) to track code changes in a GitHub repository, archive artifacts locally, and deploy updated source code directly to a 
target NFS server (/mnt/apps) via SSH using the Publish Over SSH plugin.

Infrastructure Overview (AWS EC2)

[ Developer Push ] ───> [ GitHub Repo: amarsaleem333/tooling ]
                                    │
                                 (Webhook)
                                    │
                                    ▼
                         [ Project 9 Jenkins ]
                      (IP: 3.89.202.227:8080)
                         Builds & Archives
                                    │
                            (SSH / Port 22)
                                    │
                                    ▼
                          [ Project 7 -NFS ]
                       (IP: 172.31.17.253)
                      Deploys to /mnt/apps

                      
