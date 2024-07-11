# prometheus_nodeexporter_grafana_CAdvisor

I made changes for those who are stuggling with Exited (255) for cadvisor. 

Did nothing more, just changed the image source and add a command. ie. 

**** Test with the Latest Version of cAdvisor****
Ensured we are using the latest version of cAdvisor, as newer versions may have better support for cgroup2.

**Ran cAdvisor with Debug Logging**
To get more detailed logs, I ran cAdvisor with debug logging enabled. Modified our old docker-compose.yml to include the --v=4 flag.
