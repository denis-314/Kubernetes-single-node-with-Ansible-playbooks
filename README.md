Follow the below steps to deploy a Kubernetes CLuster using Ansible Playbooks on Ubuntu 20.04

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
        - touch kubernetes.install.yml
     
    5. Copy the Ansible playbook content in it
        
    6. Make the file executable
        - chmod 755 kubernetes.install.yml
	
    7. Execute the Ansible playbook to deploy the Kubernetes cluster:
        - ansible-playbook -i hosts kubernetes_install.yml
_____________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

