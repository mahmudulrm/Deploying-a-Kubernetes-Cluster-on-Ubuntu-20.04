# Deploying-a-Kubernetes-Cluster-on-Ubuntu-20.04

## Follow step 1 to step 6 on both machines
**Install Docker**
```bash
$ sudo apt update $ sudo apt install docker.io -y
```

**Enable Docker Service**
```bash
$ sudo systemctl start docker $ sudo systemctl enable docker
```
**Installing dependencies for https and cURL**
```bash
$ sudo apt install apt-transport-https curl
```
**Add Ubuntu Repository to download Kubernetes services**
```bash
$ curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add $ sudo apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
```
**Install Kubernetes modules**
```bash
$ sudo apt install kubeadm kubelet kubectl kubernetes-cni
```
**Disable Swap Memory**
```bash
$ sudo swapoff -a
```
**Set Hostnames
On Master Machine**
```bash
$ sudo hostnamectl set-hostname kube-master
```
**On Node**
```bash
$ sudo hostnamectl set-hostname kube-node1
```
**Initialize Kubernetes Master Server**

**On Master Machine**
```bash
$ sudo kubeadm init
```
**Set-up Kubeconfig to access Kubectl command**

**On Master Machine**
```bash
$ mkdir -p $HOME/.kube $ sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config $ sudo chown $(id -u):$(id -g) $HOME/.kube/config
```
**Deploy a Pod Network(WeaveNet)**

**On Master Machine**
```bash
$ kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"
```

**Register the Node to the Kubernetes Cluster**

On Node You'll find the join command as an output of kubeadm init command on step 8
