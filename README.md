# RealTime_DevOps_Project1

Nexus-Server configuration after running terraform 
- vi /opt/nexus/bin/nexus.vmoptions \
(Note: Remove one dot prefix to nexus, wherever we find, almost in 4 lines)
- vi /opt/nexus/bin/nexus.rc \
(Note: uncomment run_as_user and also mention "nexus")
- sudo -u nexus /opt/nexus/bin/nexus start \
(Note: Nexus default port is 8081, open it in browser using public IP of Nexus)
- cat "paste location" \
(Note: above command is to get a nexus password. After hitting enter we can get password- copy that till root)
