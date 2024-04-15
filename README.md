Follow the below Deployment Steps to deploy a Kubernetes Cluster using Ansible Playbooks on Ubuntu 20.04

1. On Master Control Plane, follow the Deployment Steps from below, but use the kubernetes_install.yml
   	- Change the Node Name in steps „9. Set node hostname” and „22. taint node master”
   	  
3. To find the join command, on Master Control Plane, run:

       kubeadm token create --print-join-command
   
4. If you want to add aditional nodes, run the same Deployment Steps from below on each Node, but use the kubernetes_install_node.yml file instead
   	- Change the Node Name in step „9. Set node hostname”
   	- Run the join command obtained previously at step 3:
   	  	sudo kubeadm join <Master_Control_Plane_IP>:6443 --token <token_from_Control_Plane> --discovery-token-ca-cert-hash sha256:<Key_from_Control_Plane>
  
          sudo kubeadm join 10.40.0.132:6443 --token cg9fgp.ucsvbrgpw0vd2tic --discovery-token-ca-cert-hash sha256:0d472d7fb5907eebf9344e70258c62edc208db97721af240483ce686c8a6b5ab

	- If multiple sockets are present and the join command gives an error about this, use the flag "--cri-socket=" to point to the right socket. For example:

          sudo kubeadm join 10.40.0.132:6443 --cri-socket=unix:///var/run/crio/crio.sock --token cg9fgp.ucsvbrgpw0vd2tic --discovery-token-ca-cert-hash sha256:0d472d7fb5907eebf9344e70258c62edc208db97721af240483ce686c8a6b5ab

_____________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________________

DEPLOYMENT STEPS:

    l. Install Ansible:
    sudo apt install ansible

    2. Change directory to user home directory
    cd /home/<user>
     
    3. Create a directory to store Ansible playbooks and change directory to it
    mkdir ansible_playbooks
    cd ansible_playbooks
     
    4. Create a YAML file for the ANsible playbook content
    touch kubernetes_install.yml
     
    5. Copy the Ansible playbook content in it
        
    6. Make the file executable
    chmod 755 kubernetes_install.yml
	
    7. Execute the Ansible playbook to deploy the Kubernetes cluster:
    ansible-playbook -i hosts kubernetes_install.yml
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

