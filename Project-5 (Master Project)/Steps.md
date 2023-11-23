1. Create EC2 instance for Ansible, Jenkins and Kubernetes

- Go over the EC2 console, click on launch instance
- Choose the instance type as t2.small or bigger than this
- Select the AMI as ubuntu
- Download the new keypair for doing ssh into the instance, please make sure all three instances use the same keypair for doing ssh
- Update the security group for all the instances to allow traffice from everywhere to avoid multiple changes
- On the top left corner, change the count for instances to 3

2. Login into each of the EC2 instances in three seperate terminal

- Login to Jenkins server: ssh -i <download-location-of-login-key-pair-pem-file> ubuntu@<public-ip-of-jenkins-server>
- Login to Ansible sever: ssh -i <download-location-of-login-key-pair-pem-file> ubuntu@<public-ip-of-ansible-server>
- Login to Kubernetes/Web sever: ssh -i <download-location-of-login-key-pair-pem-file> ubuntu@<public-ip-of-web-server>

On each shell become the root user by running `sudo -i`, then run
a. set password for root : passwd and enter the password
b. set password for ubuntu user: passwd ubuntu

- Generate the SSH keys on each server connected terminal with the command `ssh-keygen -t rsa`
- Open the config file by runnning `vi /etc/ssh/sshd_config`. Uncomment PermitRootLogin by removing # and changing it to yes. Do the same with PasswordAuthentication and change it to yes as well
- Restart the ssh service by running `service sshd restart`
- To connect Jenkins and Ansible, on jenkins server terminal run `ssh-copy-id ubuntu@<ec2-private-ip-ansible-server>` to copy public key of ubuntu user to Ansible server. Enter the password for ubuntu user which you updated earlier.
- Now from each Jenkins and Ansible, Jenkins to Web Server / Kubernetes server by running `ssh-copy-id ubuntu@<ec2-private-ip-web-server>`

3. Install Jenkins

4. Set Jenkins Plugin

- Setup the jenkins server in the general way installing the suggested plugins
- Go to Manage Jenkins, then to Plugins and install ssh-agent in available plugins and install it

5. Set Anisble Server

- We need to setup docker and ansible on the EC2 instance.
- Create a shell script by running `vi ansible.sh`.
- Copy the contents of ansible-server.sh into ansible.sh
- Update the permissions by running, `chmod +x ansible.sh` and then run the shell script with command `./ansible.sh`
- Update the hosts file with the kubernetes server IP address for ansible to perform the operations. Run `vi /etc/ansible/hosts` and add below

```
[webnode]
<private-ip-kubernetes-server>
```

- You can check the connectivity to the server by running `ansible -m ping webnode -u ubuntu`

6. Set Kubernetes/ Web Server

Create the shell script similar to ansible and run the script kubernetes-server.sh to set up Minikube, Docker and Kubectl

7. Setup Jenkins pipeline

- Create the new item mentioning the name of the project and chooosing pipeline
- We need Dockerfile, Deployment and Service files to do deployment on Kubernetes server
- Go over to following github repo : https://github.com/kushaggarwal/MasterProject
- Either copy each of the files present in the above git repo or you can fork it to have it directly in your account
- Update the deployment.yaml file to update image name with the one present into your Dockerhub account where the Jenkins pipeline will update the latest image

8. Setup ansible and kubernete-server ssh-agent variables

- Go over to the jenkins project created previously and click on Pipeline Syntax under Pipeline Script section
- Select sshagent option from the Sample Step dropdown and click Add button and click Jenkins icon from it.
- In new pop-up window, select “SSH username with private key”. Then enter ID and description as ansible-server. Then set the username as “ubuntu”. Then select the Enter directly option in Private key and click add. In the resulting input field paste the content of .pem file which you downloaded while creating login key pair. Click Add.
- Do the same for Kubernetes/Web server and generate kubernetes-server variable.
- Register on DockerHub then on the Pipeline Syntax page. Select withCredentials in the Sample Step dropdown field. Click Add button under Binding section and select “secret text” and enter variable name, like, “dockerhub_passwd”. Then under credentials sub-section, click add, click Jenkins icon. In the pop-up window, select secret text as kind and enter the ID same variable name as variable name you used. Click add to close pop-up window
- Update the pipeline script present in Jenkinsfile to create the pipeline. Replace devops-project-one with your jenkins project name and kushaggarwal with your dockerhub username
- Update ansible_server_private_ip and kubernetes_server_private_ip with the respective IP for your ansible and kubernetes instance

9. SSH into the Kubernetes server and check for minikube to be running with command `minikube status`.
