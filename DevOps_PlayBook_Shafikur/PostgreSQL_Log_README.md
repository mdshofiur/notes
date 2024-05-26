### Troubleshooting PostgreSQL Using Docker Logs:

**Introduction:**
PostgreSQL is a powerful open-source relational database system, often deployed using Docker containers for easy management and scalability. This document outlines steps to troubleshoot PostgreSQL instances running in Docker containers by examining logs and configuring logging options.

**Prerequisites:** 

- Basic understanding of Docker
- Basic knowledge of PostgreSQL
- Access to a terminal with Docker installed

**Troubleshooting Steps:** 

**Way-1:-**

- Viewing Docker Logs:

```bash
docker logs postgresql-container
```

**Way-2:-**

```
docker exec -it postgresql-container /bin/bash

* Creating Errors for Testing:
psql -U my_user my_database
SELECT * FROM non_existent_table;


```

**Checking Log Files:**
By default, PostgreSQL logs are stored in /var/lib/postgresql/data/log/. You can navigate to this directory to view log files:

```
cd /var/lib/postgresql/data/log/
```

**Additional configuration may be required if the log folder and file are not present.:**

```
Configuring Logging Options:--

echo "logging_collector = on" >> postgresql.conf
echo "log_directory = 'log'" >> postgresql.conf
echo "log_filename = 'postgresql-%Y-%m-%d.log'" >> postgresql.conf

Restarting Docker Container:--

docker restart postgresql-container

```