### Troubleshooting NGINX Using Docker Logs

**Introduction:**

NGINX is a high-performance web server and reverse proxy server, often deployed using Docker containers for ease of management and scalability. This document outlines steps to troubleshoot NGINX instances running in Docker containers by examining logs and configuring logging options.

**Prerequisites:**

- Basic understanding of Docker
- Basic knowledge of NGINX
- Access to a terminal with Docker installed

**Troubleshooting Steps:**

**Way-1:**

- Viewing Docker Logs:

```bash
docker logs nginx-container
```

**Way-2:**
```
docker exec -it nginx-container /bin/bash

# Modify the configuration to include an invalid directive:

echo "invalid_directive;" >> /etc/nginx/nginx.conf
nginx -s reload


# Request a non-existent resource to generate a 404 error:

curl http://localhost/non_existent_page

```


- Checking Log Files

NGINX log files are typically located in **`/var/log/nginx/`**. You can navigate to this directory to view access and error logs:

```
cd /var/log/nginx/
cat error.log

To monitor logs in real-time, use the tail command with the -f option:

tail -f error.log
```

- Configuring Logging Options:

If you need to configure additional logging options, edit the NGINX configuration file (**`nginx.conf`**). For example, to enable debug logging, you can add the following directive:

```
echo "error_log /var/log/nginx/error.log debug;" >> /etc/nginx/nginx.conf


nginx -s reload


docker restart nginx-container

```


### Conclusion:
Troubleshooting NGINX within a Docker container involves examining logs and configuring logging options to capture relevant information. You can diagnose and resolve issues effectively by leveraging Docker commands to view logs and access the container's filesystem. Understanding NGINX's logging mechanisms and using tools like curl enables efficient troubleshooting of server-related problems in a containerized environment.