docker-oracle-xe-11g
==
Oracle XE - Dockerfile
==

This repository contains a Dockerfile to create a docker container with Oracle Express Edition 11g Release 2 and Ubuntu 14.04 LTS (Trusty)

This Dockerfile has been published as a trusted build to the public Docker Registry.

How-To: Build this image
--

If you want to build this image and use latest Oracle XE version, you will need to download Oracle XE from Oracle site.

Then you will also need to convert download rpm file into deb, using alien tool.

Run following command to convert down
loaded rpm package into deb.

```Bash
sudo alien oracle-xe-11.2.0-1.0.x86_64.rpm
```
I also keep, already downloaded Oracle XE image in GitHub repository, split into 3 pieces, due to GitHub 100MB file limit. Original file is split by running split command and merged back with cat command (Google for how to use both commands).

How-To: Install and Use
--

```Bash
docker pull alexeiled/docker-oracle-xe-11g
```

Note: It's important to run Oracle XE with >1GB shared memory.

Start Oracle XE
--

Running Oracle XE in detached mode with 1521 and 8080 ports opened and 2GB shared memory:

```Bash
docker run -d --shm-size=2g -p 1521:1521 -p 8080:8080 alexeiled/docker-oracle-xe-11g
```

Start Oracle XE and execute SQL on startup
--

Put your *.sql files for database init into some local folder and mount this folder during container startup to /etc/entrypoint-initdb.d volume.

```Bash
docker run -d --shm-size=1g -p 8080:8080 -p 1521:1521 -v /local-initdb:/etc/entrypoint-initdb.d alexeiled/docker-oracle-xe-11g
```

Connect
--

Connect database with following setting:

```Bash
hostname: localhost
port: 1521
sid: xe
username: system
password: oracle
```


```Bash
oracle
```
Connect to Oracle Application Express web management console with following settings:

```Bash
url: http://localhost:8080/apex
workspace: internal
user: admin
password: oracle
Do not forget to change admin password!
```