# Ansible Playbook to Setup a Kubernetes Cluster on Raspberry Pi 4

## Prerequisites
* Nodes prepared with ssh keys for authentication

### Defaults
network: 172.168.10.0

### Variables
kube_reset: when _true_ reset kubeadm and relaunch cluster from zero, default : _false_
deploy_dashboard: when _true_ will deploy a kubernetes dashboard and user, default: _false_

## Setup instructions
file: ansible.cfg
1. setup values as your requirements, especially private_key_file = the path of your ssh key, defaul = ~/.ssh/raspberrypi

file: hosts-dev
2. fill the server addresses as it belongs, the example settings my raspberrypies have 192.168.10.118 and 192.168.10.119 addresses, I want the first one works as master and the following as slave node



