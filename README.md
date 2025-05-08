# justin.sanderson104@gmail.com
# Designed for RHEL9.
# This repository is for public consumption but at your own risk.

This 'kubecluster' Ansible role is designed to setup a small VM lab network that I use for testing Kubernetes while I train for the certification.
But, for all intents and purposes, this Ansible role doesn't care if it's a home vm or a server room - works the same.

# Key notes about the role:
# 1. "control.k8s.sanderson.com" is the only kube cluster control plane (eg - cluster mgr). It's specific name is used exclusively in ../tasks/init_k8s.yml
#     so if you don't want your cluster manager to be named something differently then you'll need to change it in the tasks/*.yml files. It's only 2 or 3 entries.
      or you can fix the code for me and send it to me. ;) 

# 2. the ip's of the vm's i use for the lab are defined in the inventory file, which should really just be FQDN's of your intended cluster nodes.
     Let DNS verify the names for Ansible since it will be crucial that DNS is performing properly for the cluster any way.

# To generate a new token to join nodes to cluster manually, run:   kubeadm token create |grep -v TOKEN |awk '{print $1}'

