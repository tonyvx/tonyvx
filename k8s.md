
# K8s Local Setup - Ubuntu 21.10

## Installation

### docker
_Refer [how-to-install-and-use-docker-on-ubuntu-20-04](https://www.digitalocean.com/community/tutorials/how-to-install-and-use-docker-on-ubuntu-20-04)_

```sh
## First, update your existing list of packages:
sudo apt update
 
## Next, install a few prerequisite packages which let apt use packages over HTTPS:
sudo apt install apt-transport-https ca-certificates curl software-properties-common
 
## Then add the GPG key for the official Docker repository to your system:
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
 
## Add the Docker repository to APT sources:
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
 
## This will also update our package database with the Docker packages from the newly added repo.

## Make sure you are about to install from the Docker repo instead of the default Ubuntu repo:
apt-cache policy docker-ce
 
## You’ll see output like this, although the version number for Docker may be different:
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
   
 
## Notice that docker-ce is not installed, but the candidate for installation is from the Docker repository for Ubuntu 20.04 (focal).

## Finally, install Docker:
sudo apt install docker-ce
 
## Docker should now be installed, the daemon started, and the process enabled to start on boot. Check that it’s running:
sudo systemctl status docker
 
## The output should be similar to the following, showing that the service is active and running:
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

#### Executing the Docker Command Without Sudo (Optional)
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

### minikube
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

### kubectl

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
