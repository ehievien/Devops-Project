1. Go to .ssh directory to copy the host keypair

`$ cd ~/.ssh`

2. Create a keypair file by the name ansible_key and the private key data to it

`$ vi ansible_key`

3. Go back to root directory and create ansible directory for hosts file

`$ cd`
`$ mkdir ansible && cd ansible`
`$ touch hosts`

4. Edit the hosts file to add the hosts information as present in hosts.txt, replace the IP address with publicj
   IP of your EC2 instances

5. Check the inventory using ansible command

`$ ansible-inventory --list -y -i /home/ubuntu/ansible/hosts`

6. Try pinging instance to check connectivity, type yes to add each hosts into ansible master

`$ ansible all -m ping -i /home/ubuntu/ansible/hosts --private-key=~/.ssh/ansible_key`

7. Copy any playbook from the playbook folder to check for any syntax issues

`$ ansible-playbook <playbook-file-name> --syntax-check`

8. Run the playbook to perform the operations over the related instances

`$ ansible-playbook <playbook-file-name> -i /home/ubuntu/ansible/hosts --private-key=~/.ssh/ansible_key`
