# Deploying-a-Kubernetes-Cluster-on-Ubuntu-20.04


    Follow step 1 to step 6 on both machines

1. Install Docker

$ sudo apt update
$ sudo apt install docker.io -y

2. Enable Docker Service

$ sudo systemctl start docker
$ sudo systemctl enable docker

3. Installing dependencies for https and cURL

$ sudo apt install apt-transport-https curl

4. Add Ubuntu Repository to download Kubernetes services

$ curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add
$ sudo apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"

5. Install Kubernetes modules

$ sudo apt install kubeadm kubelet kubectl kubernetes-cni

6. Disable Swap Memory

$ sudo swapoff -a

7. Set Hostnames

    On Master Machine

$ sudo hostnamectl set-hostname kube-master

    On Node

$ sudo hostnamectl set-hostname kube-node1

8. Initialize Kubernetes Master Server

    On Master Machine

$ sudo kubeadm init

9. Set-up Kubeconfig to access Kubectl command

    On Master Machine

$ mkdir -p $HOME/.kube
$ sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
$ sudo chown $(id -u):$(id -g) $HOME/.kube/config

10. Deploy a Pod Network(WeaveNet)

    On Master Machine

$ kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"

11. Register the Node to the Kubernetes Cluster

    On Node You'll find the join command as an output of kubeadm init command on step 8
