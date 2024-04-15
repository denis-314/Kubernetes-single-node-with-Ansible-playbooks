Follow the below steps to deploy a Kubernetes Cluster using Ansible Playbooks on Ubuntu 20.04

_____________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

DEPLOYMENT STEPS:

    l. Install Ansible:
        - sudo apt install ansible

    2. Change directory to user home directory
        - cd /home/<user>
     
    3. Create a directory to store Ansible playbooks and change directory to it
        - mkdir ansible_playbooks
        - cd ansible_playbooks
     
    4. Create a YAML file for the ANsible playbook content
        - touch kubernetes_install.yml
     
    5. Copy the Ansible playbook content in it
        
    6. Make the file executable
        - chmod 755 kubernetes_install.yml
	
    7. Execute the Ansible playbook to deploy the Kubernetes cluster:
        - ansible-playbook -i hosts kubernetes_install.yml
_____________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________


IMPORTANT !

After a VM reboot, it is possible that Kubernetes cluster to be no longer available, reporting the following error:
	”The connection to the server <node>:6443 was refused - did you specify the right host or port?”

 In order to fix it, run the following commands, starting as kubernetes admin user:
 
    sudo -i
    swapoff -a
    exit
    strace -eopenat kubectl version

To check if the Kubernetes cluster is now available, run "kubectl get nodes".

To obtain the token and SHA key:

    kubeadm token list
    vi /etc/kubernetes/pki/ca.crt
