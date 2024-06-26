# Nginx Configuration Script to Scale Up Multiple Servers with Passed Server Addresses as Arguments.

This script sets up an Nginx configuration to load balance between multiple servers and runs Docker containers for an ASP.NET application.

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

# Check if at least two parameters (server and container) are provided
if [ "$#" -lt 2 ]; then
    echo "Usage: $0 server1:port1 container_name1 [server2:port2 container_name2 ... serverN:portN container_nameN]"
    exit 1
fi

# Collect server addresses and container names from command-line arguments
servers=()
container_names=()
while [ "$#" -gt 0 ]; do
    servers+=("$1")
    container_names+=("$2")
    shift 2
done

# Path to your nginx configuration file
nginx_conf="/etc/nginx/nginx.conf"

# Function to add servers to upstream block
add_servers_to_upstream() {
    for server in "${servers[@]}"; do
        sed -i "/upstream backend {/a \    server $server;" $nginx_conf
    done
}


# Check if nginx configuration file exists
if [ ! -f "$nginx_conf" ]; then
    echo "Nginx configuration file not found: $nginx_conf"
    exit 1
fi


# Add servers to upstream block
add_servers_to_upstream


# Reload nginx to apply changes
nginx -s reload

# Docker run command
for i in "${!servers[@]}"; do
    port=$(echo "${servers[$i]}" | cut -d':' -f2)
    docker run -d -p $port:8080 --name "${container_names[$i]}" shafikur/aspdotnet-app:dev
done

```

### Run the script with server addresses as arguments:

```
sudo bash ./my_script.sh localhost:8083 localhost:8084

```