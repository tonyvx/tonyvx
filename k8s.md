[Kubernetes Crash Course for Absolute Beginners](https://www.youtube.com/watch?v=s_o8dwzRlu4)
#### Table of Contents
[K8s Local Setup - Ubuntu 21.10](#k8s-local-setup---ubuntu-2110)
1. [Installation](#1-installation)
   1. [docker](#i-docker)
      1. [Executing the Docker Command Without Sudo (Optional)](#a-executing-the-docker-command-without-sudo-optional)
   1. [minikube](#ii-minikube)
   1. [kubectl](#iii-kubectl)
1. [minikube start](#2-minikube-start)

[k8s Architecture](#k8s-architecture)

# K8s Local Setup - Ubuntu 21.10
![miniKube Architecture](images/k8s/k8sClusterVSminiKube.png)

## 1) Installation 
[Back to top](#table-of-contents)

### i) docker
[Back to top](#table-of-contents)

_Refer [how-to-install-and-use-docker-on-ubuntu-20-04](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-20-04)_

First, update your existing list of packages: 
```sh
sudo apt update
``` 

Next, install a few prerequisite packages which let apt use packages over HTTPS:
```sh
sudo apt install apt-transport-https ca-certificates curl software-properties-common
```
 
Then add the GPG key for the official Docker repository to your system:
```sh
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```

Add the Docker repository to APT sources:
```sh
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
```
 
This will also update our package database with the Docker packages from the newly added repo.
Make sure you are about to install from the Docker repo instead of the default Ubuntu repo:
```sh
apt-cache policy docker-ce
```

You’ll see output like this, although the version number for Docker may be different:
```
## Output of apt-cache policy docker-ce
docker-ce:
  Installed: 5:20.10.10~3-0~ubuntu-focal
  Candidate: 5:20.10.10~3-0~ubuntu-focal
  Version table:
 *** 5:20.10.10~3-0~ubuntu-focal 500
        500 https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
        100 /var/lib/dpkg/status
     5:20.10.9~3-0~ubuntu-focal 500
        500 https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
     5:20.10.8~3-0~ubuntu-focal 500
        500 https://download.docker.com/linux/ubuntu focal/stable amd64 Packages
```
Notice that docker-ce is not installed, but the candidate for installation is from the Docker repository for Ubuntu 21.10.

Finally, install Docker:
```sh
sudo apt install docker-ce
```
 
Docker should now be installed, the daemon started, and the process enabled to start on boot. Check that it’s running:
```sh
sudo systemctl status docker
```
 
The output should be similar to the following, showing that the service is active and running:
```
## Output
● docker.service - Docker Application Container Engine
     Loaded: loaded (/lib/systemd/system/docker.service; enabled; vendor preset>
     Active: active (running) since Tue 2021-11-02 10:08:06 EDT; 11min ago
TriggeredBy: ● docker.socket
       Docs: https://docs.docker.com
   Main PID: 2548 (dockerd)
      Tasks: 13
     Memory: 108.6M
        CPU: 761ms
     CGroup: /system.slice/docker.service
             └─2548 /usr/bin/dockerd -H fd:// --containerd=/run/containerd/cont>

Nov 02 10:08:05 tony-XPS-13-9370 dockerd[2548]: time="2021-11-02T10:08:05.65649>
```

#### a) Executing the Docker Command Without Sudo (Optional)
[Back to top](#table-of-contents)
```sh
## If you want to avoid typing sudo whenever you run the docker command, add your username to the docker group:
sudo usermod -aG docker ${USER}
 
## To apply the new group membership, log out of the server and back in, or type the following:
su - ${USER}
 
## You will be prompted to enter your user’s password to continue.
## Confirm that your user is now added to the docker group by typing:
groups
 
## Output
avalantra sudo docker

## If you need to add a user to the docker group that you’re not logged in as, declare that username explicitly using:
sudo usermod -aG docker username
 
```

### ii) minikube
[Back to top](#table-of-contents)

_Refer_
* _[minikube.sigs.k8s.io](https://minikube.sigs.k8s.io/docs/start/)_
* _[minikube docker](https://minikube.sigs.k8s.io/docs/drivers/docker/)_

```sh

# To install the latest minikube stable release on x86-64 Linux using binary download:
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube

# Start a cluster using the docker driver:
minikube start --driver=docker

```

### iii) kubectl
[Back to top](#table-of-contents)

_Refer [install-kubectl-linux](https://kubernetes.io/docs/tasks/tools/install-kubectl-linux/)_

```sh
## Download the latest release with the command:
curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

## Download the kubectl checksum file:
curl -LO "https://dl.k8s.io/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl.sha256"

## Validate the kubectl binary against the checksum file:
echo "$(<kubectl.sha256) kubectl" | sha256sum --check

## If valid, the output is:
kubectl: OK

## Install kubectl
sudo install -o root -g root -m 0755 kubectl /usr/local/bin/kubectl

```

## 2) minikube start
[Back to top](#table-of-contents)

minikube is local Kubernetes, focusing on making it easy to learn and develop for Kubernetes.

All you need is Docker (or similarly compatible) container or a Virtual Machine environment, and Kubernetes is a single command away: 

```sh
○ → minikube start --driver docker
😄  minikube v1.23.2 on Ubuntu 21.10
✨  Using the docker driver based on existing profile
👍  Starting control plane node minikube in cluster minikube
🚜  Pulling base image ...
🔄  Restarting existing docker container for "minikube" ...
🐳  Preparing Kubernetes v1.22.2 on Docker 20.10.8 ...
🔎  Verifying Kubernetes components...
    ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5
🌟  Enabled addons: storage-provisioner, default-storageclass
🏄  Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default

```
## 3) minikube ingress
```sh
± |main → origin U:4 ?:2 ✗| → minikube addons enable ingress
    ▪ Using image k8s.gcr.io/ingress-nginx/controller:v1.0.0-beta.3
    ▪ Using image k8s.gcr.io/ingress-nginx/kube-webhook-certgen:v1.0
    ▪ Using image k8s.gcr.io/ingress-nginx/kube-webhook-certgen:v1.0
🔎  Verifying ingress addon...
🌟  The 'ingress' addon is enabled

````

### 4) kubectl commands to check ingress

```sh

± |main → origin U:4 ?:2 ✗| → minikube service webapp-service --url
http://192.168.49.2:31000

± |main → origin U:4 ?:2 ✗| → kubectl get ingress webapp
NAME     CLASS   HOSTS   ADDRESS        PORTS   AGE
webapp   nginx   *       192.168.49.2   80      8m22s

```


# K8s Architecture

_Refer [understanding-the-kubernetes-node](https://www.suse.com/c/rancher_blog/understanding-the-kubernetes-node/)_

![k8s-node-components-architecture](images/k8s/k8s-node-components-architecture.png)

