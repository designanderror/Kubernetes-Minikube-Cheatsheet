# Minikube-Cheatsheet - Kali Linux

This repository contains Installation of Minikube over Kali Linux and some basic commands to play around with minikube.

**Make sure you have 4 processor cores 4 GB of RAM and atleast 50 GB of space allocated to Kali Linux Virtual Machine**

## Creating and adding a new user

```
adduser <username>
```
Create and Enter the password you want for your username. If you dont wan to enter any further information then simply press enter and at last press "Y" 

#### Adding user to sudo group 
```
usermod -aG sudo <username>
  ```

#### Login to the newly created User 

```
su - <username>
```
Then enter the password


## Installing Docker on Kali Linux
#### 1. Update the Kali 

 ``` 
 sudo apt update 
 ```
#### 2. Installing Docker 
 
```
sudo apt install -y docker.io
```

#### 3. Enabling Docker on the Kali Machine
```
sudo systemctl enable docker --now
```
#### 4. Check the installation and version of Docker
```
docker --version
```
#### 5. Adding user to docker group (Optional) 
```
sudo usermod -aG docker $USER
```
**If you donot want to add the user to the docker Group then run the commands using sudo**
The final thing is to logout and in again once you add the user to docker group.

## Installing docker-ce on Kali Linux
docker-ce can be installed from Docker repository. One thing to bare in mind, Kali Linux is based on Debian, so we need to use Debian's current stable version

```
printf "%s\n" "deb [arch=amd64] https://download.docker.com/linux/debian buster stable" \ | sudo tee /etc/apt/sources.list.d/docker-ce.list
```
#### Import the gpg key:

```
curl -fsSL https://download.docker.com/linux/debian/gpg \ | sudo apt-key add -
  ```
#### Fingerprint checking:

```
sudo apt-key fingerprint 0EBFCD88
```
#### Install the latest version of docker-ce:

```
sudo apt install -y docker-ce docker-ce-cli containerd.io
```

## Install Minicube
```
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
chmod +x minikube
mv ./minikube /usr/local/bin/minikube
```
## Start minikube with Docker Driver
```
minikube start --driver=docker
```

## Verify minikube Installation
```
docker ps
```

## Install Kubectl
To deploy and manage clusters, you need to install kubectl, the official command line tool for Kubernetes.

#### 1. Download kubectl with the following command:
```
curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl
Download Kubectl binary on Ubuntu.
```
#### 2. Make the binary executable by typing:
```
chmod +x ./kubectl
```
#### 3. Then, move the binary into your path with the command:
```
sudo mv ./kubectl /usr/local/bin/kubectl
```
#### 4. Verify the installation by checking the version of your kubectl instance:
```
kubectl version -o json
```
