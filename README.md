# RealTime_DevOps_Project1
Some Mannual commands to be performed on servers after running terraform

Step-1: Nexus-Server 
- vi /opt/nexus/bin/nexus.vmoptions \
(Note: Remove one dot prefix to nexus, wherever we find, almost in 4 lines)
- vi /opt/nexus/bin/nexus.rc \
(Note: uncomment run_as_user and also mention "nexus")
- sudo -u nexus /opt/nexus/bin/nexus start \
(Note: Nexus default port is 8081, open it in browser using public IP of Nexus)
- cat "paste location" \
(Note: above command is to get a nexus password. After hitting enter we can get password- copy that till root)


Step-2: On Master-server
- kubeadm init --pod-network-cidr=192.168.0.0/16 \
 (Note:Copy the token and paste it into the worker node.)
- exit
- mkdir -p $HOME/.kube
- sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
- sudo chown $(id -u):$(id -g) $HOME/.kube/config
- kubectl apply -f https://docs.projectcalico.org/manifests/calico.yaml
- kubectl apply -f https://raw.githubusercontent.com/kubernetes/ingress-nginx/controller-v0.49.0/deploy/static/provider/baremetal/deploy.yaml
- kubectl get nodes

