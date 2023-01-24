# RealTime_DevOps_Project1
All required Servers created using terraform file 'servers.tf' and below commands are for further configuration of those servers

Server-1: Jenkins-server
- udo apt update -y
- sudo apt install default-jre -y
- wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key
- sudo apt-key add -
- sudo sh -c "echo deb https://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list"
- sudo apt update -y
- sudo add-apt-repository universe -y
- sudo apt-get install jenkins -y
- sudo service jenkins start \
(Note: Open jenkins in browser using public ip and port 8080)

Server-2: SonarQube-server
- sudo apt update -y
- sudo apt install apt-transport-https ca-certificates curl software-properties-common -y
- curl -fsSL https://download.docker.com/linux/ubuntu/gpg
- sudo apt-key add -
- sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable" -y
- sudo apt update -y
- apt-cache policy docker-ce -y
- sudo apt install docker-ce -y
- sudo chmod 777 /var/run/docker.sock
- docker run -d --name sonarqube -p 9000:9000 -p 9092:9092 sonarqube

Server-3: Nexus-Server 
- apt-get update -y
- echo 'Install Java'
- apt-get install openjdk-8-jdk -y
- echo "Install Nexus"
- useradd -M -d /opt/nexus -s /bin/bash -r nexus
- echo "nexus ALL=(ALL) NOPASSWD: ALL" > /etc/sudoers.d/nexus
- mkdir /opt/nexus
- wget https://sonatype-download.global.ssl.fastly.net/repository/downloads-prod-group/3/nexus-3.29.2-02-unix.tar.gz
- tar xzf nexus-3.29.2-02-unix.tar.gz -C /opt/nexus --strip-components=1
- chown -R nexus:nexus /opt/nexus
- vi /opt/nexus/bin/nexus.vmoptions \
(Note: Remove one dot prefix to nexus, wherever we find, almost in 4 lines)
- vi /opt/nexus/bin/nexus.rc \
(Note: uncomment run_as_user and also mention "nexus")
- sudo -u nexus /opt/nexus/bin/nexus start \
(Note: Nexus default port is 8081, open it in browser using public IP of Nexus)
- cat "paste location" \
(Note: above command is to get a nexus password. After hitting enter we can get password- copy that till root)

Server-4: Master-server
- sudo su
- apt-get update
- apt-get install docker.io -y
- service docker restart
- curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg
- apt-key add -
- echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" >/etc/apt/sources.list.d/kubernetes.list
- apt-get update
- apt install kubeadm=1.20.0-00 kubectl=1.20.0-00 kubelet=1.20.0-00 -y
- kubeadm init --pod-network-cidr=192.168.0.0/16 \
 (Note:Copy the token and paste it into the worker node.)
- exit
- mkdir -p $HOME/.kube
- sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
- sudo chown $(id -u):$(id -g) $HOME/.kube/config
- kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml
- kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.49.0/deploy/static/provider/baremetal/deploy.yaml
- kubectl get nodes

Server-5: Node-server
- sudo su
- apt-get update
- apt-get install docker.io -y
- service docker restart
- curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg
- apt-key add -
- echo "deb http://apt.kubernetes.io/ kubernetes-xenial main" >/etc/apt/sources.list.d/kubernetes.list
- apt-get update
- apt install kubeadm=1.20.0-00 kubectl=1.20.0-00 kubelet=1.20.0-00 -y

