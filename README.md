# prometheus_nodeexporter_grafana_CAdvisor

I made changes for those who are stuggling with Exited (255) for cadvisor. 

Did nothing more, just changed the image source and add a command. ie. 

**Test with the Latest Version of cAdvisor**
Ensured we are using the latest version of cAdvisor, as newer versions may have better support for cgroup2.

**Ran cAdvisor with Debug Logging**
To get more detailed logs, I ran cAdvisor with debug logging enabled. Modified our old docker-compose.yml to include the --v=4 flag.

**How & why ?**
See if you still hvaing the issue. Then understand why we get this exited 255. The Exited (255) status for cAdvisor in Docker typically indicates that the container encountered an error and stopped. Here are some steps to diagnose and resolve the issue:

Steps to Diagnose:
Check Container Logs:
Use docker logs <container_id> to check the logs for the cAdvisor container to see if there are any error messages that provide clues.

 ```sh

docker logs <container_id>
Verify docker-compose.yml:
Ensure that your docker-compose.yml file is correctly configured. I have attached an example configuration for cAdvisor in docker-compose.yml
Check Volume Mounts:
Ensure that the volume mounts in the docker-compose.yml file are correct and that cAdvisor has the necessary permissions. Note that in your setup, you needed to avoid read-only mount points to resolve an issue.

Inspect Resource Limits:
Check if there are any resource limits (memory, CPU) that might be causing the container to exit.

 ```sh

docker inspect <container_id>

Common Issues and Fixes:
Permission Issues:
Ensure that cAdvisor has the necessary permissions to read the directories it needs. This might involve adjusting the permissions of the directories or the Docker daemon configuration.

Incompatible cAdvisor Version:
Make sure you are using a version of cAdvisor that is compatible with your Docker and host system.

Conflicting Container:
Ensure that no other container is conflicting with cAdvisor's ports or mounts.

System Configuration:
If your system uses cgroup2 and Ubuntu 22.04, like it was in my case, ensure cAdvisor is compatible with cgroup2.

Next Steps:
Check logs and inspect the container:

 ```sh

docker logs cadvisor

Ensure Correct cgroup Mount Points
Run the following command to verify the cgroup mount points on your host:

 ```sh

mount | grep cgroup
docker inspect cadvisor
Verify volume mounts and permissions.

Update docker-compose.yml if necessary.

Restart the cAdvisor container:

 ```sh

docker-compose up -d cadvisor
