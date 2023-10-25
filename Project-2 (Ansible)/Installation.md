To check if ansible is installed on the server or not, run the below command

`$ ansible`

if you get command not found, we need to install ansible

To install ansible, run the below command (please specift the package manager for your linux distro)
This is an example for ubuntu

`$ sudo apt-get install ansible`

Ansible needs python to run and update related hosts configuration, check python with below command and
if not present you can install with below steps

Check for python3

`$ python3`

If shown command not found, run the below commands for installation

`$ sudo apt-get install python3`
