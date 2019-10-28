# OpenShift - Install on Parallels


These instruction are for development only. Do not use this setup in a production environment!


## Resources

https://docs.openshift.com/container-platform/3.11/install/

## Prerequisites

vi /etc/environment

```
LANG=en_US.utf-8
LC_ALL=en_US.utf-8
```

sudo subscription-manager register --username [username]
sudo subscription-manager subscribe

### Generate Keypair on Master 
```
ssh-keygen -t ecdsa -b 256
ssh-copy-id ansible@10.211.55.33     # Master
ssh-copy-id ansible@10.211.55.34     # Node 1
ssh-copy-id ansible@10.211.55.36     # Node 2

subscription-manager repos --disable="*"
subscription-manager refresh
subscription-manager list --available --matches '*OpenShift*'
subscription-manager attach --pool=[pool_id]
subscription-manager repo --enable="rhel-7-server-rpms" --enable="rhel-7-server-extras-rpms" --enable="rhel-7-server-ose-3.11-rpms" --enable="rhel-7-server-ansible-2.6-rpms"
yum -y install wget git net-tools bind-utils yum-utils iptables-services bridge-utils bash-completion kexec-tools sos psacct
yum -y update
yum -y install docker-1.13.1
yum -y install atomic
reboot
```

## OpenShift Ansible RPM Based Installation
```
yum -y install openshift-ansible 
cd /usr/share/ansible/openshift-ansible
ansible-playbook -i /root/inventory.ini playbooks/prerequisites.yml
```
