# Ansible Playbook to Setup a Kubernetes Cluster on Raspberry Pi 4

This playbook will deploy and configure a kubernetes cluster on a **raspberry pi 4B**, but it could work over any device running **Ubuntu 20.04**

What this playbook will do?

1. Remove root password if exists
2. Remove password authentication
3. Add all hosts in inventory to /etc/hosts
4. Change Hostname as defined in inventory file
5. Configure NTP settings
6. Update and Upgrade APT and install Aptitude
7. Install and enable if required following packages
    - apt-transport-https
    - ca-certificates
    - curl
    - gnupg-agent
    - software-properties-common
    - docker.io
    - kubedm
    - kubelet
    - kubectl
8. Enable CGROUP Memory and Reboot once
9. Setup kubernetes master node as defined in inventory file
10. Setup kubernetes worker nodes as defined in inventory file

Optionally you can reset the kubernetes cluster setup
This playbook has been developed for testing purposes in dev enviroments, it is not intended to run for production, however feel free to add as many tasks you want to make sure if fits to your purposes

## Prerequisites
* Nodes prepared with ssh keys for authentication

## Defaults
**network**: 172.168.10.0

## Variables
**kube_reset**: when **_true_** reset kubeadm and relaunch cluster from zero, default : **_false_**
**deploy_dashboard**: when **_true_** will deploy a kubernetes dashboard and user, default: **_false_**

## Setup instructions
file: _ansible.cfg_
1. setup values as your requirements, especially private_key_file = the path of your ssh key, defaul = ~/.ssh/raspberrypi

file: _hosts-dev_
2. fill the server addresses as it belongs, the example settings my raspberrypies have 192.168.10.118 and 192.168.10.119 addresses, I want the first one works as master and the following as slave node

### Running playbook examples

1. first run for a cluster for master and node (s)
`ansible-playbook setup-cluster.yml`
2. Join a node or nodes to an existing clusted
`ansible-playbook setup-nodes.yml`
3. Setup only the master node
`ansible-playbook setup-nodes.yml`
4. reset your cluster (s), this command will reset cluster and nodes
`ansible-playbook setup-cluster.yml -e kube_reset=true`
5. or just reset the nodes
`ansible-playbook setup-cluster.yml -e kube_reset=true`
6. Deploy kubernetes-dashboard 
`ansible-playbook setup-cluster.yml -e deploy_dashboard=true`
