Follow the below steps to deploy a Kubernetes Cluster using Ansible Playbooks on Ubuntu 20.04

1. On Master Control Plane, run the kubernetes_install.yml. Use the Deployment steps below.
   	- Change the Node Name in steps „9. Set node hostname” and „22. taint node master”
   	  
3. To find the join command, run:

       kubeadm token create --print-join-command
   
4. On Nodes, run the kubernetes_install_node.yml. Use the same Deployment steps
   	- Change the Node Name in step „9. Set node hostname”
   	- Run the join command obtained previously at step 3:
  
          sudo kubeadm join 10.40.0.132:6443 --token cg9fgp.ucsvbrgpw0vd2tic --discovery-token-ca-cert-hash sha256:0d472d7fb5907eebf9344e70258c62edc208db97721af240483ce686c8a6b5ab

   
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

To generate the join node command on the control-plane master node, or to list the token and SHA key:

    kubeadm token create --print-join-command
    kubeadm token list
    openssl x509 -pubkey -in /etc/kubernetes/pki/ca.crt | openssl rsa -pubin -outform der 2>/dev/null | \openssl dgst -sha256 -hex | sed 's/^.* //'

