sudo dnf install java-11-amazon-corretto
sudo dnf install java-11-amazon-corretto-devel
java -version
sudo wget -O /etc/yum.repos.d/jenkins.repo \
 https://pkg.jenkins.io/redhat-stable/jenkins.repo

sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
sudo dnf install jenkins -y

jenkins --version

service jenkins start

Redirecting to /bin/systemctl start jenkins.service
Failed to start jenkins.service: Access denied
See system logs and 'systemctl status jenkins.service' for details.

systemctl status jenkins

sudo yum install git
