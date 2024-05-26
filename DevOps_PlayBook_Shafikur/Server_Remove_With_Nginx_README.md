# This script removes specified server addresses from the Nginx configuration, stops, and removes specific Docker containers.


## Prerequisites

- Ensure you have Nginx installed and configured on your system.
- Docker must be installed and running.




### Create and give permission to the bash file
```

sudo nano my_script.sh

chmod +x my_script.sh
```

```
#!/bin/bash

# Define the server addresses and ports
servers=("localhost:8081" "localhost:8082")

# Path to your nginx configuration file
nginx_conf="/etc/nginx/nginx.conf"


# Function to remove servers from upstream block
remove_servers_from_upstream() {
    for server in "${servers[@]}"; do
        sed -i "/server $server;/d" $nginx_conf
    done
}

# Function to stop and remove Docker containers
stop_and_remove_containers() {
    docker stop dev_app-container_1
    docker rm dev_app-container_1
    docker stop prod_app-container_1
    docker rm prod_app-container_1
}

# Check if nginx configuration file exists
if [ ! -f "$nginx_conf" ]; then
    echo "Nginx configuration file not found: $nginx_conf"
    exit 1
fi


# Reload nginx to apply changes
# nginx -s reload

# Docker run command
# docker run -d -p 8081:8080 --name dev_app-container_1 shafikur/aspdotnet-app:dev
# docker run -d -p 8082:8080 --name prod_app-container_1 shafikur/aspdotnet-app:prod

# Stop and remove Docker containers
stop_and_remove_containers

# Remove servers from upstream block
remove_servers_from_upstream

# Reload nginx to apply changes
nginx -s reload



```

### Run the script with server addresses as arguments:

```
sudo bash ./my_script.sh localhost:8083 localhost:8084

```
    
