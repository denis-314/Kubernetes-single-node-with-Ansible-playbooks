# Kubernetes
Ansible Playbook for Kubernetes on Ubuntu 20.04


After the Deployment of ToDo app, the Ingress service was configured:

Ingress installation
NGINX was installed as Ingress Controller
"todo-ingress" Service was created, configured to use NGINX as Ingress Controller, and configured to present the "todo-app" Service over HTTP, on host todoapp.example.com, at the default "/" path
DEPLOYMENT STEPS:

All steps are performet on VM1:

l. Install Ansible:
    - sudo apt install ansible

2. Edit /etc/hosts and add the IP address and hostname of VM2

3. Reboot VM1:
    - sudo reboot
 
4. Generate SSH key and copy it on VM2, as root:
    - su root
    - ssh-keygen
    - cd .ssh/
    - ssh-copy-id root@<VM2_hostname>
DEPLOYMENT STEPS:

All steps are performet on VM1:

l. Deploy Kubernetes:
    - ansible-playbook -i hosts kubernetes_install.yml

2. Deploy ToDo app:
    - ansible-playbook -i hosts todo-app-install.yml
