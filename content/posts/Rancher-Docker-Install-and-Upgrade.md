---
title: "Installing and Upgrading Rancher via Docker"
date: 2023-02-02T12:00:46-05:00
draft: true
---
**Author:** [**Jameson McGhee**](https://www.linkedin.com/in/jameson-mcghee-ctfl/)


## Install Docker (Preferred Rancher method):

`curl https://releases.rancher.com/install-docker/20.10.sh | sh`


## Install Docker (Standard method):

- `sudo apt-get update && \
   sudo apt -y install docker.io && \
   sudo systemctl start docker && \
   sudo systemctl enable docker && \
   docker --version`


## Install Rancher via Docker:

- `sudo docker run -d --restart=unless-stopped -p 80:80 -p 443:443 --privileged -e CATTLE_BOOTSTRAP_PASSWORD=admin rancher/rancher:`*{RANCHER_VERSION - e.g. v2.6.9}*


## Upgrade Rancher from a Docker Installation:

- `sudo docker ps`
	- This allows you to obtain the **CONTAINER ID** of rancher server that is running)
- `sudo docker stop` *{CONTAINER ID}*
- `sudo docker create --volumes-from` *{CONTAINER ID}* `--name rancher-data rancher/rancher:`*{PREVIOUS RANCHER_VERSION - e.g. v2.6.9}*
- `sudo docker run -d --privileged --volumes-from rancher-data --restart=unless-stopped -p 80:80 -p 443:443 rancher/rancher:`*{NEW RANCHER_VERSION - e.g. v2.7.0}*