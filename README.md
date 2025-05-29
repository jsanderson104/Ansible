# Designed for RHEL9.
# This repository is for public consumption but at your own risk.

# How to use:
  - Need 4 VM's on RHEL9. (1 Master, and 3 Workers)
  - Do NOT use this role over-and-over" and expect it to be a solid cluster. If it messes, revert your snapshots on all of them and start over.
     - You don't need a hosts file. I do that.
     - I set the hostname FQDN of all nodes based on inventory names and a var called 'service_dns_domain'.
     - You can modify the hosts file that gets deployed. The template is located at ./kubecluter/templates/hosts.j2
     - Alternatively, you can just use the inventory ansible_host option to tag a system in /etc/hosts. 
  - Ansible should be able to ssh and sudo to all nodes without any prompts. (ie - SSHPUBKEYS and SUDONOPASSWD).
      a) Make adjustments for security on your own discretion. This is a lab build and used for development/learning.
      b) I used account name:  automation
  - All VM's should be able to route each other. For ease, just put them on the same subnet.
  - Installed a GUI on the Control Node to use firefox when testing the Kube Dashboard deployment. We won't have to depend on an ingress controller to test the dashboard.
  - All nodes tend to run under decent load at idle due to kubelet service(s) so you'll want to make sure you're CPU cores are decent. Memory didn't seem to be taxed too much so far.
       a) During the cluster install role (this role), at the HELM and GO installations, the CPU is intense and takes a while to run because it's compiling the applications from source. Be patient - it hasn't halted or zombied.

** Setup your 4+ vm's and get everything talking and ssh to/from the ansible controller is working as expected (ssh and sudo) 
** Take a Snapshot of all 4 VM's in a powered off state. Boot up all 4+ VMs for the cluster you're building THEN run this Ansible role.
** Reboot is not necessary during or after the role has been executed.


This 'kubecluster' Ansible role is designed to setup a small VM lab network that I use for testing Kubernetes while I train for the certification.
But, for all intents and purposes, this Ansible role doesn't care if it's a home vm or a server room - works the same.
I made this a 4-node cluster with 3-workers because a default Kubernetes replicaset needs 3 workers to be truly protected (or atleast that was my understanding of how replicasets work)

# 1. The ip's of the vm's I use for the lab are defined in the inventory file, which should really just be FQDN's of your intended cluster nodes.
     Let DNS verify the names for Ansible since it will be crucial that DNS is performing properly for the cluster any way.

# To generate a new token to join nodes to cluster manually, run:   kubeadm token create |grep -v TOKEN |awk '{print $1}'

# As of this release on 05/29/25, I believe I have made the role more "default" or "generic" in how it builds the cluster. Notice the new playbooks and tasks in main.yml. 

